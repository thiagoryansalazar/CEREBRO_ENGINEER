# Fluxos - LOG_VENCIMENTOS

## 1. Leitura lógica da Arquitetura Geral

O artefato reconstruído em 2026-06-30 é uma **Arquitetura Geral**, não apenas um
fluxo de funcionamento. A leitura abaixo explica as relações desenhadas:

```text
Fornecedor entrega o lote
  → conferente aceita ou rejeita
  → se aceito, a empresa registra os dados no ERP
  → Adaptador de Consulta ERP consulta o Repositório de Lotes do ERP
  → adaptador encaminha os dados ao LOG
  → monitoramento calcula o risco
  → serviço de alertas notifica o gestor
  → gestor analisa indicadores e direciona a conferência
  → repositor verifica o lote fisicamente
  → resultado retorna ao gestor
  → gestor atualiza o Repositório de Lotes do ERP
  → um evento ou agendamento aciona uma nova consulta do adaptador
```

O sentido da seta de consulta deve partir do `Adaptador de Consulta ERP` e
apontar para o repositório do ERP, pois o adaptador inicia a consulta. Essa
consulta não precisa ser contínua: deve ocorrer após evento ou conforme agenda
configurada para a fonte.

O desenho deve mostrar os limites entre mundo físico, ERP, LOG_VENCIMENTOS e
operação humana.

### Decisões

- **Sistema:** classificar criticidade e gerar alerta conforme regras.
- **Gestor:** priorizar ação e direcionar equipe.
- **Operação:** confirmar a condição física e executar a ação.

O gestor pode consultar indicadores e também comunicar diretamente a equipe.

### Regra central

```text
Sistema de origem armazena e informa mudanças.
Camada de integração recebe ou consulta.
LOG_VENCIMENTOS normaliza, monitora e alerta.
Gestor decide.
Operação confere.
Gestor atualiza a fonte oficial.
```

## 2. Fluxo técnico do LOG_VENCIMENTOS

Representa tecnologias, integrações e trocas de dados. Não deve substituir o
fluxo geral.

### Consulta síncrona de produtos

```text
Usuário → listar produtos → Frontend → HTTP GET → Django/DRF
       → consulta → PostgreSQL → dados → Django/DRF
       → HTTP 200 + JSON → Frontend
```

O mesmo padrão serve como base para cadastro e edição, alterando método HTTP,
validação e resposta.

### Integração orientada a eventos

```text
Sistema de origem
  → publica mudança
  → webhook
  → receptor de eventos
  → fila de processamento
  → adaptador da fonte
  → consulta dados completos, quando necessário
  → mapeamento
  → validação e normalização
  → contrato canônico
  → memória operacional
  → monitoramento
  → notificações
```

O evento pode conter apenas o identificador e os dados mínimos da mudança. O
adaptador busca os dados completos na fonte autorizada. O payload definitivo e
as regras de idempotência ainda precisam ser definidos.

### Alternativas quando não há evento

```text
Consulta agendada: scheduler → API ou banco somente leitura → adaptador
Importação: arquivo acordado → importador → adaptador
```

Os três modos convergem para a mesma validação, normalização e monitoração:

1. webhook ou consumo de evento;
2. consulta agendada por API ou banco;
3. importação de arquivo.

A linguagem do sistema de origem não altera esse fluxo. A capacidade de
integração depende da interface disponível e autorizada.

### Integração de dados externos

```text
Fonte externa
  → camada de integração externa
  → conector ou importador
  → mapeamento
  → validação
  → contrato canônico
  → memória operacional
  → monitoramento
```

### Tarefa em segundo plano

```text
Django → RabbitMQ → Celery Worker ↔ PostgreSQL
```

### Tarefa agendada

```text
Celery Beat → RabbitMQ → Celery Worker
```

## 3. Adoção pela empresa

1. Mapear o processo atual de controle de validade.
2. Definir responsáveis por alertas e conferências.
3. Identificar a fonte de dados e obter acesso autorizado.
4. Escolher o modo de integração disponível.
5. Configurar o conector e o mapeamento de campos.
6. Definir critérios e prazos de alerta.
7. Capacitar as pessoas envolvidas.
8. Iniciar o monitoramento e executar conferências preventivas.
9. Registrar resultados e usar indicadores nas decisões.

## 4. Exceções relevantes

- Fonte indisponível: registrar falha e não tratar dados antigos como atuais.
- Evento duplicado: aplicar chave de idempotência e evitar processamento duplo.
- Evento incompleto: consultar a fonte ou colocar o registro em revisão.
- Campo obrigatório ausente: bloquear ou colocar o registro em revisão.
- Data inválida ou ambígua: exigir correção.
- Duplicidade: identificar pela chave acordada com a fonte.
- Localização desatualizada: solicitar confirmação operacional.
- Divergência física: registrar feedback sem sobrescrever silenciosamente a
  fonte principal.
