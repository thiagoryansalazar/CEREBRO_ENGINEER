# Arquitetura - LOG_VENCIMENTOS

## Integração orientada a eventos — 2026-07-01

A arquitetura passa a explicitar uma `Camada de Integração Externa` entre os
sistemas de origem e o núcleo do LOG_VENCIMENTOS.

```text
Sistemas de origem
  ├─ ERP
  ├─ WMS
  ├─ MES
  ├─ LIMS
  ├─ CMMS/EAM
  ├─ QMS
  ├─ DMS/GED
  └─ arquivos e APIs externas
        ↓
Camada de Integração Externa
  ├─ Webhook Receiver
  ├─ API Connector
  ├─ File Importer
  ├─ Database Reader
  ├─ Event Consumer
  └─ Field Mapper
        ↓
Validador e normalizador
        ↓
Modelo canônico LOG_VENCIMENTOS
        ↓
Motor de monitoramento
        ↓
Central de notificações
```

O modo preferencial é orientado a eventos:

```text
Evento no sistema de origem
  → webhook
  → receptor de eventos
  → fila de processamento
  → adaptador da fonte
  → normalizador
  → monitoramento
  → notificações
```

O evento pode transportar apenas o identificador e os dados mínimos da mudança;
o adaptador consulta os dados completos na fonte autorizada. O contrato exato do
evento ainda precisa ser validado.

O adaptador não deve consultar o ERP continuamente. Ele atua após um evento ou,
quando a fonte não oferece eventos, por uma alternativa configurada:

1. webhook ou consumo de evento;
2. consulta agendada por API ou banco somente leitura;
3. importação de arquivo CSV/XLSX ou outro formato acordado.

A integração depende da porta disponível — webhook, API, banco, arquivo ou fila
— e não da linguagem em que o sistema de origem foi implementado. Sistemas em
PHP, Java, Node.js, Elixir, Delphi, .NET ou outras tecnologias podem ser
integrados se expuserem uma interface autorizada e estável.

A representação de 2026-06-30 continua válida como visão conceitual. A revisão
de 2026-07-01 refina como o `Adaptador de Consulta ERP` é acionado e generaliza
a entrada para outras categorias de sistema.

## Arquitetura geral atualizada em 2026-06-30

O desenho geral separa quatro domínios:

1. mundo físico;
2. sistema ERP da empresa;
3. LOG_VENCIMENTOS;
4. operação humana de decisão e conferência.

```text
Fornecedor
  → entrega lote
  → Conferente
  → lote aceito?
      ├─ não → retorna ao fornecedor
      └─ sim → dados do lote → Repositório de Lotes do ERP

LOG_VENCIMENTOS
  └─ Adaptador de Consulta ERP
       ├─ consulta → Repositório de Lotes do ERP
       ├─ envia dados → Monitoramento de Vencimentos
       └─ envia dados → Serviço de Alertas

Serviço de Alertas
  → alerta Gestor

Gestor
  ├─ consulta Monitoramento de Vencimentos
  └─ orienta Repositor
       → realiza conferência física
       → gera resultado
       → informa Gestor
       → Gestor atualiza Repositório de Lotes do ERP

Repositório atualizado
  → nova consulta pelo Adaptador de Consulta ERP
```

### Responsabilidades principais

- **ERP:** armazenar os dados operacionais dos lotes.
- **Adaptador de Consulta ERP:** iniciar o acesso ao repositório do ERP e
  encaminhar os dados necessários ao LOG.
- **Monitoramento de Vencimentos:** analisar prazos, criticidade e indicadores.
- **Serviço de Alertas:** notificar o gestor sobre situações que exigem atenção.
- **Gestor:** consultar indicadores, direcionar a operação e atualizar o ERP.
- **Repositor:** verificar fisicamente os lotes e informar o resultado.

O adaptador representa uma responsabilidade lógica. A forma concreta de acesso
— API, banco somente leitura ou arquivo exportado — continua sendo uma decisão
de integração a ser validada com cada ERP.

