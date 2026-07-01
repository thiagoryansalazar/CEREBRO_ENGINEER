# Decisões - LOG_VENCIMENTOS

## 2026-07-01 — Backend inicial executável

**Contexto:** a arquitetura técnica já definia Python, Django e Django REST
Framework, mas ainda não existia uma implementação versionada do projeto.

**Decisão:** iniciar o backend no repositório público
`thiagoryansalazar/LOG_VENCIMENTOS`, mantendo transporte HTTP, validação,
entidades de domínio, regras de negócio e futuras integrações em módulos
separados.

**Implementado:**

- `GET /health` para diagnóstico básico;
- `POST /lotes/validar` para validar o contrato inicial e classificar risco;
- sete testes automatizados para rotas, validação e limites de classificação.

**Impacto:** a arquitetura agora possui uma base executável. Essa base ainda não
representa o monitoramento completo, a integração ERP nem a central de alertas.

## 2026-07-01 — Persistência apenas de desenvolvimento

**Decisão:** usar SQLite somente para permitir execução local nesta primeira
iteração, sem criar tabelas de estoque ou transformar o LOG em fonte principal.

**Destino arquitetural mantido:** PostgreSQL para a futura memória operacional.

**Ainda não implementado:** PostgreSQL, RabbitMQ, Celery Worker e Celery Beat.

## 2026-07-01 — Faixas técnicas iniciais de risco

**Decisão técnica inicial:**

```text
VENCIDO = menos de 0 dias
CRITICO = de 0 a 7 dias
ATENCAO = de 8 a 30 dias
NORMAL = acima de 30 dias
```

**Status:** implementada e testada, mas pendente de validação de negócio com uma
empresa real. Uma mudança futura nas faixas deve ser tratada como decisão de
produto, não apenas alteração de código.

## 2026-07-01 — Escopo do contrato executável

O validador inicial exige:

```text
codigo_produto
nome_produto
lote
quantidade
data_validade
local
```

O campo `status`, previsto no contrato canônico da arquitetura, não foi incluído
no primeiro endpoint porque sua origem, semântica e obrigatoriedade ainda não
foram decididas. Isso é uma pendência explícita, não remoção do modelo canônico.

## 2026-06-30 — Artefato atual é a Arquitetura Geral

**Contexto:** o desenho estava sendo tratado como Fluxo Geral de Funcionamento,
mas a versão recriada tem outro objetivo.

**Decisão:** o artefato atual representa a **Arquitetura Geral do
LOG_VENCIMENTOS**. Ele mostra os fatores dos quais o sistema depende, os limites
entre mundo físico, ERP, LOG_VENCIMENTOS e operação humana, além das relações
entre esses blocos.

**Impacto:** as setas indicam dependência, consulta, envio de dados e retorno
operacional. Elas não devem ser interpretadas somente como uma sequência
temporal de telas ou tecnologias.

## 2026-06-30 — Adaptador de Consulta ERP

**Decisão:** usar o nome `Adaptador de Consulta ERP` no lugar de `Atuador PY`.

**Responsabilidade:** o adaptador é o elemento ativo que acessa o banco ou
repositório de lotes mantido pelo ERP e entrega os dados necessários às camadas
do LOG_VENCIMENTOS.

**Direção obrigatória da relação:**

```text
Adaptador de Consulta ERP → consulta dados → Repositório de Lotes do ERP
```

**Motivo:** o nome descreve a responsabilidade arquitetural sem vincular o
componente prematuramente à linguagem Python.

## 2026-06-29 — Fonte de verdade externa

**Contexto:** a hipótese inicial armazenava os lotes no banco principal do
LOG_VENCIMENTOS.

**Decisão:** os sistemas da empresa são a fonte principal de produtos, lotes,
quantidades, validade e localização. O LOG consulta esses dados e não substitui
o ERP.

**Impacto:** cadastro manual, scanner e OCR deixam de ser o fluxo principal.
Continuam possíveis como alternativas para empresas sem fonte estruturada.

## 2026-06-29 — Memória operacional própria

**Decisão:** o LOG pode persistir somente os dados necessários ao seu trabalho:

- última consulta e sincronização;
- lotes sob monitoramento ou uma projeção normalizada;
- estado e histórico dos alertas;
- configurações da empresa;
- mapeamentos entre campos externos e o contrato do LOG;
- resultados de conferências e ações.

**Princípio:** o LOG não é dono do estoque, mas precisa de memória operacional.

## 2026-06-29 — Camada de Integração e Normalização

**Decisão:** toda fonte externa passa por um adaptador, mapeamento de campos e
validação antes do monitoramento.

**Motivo:** ERPs, bancos e arquivos apresentam protocolos, nomes e formatos
diferentes.

## 2026-06-29 — Contrato mínimo de dados

O modelo canônico inicial contém:

```text
codigo_produto
nome_produto
lote
quantidade
data_validade
local
status
```

Cada conector traduz a fonte externa para esse contrato. A semântica, a
obrigatoriedade e a origem do campo `status` ainda precisam ser validadas.

## 2026-06-29 — Separação dos fluxos

- O **Fluxo Geral de Funcionamento do Sistema** representa negócio, pessoas,
  decisões e fronteira do sistema.
- O **Fluxo LOG_VENCIMENTOS** representa componentes técnicos e comunicação
  interna do software.

Misturar os dois reduz a clareza do projeto.

> Atualização de 2026-06-30: o artefato geral em reconstrução passou a ser
> tratado como **Arquitetura Geral**, pois seu objetivo atual é representar
> dependências e responsabilidades, não somente o fluxo de funcionamento.

## 2026-06-29 — Limite do produto

O foco é vencimento. Funcionalidades que aproximem o produto de um ERP completo
devem ser recusadas ou adiadas.

## 2026-06-29 — Processamento síncrono e assíncrono

- Consultas simples usam Django/DRF e PostgreSQL de forma síncrona.
- RabbitMQ e Celery são reservados para tarefas em segundo plano.
- Celery Beat inicia tarefas agendadas por meio da fila.

## 2026-06-29 — Camada física adiada

ESP32 e sinalização física só entram depois que o software, o monitoramento e os
alertas digitais estiverem validados.

Se a camada física avançar, a primeira granularidade será por **gôndola**, não
por prateleira. O objetivo é chamar atenção para uma região, sem exigir
endereçamento de alta precisão.
