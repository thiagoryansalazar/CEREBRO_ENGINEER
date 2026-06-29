# Decisões - LOG_VENCIMENTOS

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