## Visão geral vigente

```text
ERP, banco, API ou arquivo exportado
    ↓
Conector específico
    ↓
Mapeador de campos
    ↓
Validador e normalizador
    ↓
Modelo canônico LOG_VENCIMENTOS
    ↓
Monitoramento de vencimentos
    ↓
Central de alertas
    ↓
Gestor e operação física
```

## Fonte de dados e integração

A `Camada de Integração e Normalização` isola o núcleo das diferenças entre
clientes. Sua responsabilidade é:

1. conectar à fonte autorizada;
2. ler os dados sem alterar o sistema de origem;
3. traduzir campos e formatos para o contrato do LOG;
4. validar tipos, obrigatoriedade e consistência;
5. entregar dados normalizados ao monitoramento.

Formas previstas de conexão:

- API do ERP;
- consulta somente leitura a banco autorizado;
- relatório CSV/XLSX exportado;
- planilha controlada para operações sem integração.

Cada fonte usa um conector específico. Depois do conector, o restante do sistema
trabalha com o mesmo modelo.

Na Arquitetura Geral, essa responsabilidade é resumida pelo bloco `Adaptador de
Consulta ERP`. No fluxo técnico, o bloco pode ser detalhado em conector,
mapeador, validador e normalizador.

## Contrato de dados inicial

| Campo | Finalidade |
|---|---|
| `codigo_produto` | identificar o produto na fonte |
| `nome_produto` | exibição e conferência |
| `lote` | identificar o lote |
| `quantidade` | apoiar avaliação e ação |
| `data_validade` | calcular criticidade |
| `local` | orientar a conferência |
| `status` | representar o estado conhecido |

Produto e lote são entidades diferentes: produto é relativamente estável; lote,
quantidade, validade e localização variam.

### Proposta de generalização do contrato

Para permitir outros domínios no futuro, foram sugeridos os campos
`entidade_monitorada`, `tipo_vencimento` e `data_limite`. Essa é uma proposta de
arquitetura, ainda sujeita a validação. Ela não substitui automaticamente o
contrato executável atual baseado em produto, lote e data de validade.

## Base técnica definida nos fluxos

- Frontend: HTML, CSS e JavaScript leve.
- Backend: Python, Django e Django REST Framework.
- Persistência operacional: PostgreSQL.
- Mensageria: RabbitMQ.
- Tarefas: Celery Worker.
- Agendamento: Celery Beat.

O DRF faz parte da aplicação Django; não é um serviço independente.

## Comunicação síncrona

```text
Usuário
  → Frontend
  → HTTP GET
  → Django/DRF
  → consulta PostgreSQL
  ← dados
  ← HTTP 200 + JSON
  ← Frontend
```

O banco devolve dados. O backend aplica regras e serializa a resposta HTTP/JSON.
RabbitMQ e Celery não participam de uma listagem simples.

## Comunicação assíncrona

```text
Django → publica tarefa → RabbitMQ → Celery Worker
Celery Worker ↔ PostgreSQL
Django → HTTP 202 ao cliente, quando aplicável
```

O worker não precisa devolver a tarefa diretamente ao Django. O resultado e o
estado podem ser consultados na persistência apropriada.

## Processamento agendado

```text
Celery Beat → RabbitMQ → Celery Worker → monitoramento/alertas
```

## Memória operacional

O PostgreSQL do LOG não replica o estoque inteiro. Ele guarda configurações,
mapeamentos, sincronizações, projeções necessárias ao monitoramento, alertas,
histórico e feedback operacional.

## Restrições

- A integração deve ser autorizada e preferencialmente somente leitura.
- O núcleo não deve depender do esquema particular de um ERP.
- XLSX arbitrário não é um protocolo estável; precisa de mapeamento.
- Dados externos inválidos não podem avançar silenciosamente.
- IA/OCR, quando existirem, sugerem valores; uma pessoa confirma.
