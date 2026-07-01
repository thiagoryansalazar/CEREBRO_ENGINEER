# Arquitetura - LOG_VENCIMENTOS

## Estado de implementação em 2026-07-01

O primeiro backend executável foi publicado no repositório público
[`thiagoryansalazar/LOG_VENCIMENTOS`](https://github.com/thiagoryansalazar/LOG_VENCIMENTOS),
commit inicial `13a533c`.

A implementação atual confirma a escolha de Python, Django e Django REST
Framework e separa as responsabilidades internas desta forma:

```text
Cliente HTTP
  → src/routes
  → src/validators
  → src/models
  → src/services
  → resposta HTTP/JSON

src/integrations
  → reservado para conectores futuros
```

### Componentes implementados

- `config/`: configuração Django, URLs e ponto WSGI.
- `src/routes/`: transporte HTTP e composição das respostas.
- `src/validators/`: validação e normalização do lote recebido.
- `src/models/`: entidade de domínio `Lote`, sem persistência de estoque.
- `src/services/`: cálculo de dias restantes e classificação de risco.
- `src/integrations/`: fronteira criada, ainda sem conector real.

Rotas disponíveis:

```text
GET  /health
POST /lotes/validar
```

A classificação técnica inicial é:

| Dias restantes | Classificação |
|---|---|
| menor que 0 | `VENCIDO` |
| de 0 a 7 | `CRITICO` |
| de 8 a 30 | `ATENCAO` |
| acima de 30 | `NORMAL` |

Essas faixas estão implementadas e testadas, mas ainda precisam de validação de
negócio com uma empresa real.

### Limites da implementação atual

- SQLite é usado somente no ambiente inicial de desenvolvimento.
- PostgreSQL continua sendo o destino previsto para memória operacional.
- RabbitMQ, Celery Worker e Celery Beat ainda não foram implementados.
- Não existe integração real com ERP, banco externo ou CSV/XLSX.
- Não existe frontend nem autenticação avançada.
- O contrato executável atual exige `codigo_produto`, `nome_produto`, `lote`,
  `quantidade`, `data_validade` e `local`.
- O campo canônico `status` ainda não faz parte da validação executável; sua
  semântica, origem e obrigatoriedade continuam pendentes.

O backend inicial possui sete testes automatizados cobrindo validação, rotas,
faixas de risco e seus limites. Esta seção descreve o que existe no código; as
seções seguintes preservam a arquitetura-alvo e as integrações planejadas.

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
