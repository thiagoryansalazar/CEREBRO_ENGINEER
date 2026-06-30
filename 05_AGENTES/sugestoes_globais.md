# Sugestões globais

## Agentes e chats especializados do LOG_VENCIMENTOS

Este registro transforma papéis úteis observados no projeto em referências para
outros projetos da Wiki. Ele não transforma automaticamente as respostas desses
chats em decisões.

Os identificadores e as etiquetas de origem estão em
[`id_agentes.yaml`](id_agentes.yaml).

### AI ARCHITECT

- **ID:** `log_vencimentos_ai_architect`
- **Papel declarado no chat:** Arquiteto de Software e AI Architect.
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
- **Status:** papel documentado; reutilização depende do contexto do projeto.

### Engenheiro de Produção

- **ID:** `log_vencimentos_engenheiro_producao`
- **Papel declarado no chat:** Engenheiro de Produção do LOG_VENCIMENTOS.
- **Como se comporta:** aplica visão sistêmica, operacional e de chão de
  operação. Mapeia o processo físico, identifica quem toca no lote, separa mundo
  físico e digital, procura o ponto natural de captura e evita escolher
  tecnologia antes de compreender a operação.
- **Por que é útil:** verifica se uma proposta cabe na rotina real sem criar
  custo, retrabalho ou dependência manual excessiva.
- **Como agregou ao projeto:** reposicionou o gargalo como problema operacional
  de captura e confiabilidade dos dados; reforçou que o sistema deve se encaixar
  no processo existente da empresa.
- **Status:** papel documentado; reutilização depende do contexto do projeto.

### ESP32 - HARDWARE

- **ID:** `log_vencimentos_esp32_hardware`
- **Papel observado no chat:** especialista de exploração e prototipagem da
  camada física/IoT. O chat não contém uma definição formal de agente equivalente
  às três personas declaradas.
- **Como se comporta:** avalia o lugar do ESP32 na solução, reduz o protótipo ao
  menor teste útil, compara comunicação por consulta e por eventos e explicita
  dependências de localização física.
- **Por que é útil:** evita comprar componentes ou sofisticar a automação antes
  de provar a comunicação entre software e dispositivo.
- **Como agregou ao projeto:** definiu o ESP32 como cliente de alertas, não como
  entrada principal de lotes; propôs laboratório inicial pelo Serial Monitor e
  identificou a gôndola como granularidade futura mais simples que a prateleira.
- **Status:** comportamento observado; papel formal ainda não declarado.

### FLUXO_LOG_VENCIMENTOS

- **ID:** `log_vencimentos_fluxo_tecnico`
- **Papel observado no chat:** revisor arquitetural do fluxo técnico.
- **Como se comporta:** avalia diagramas por partes, confere responsabilidades
  entre camadas e valida cada correção antes de avançar. Distingue caminho
  síncrono, processamento assíncrono e tarefas agendadas.
- **Por que é útil:** transforma componentes tecnológicos em um fluxo legível e
  tecnicamente coerente.
- **Como agregou ao projeto:** consolidou Django e DRF no mesmo backend,
  posicionou RabbitMQ, Celery Worker e Celery Beat, separou retorno do banco de
  resposta HTTP/JSON e corrigiu ligações indevidas entre componentes.
- **Status:** comportamento observado; papel formal ainda não declarado.

### PRODUCT OWNER

- **ID:** `log_vencimentos_product_owner`
- **Papel declarado no chat:** dono do produto do LOG_VENCIMENTOS.
- **Como se comporta:** executa o ciclo leitura, avaliação, feedback, validação,
  sugestão, encaixe no backlog e comentário final. Examina valor, clareza,
  coerência, risco de escopo, prioridade e aderência à operação física.
- **Por que é útil:** protege o foco do produto e decide se uma ideia pertence ao
  presente, ao backlog ou à visão futura.
- **Como agregou ao projeto:** reforçou que o LOG resolve vencimentos, não todo o
  estoque, e passou a avaliar melhorias pelo valor entregue a gestores,
  conferentes e repositores.
- **Status:** papel documentado; reutilização depende do contexto do projeto.

### CONTEXTO_GERAL

- **ID:** `log_vencimentos_contexto_geral`
- **Papel observado no chat:** curador do contexto e da narrativa central do
  projeto.
- **Como se comporta:** revisa definições, reduz textos quando solicitado e
  mantém separadas a visão de negócio e a visão tecnológica.
- **Por que é útil:** oferece uma fonte de contexto coerente para que novos
  artefatos não contradigam a proposta do produto.
- **Como agregou ao projeto:** consolidou visão geral, público, problema,
  hipótese, objetivos, solução, ciclo operacional e distinção entre Fluxo Geral
  e Fluxo LOG_VENCIMENTOS.
- **Status:** comportamento observado; papel formal ainda não declarado.

### TERMO DE ABERTURA

- **ID:** `log_vencimentos_termo_abertura`
- **Papel observado no chat:** organizador e revisor do documento de abertura.
- **Como se comporta:** estrutura tópicos em ordem de leitura, adapta o nível de
  detalhe ao caráter conceitual do documento e incorpora novos artefatos sem
  duplicar sua explicação.
- **Por que é útil:** mantém o documento compreensível para quem conhece o
  projeto pela primeira vez.
- **Como agregou ao projeto:** organizou público, problema, hipótese, objetivos,
  solução, figura do fluxo geral e adoção pela empresa em uma narrativa
  consistente.
- **Status:** comportamento observado; papel formal ainda não declarado.

### FLUXO GERAL DE FUNCIONAMENTO DO SISTEMA

- **ID:** `log_vencimentos_fluxo_geral`
- **Papel observado no chat:** revisor e modelador do fluxo conceitual,
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
- **Status:** comportamento observado; papel formal ainda não declarado.

## Regra de uso

Ao reutilizar qualquer um desses papéis:

1. informar o ID do agente;
2. informar o projeto em que está atuando;
3. manter sugestões separadas de decisões;
4. registrar a origem da contribuição;
5. não presumir autoridade fora do papel documentado.
