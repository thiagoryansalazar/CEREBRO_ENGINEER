# CEREBRO_ENGINEER_WIKI

## O que é

CEREBRO_ENGINEER_WIKI é uma Wiki de contexto, estudo, memória e projetos.

Ela existe para transformar conversas, estudos, decisões e erros em conhecimento organizado e reutilizável.

## Por que existe

Durante o desenvolvimento de projetos, muitas decisões importantes ficam presas em chats. Quando o chat termina, o contexto se perde.

Esta Wiki resolve esse problema registrando:

- contexto;
- decisões;
- arquitetura;
- erros e soluções;
- referências;
- dúvidas;
- procedimentos;
- próximos passos;
- aprendizados.

## O que a Wiki faz

A Wiki funciona como memória de longo prazo:

1. o ChatGPT ajuda a construir raciocínio;
2. as informações importantes são enviadas ao GitHub;
3. a Wiki organiza o contexto;
4. Codex e Claude consultam a Wiki;
5. os projetos são desenvolvidos com base nas decisões já tomadas.

## Conteúdos que devem entrar

- conteúdo de estudo e de projetos;
- erros e soluções;
- decisões;
- referências externas;
- procedimentos;
- dúvidas abertas;
- sugestões de agentes;
- próximos passos.

Não devem entrar sem tratamento:

- transcrições brutas sem síntese;
- ideias confusas sem classificação;
- conteúdo duplicado;
- decisão sem contexto;
- link externo sem resumo.

## Como enviar informações dos chats

Use o comando:

> Envie esta informação para o @GitHub no repositório CEREBRO_ENGINEER_WIKI, seguindo o README.md, o TREE_DECISION.md e atualizando o SUMMARY.md se criar novo arquivo.

O agente deve:

1. identificar o tipo de informação;
2. consultar o `TREE_DECISION.md`;
3. escolher o arquivo correto;
4. escrever em Markdown;
5. atualizar o `SUMMARY.md` se criar novo arquivo;
6. atualizar o `LOG.md` em alteração relevante;
7. não salvar informação solta sem classificação.

## Como Codex e Claude devem usar

Antes de executar tarefas de projeto, consultar:

1. `README.md`;
2. `AGENTS.md` ou `CLAUDE.md`;
3. `TREE_DECISION.md`;
4. `SUMMARY.md`;
5. `INDEX.md`;
6. arquivos específicos do projeto.

Para projetos, consultar primeiro `contexto_geral.md`, `decisoes.md`, `arquitetura.md`, `erros_e_solucoes.md` e `proximos_passos.md`.

## Como manter organizada

Markdown é a fonte da verdade. Toda informação precisa de categoria, contexto e finalidade. Novas páginas entram no `SUMMARY.md`; mudanças relevantes entram no `LOG.md`.

## Regra principal

A Wiki não é depósito. A Wiki é memória organizada.

Toda informação deve responder pelo menos uma pergunta:

1. O que isso explica?
2. Que decisão isso registra?
3. Que erro isso evita?
4. Que projeto isso melhora?
5. Que estudo isso consolida?
6. Que ação isso orienta?
