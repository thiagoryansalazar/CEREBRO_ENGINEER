# Fluxos - LOG_VENCIMENTOS

## 1. Fluxo geral de funcionamento

Representa o processo de negócio e a interação entre sistema e pessoas:

```text
Empresa registra o lote em seu sistema
  → LOG consulta a fonte autorizada
  → integração normaliza e valida
  → monitoramento calcula o risco
  → central notifica o gestor
  → gestor analisa indicadores e direciona a conferência
  → conferente/repositor verifica o produto
  → resultado e ação são registrados
  → monitoramento recalcula o estado
```

Esse desenho deve mostrar o `Limite do Sistema`, os participantes externos e
quais decisões são do sistema ou de uma pessoa.

### Decisões

- **Sistema:** classificar criticidade e gerar alerta conforme regras.
- **Gestor:** priorizar ação e direcionar equipe.
- **Operação:** confirmar a condição física e executar a ação.

O gestor pode consultar indicadores e também comunicar diretamente a equipe.

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

### Integração de dados externos

```text
Fonte externa
  → conector
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
4. Configurar o conector e o mapeamento de campos.
5. Definir critérios e prazos de alerta.
6. Capacitar as pessoas envolvidas.
7. Iniciar o monitoramento e executar conferências preventivas.
8. Registrar resultados e usar indicadores nas decisões.

## 4. Exceções relevantes

- Fonte indisponível: registrar falha e não tratar dados antigos como atuais.
- Campo obrigatório ausente: bloquear ou colocar o registro em revisão.
- Data inválida ou ambígua: exigir correção.
- Duplicidade: identificar pela chave acordada com a fonte.
- Localização desatualizada: solicitar confirmação operacional.
- Divergência física: registrar feedback sem sobrescrever silenciosamente a
  fonte principal.
