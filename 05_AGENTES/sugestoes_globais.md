# Sugestões globais

## Auxiliares de construção do LOG_VENCIMENTOS

Estes itens são chatbots auxiliares usados na construção teórica do projeto.
Eles ajudam a pensar, revisar, organizar e validar partes específicas, mas não
são agentes.

Os identificadores e as etiquetas de origem estão em
[`id_auxiliares.yaml`](id_auxiliares.yaml).

Um auxiliar pode futuramente ser transformado em agente, mas isso exige uma
decisão explícita, definição de responsabilidades, regras de atuação e limites.

### AI ARCHITECT

- **ID do auxiliar:** `aux_log_vencimentos_ai_architect`
- **Atuação assumida no chat:** Arquiteto de Software e AI Architect.
- **Como se comporta:** trabalha em construção guiada: pensar, isolar o
  problema, decidir a próxima peça, validar com o usuário e avançar. Analisa
  responsabilidades, integrações, dados e riscos antes de escolher tecnologia.
  A IA aparece como acelerador depois que entrada, saída, contexto e validação
  estão definidos.
- **Por que é útil:** impede que o projeto pule diretamente para ferramentas ou
  IA sem compreender o fluxo e a origem dos dados.
- **Como agregou ao projeto:** ajudou a separar fonte externa, integração,
  normalização e monitoramento; identificou a necessidade de um contrato de
  dados e de memória operacional sem transformar o LOG em dono do estoque.
- **Status:** auxiliar documentado; não é agente.

### Engenheiro de Produção

- **ID do auxiliar:** `aux_log_vencimentos_engenheiro_producao`
- **Atuação assumida no chat:** Engenheiro de Produção do LOG_VENCIMENTOS.
- **Como se comporta:** aplica visão sistêmica, operacional e de chão de
  operação. Mapeia o processo físico, identifica quem toca no lote, separa mundo
  físico e digital, procura o ponto natural de captura e evita escolher
  tecnologia antes de compreender a operação.
- **Por que é útil:** verifica se uma proposta cabe na rotina real sem criar
  custo, retrabalho ou dependência manual excessiva.
- **Como agregou ao projeto:** reposicionou o gargalo como problema operacional
  de captura e confiabilidade dos dados; reforçou que o sistema deve se encaixar
  no processo existente da empresa.
- **Status:** auxiliar documentado; não é agente.

### ESP32 - HARDWARE

- **ID do auxiliar:** `aux_log_vencimentos_esp32_hardware`
- **Atuação observada no chat:** exploração e prototipagem da camada física/IoT.
- **Como se comporta:** avalia o lugar do ESP32 na solução, reduz o protótipo ao
  menor teste útil, compara comunicação por consulta e por eventos e explicita
  dependências de localização física.
- **Por que é útil:** evita comprar componentes ou sofisticar a automação antes
  de provar a comunicação entre software e dispositivo.
- **Como agregou ao projeto:** definiu o ESP32 como cliente de alertas, não como
  entrada principal de lotes; propôs laboratório inicial pelo Serial Monitor e
  identificou a gôndola como granularidade futura mais simples que a prateleira.
- **Status:** auxiliar documentado; não é agente.

### FLUXO_LOG_VENCIMENTOS

- **ID do auxiliar:** `aux_log_vencimentos_fluxo_tecnico`
- **Atuação observada no chat:** revisão arquitetural do fluxo técnico.
- **Como se comporta:** avalia diagramas por partes, confere responsabilidades
  entre camadas e valida cada correção antes de avançar. Distingue caminho
  síncrono, processamento assíncrono e tarefas agendadas.
- **Por que é útil:** transforma componentes tecnológicos em um fluxo legível e
  tecnicamente coerente.
- **Como agregou ao projeto:** consolidou Django e DRF no mesmo backend,
  posicionou RabbitMQ, Celery Worker e Celery Beat, separou retorno do banco de
  resposta HTTP/JSON e corrigiu ligações indevidas entre componentes.
- **Status:** auxiliar documentado; não é agente.

### PRODUCT OWNER

- **ID do auxiliar:** `aux_log_vencimentos_product_owner`
- **Atuação assumida no chat:** dono do produto do LOG_VENCIMENTOS.
- **Como se comporta:** executa o ciclo leitura, avaliação, feedback, validação,
  sugestão, encaixe no backlog e comentário final. Examina valor, clareza,
  coerência, risco de escopo, prioridade e aderência à operação física.
- **Por que é útil:** protege o foco do produto e decide se uma ideia pertence ao
  presente, ao backlog ou à visão futura.
- **Como agregou ao projeto:** reforçou que o LOG resolve vencimentos, não todo o
  estoque, e passou a avaliar melhorias pelo valor entregue a gestores,
  conferentes e repositores.
- **Status:** auxiliar documentado; não é agente.

### CONTEXTO_GERAL

- **ID do auxiliar:** `aux_log_vencimentos_contexto_geral`
- **Atuação observada no chat:** curadoria do contexto e da narrativa central do
  projeto.
- **Como se comporta:** revisa definições, reduz textos quando solicitado e
  mantém separadas a visão de negócio e a visão tecnológica.
- **Por que é útil:** oferece uma fonte de contexto coerente para que novos
  artefatos não contradigam a proposta do produto.
- **Como agregou ao projeto:** consolidou visão geral, público, problema,
  hipótese, objetivos, solução, ciclo operacional e distinção entre Fluxo Geral
  e Fluxo LOG_VENCIMENTOS.
- **Status:** auxiliar documentado; não é agente.

### TERMO DE ABERTURA

- **ID do auxiliar:** `aux_log_vencimentos_termo_abertura`
- **Atuação observada no chat:** organização e revisão do documento de abertura.
- **Como se comporta:** estrutura tópicos em ordem de leitura, adapta o nível de
  detalhe ao caráter conceitual do documento e incorpora novos artefatos sem
  duplicar sua explicação.
- **Por que é útil:** mantém o documento compreensível para quem conhece o
  projeto pela primeira vez.
- **Como agregou ao projeto:** organizou público, problema, hipótese, objetivos,
  solução, figura do fluxo geral e adoção pela empresa em uma narrativa
  consistente.
- **Status:** auxiliar documentado; não é agente.

### FLUXO GERAL DE FUNCIONAMENTO DO SISTEMA

- **ID do auxiliar:** `aux_log_vencimentos_fluxo_geral`
- **Atuação observada no chat:** revisão e modelagem do fluxo conceitual,
  operacional, informacional e decisório.
- **Como se comporta:** avalia diagramas iterativamente, verifica clareza para
  terceiros, separa ações humanas das ações internas do sistema e revisa
  entidades, processos, decisões, conexões, cores, legenda e limite do sistema.
- **Por que é útil:** garante que o funcionamento de ponta a ponta seja
  compreensível sem depender da arquitetura tecnológica.
- **Como agregou ao projeto:** tornou explícitos os dois caminhos do gestor, o
  retorno da conferência física, a diferença entre decisão humana e automatizada
  e o `Limite do Sistema`; também consolidou o nome do artefato.
- **Observação de origem:** o chat contém conteúdo legado de outro projeto; para
  este registro foi considerada somente a parte relacionada ao LOG_VENCIMENTOS.
- **Status:** auxiliar documentado; não é agente.

## Regra de uso

Ao reutilizar qualquer um desses auxiliares:

1. informar o ID do auxiliar;
2. informar o projeto em que está atuando;
3. manter sugestões separadas de decisões;
4. registrar a origem da contribuição;
5. não tratá-lo como agente;
6. formalizar separadamente caso seja transformado em agente.
