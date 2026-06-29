# Arquitetura - LOG_VENCIMENTOS

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
