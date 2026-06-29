# AGENTS.md - CEREBRO_ENGINEER_WIKI

## Papel do agente

Este repositório é uma Wiki de contexto, estudo, memória e projetos. O agente deve atuar como curador da memória e manter a Wiki útil, navegável e confiável.

## Ordem de leitura

1. `README.md`
2. `TREE_DECISION.md`
3. `SUMMARY.md`
4. `INDEX.md`
5. arquivo específico relacionado ao tema

## Regras principais

1. Markdown é a fonte da verdade.
2. Não salvar informação sem classificação.
3. Não misturar estudo pessoal com projeto.
4. Não tratar hipótese como decisão.
5. Não tratar chat como verdade final.
6. Diferenciar fato, hipótese, decisão, sugestão, erro e dúvida.
7. Se criar um novo arquivo, atualizar `SUMMARY.md`.
8. Se fizer alteração relevante, atualizar `LOG.md`.
9. Se encontrar inconsistência, registrar em `sugestoes.md`.
10. Se identificar erro superado, registrar em `erros_e_solucoes.md`.
11. Não apagar conteúdo antigo sem justificativa.
12. Não duplicar conteúdo existente.
13. Se não souber onde salvar, usar `99_INDEFINIDOS/` e registrar sugestão de classificação.

## Como classificar informação

Use `TREE_DECISION.md`.

## Decisões

Salvar em `07_PROJETOS/<PROJETO>/decisoes.md`, contendo contexto, decisão, justificativa, impacto e data.

## Erros e soluções

Salvar em `07_PROJETOS/<PROJETO>/erros_e_solucoes.md`, contendo erro, motivo do bloqueio, solução, aprendizado e prevenção.

## Sugestões

Salvar em `07_PROJETOS/<PROJETO>/sugestoes.md`. Não aplicar automaticamente sugestões que alterem decisões ou arquitetura.

## Referências

Salvar em `08_REFERENCIAS/`, contendo título, link, resumo, ideias principais, aplicação nos projetos e tags.

## Relação com Codex

Antes de implementar, consultar a Wiki. Para `LOG_VENCIMENTOS` e `ALI_CONSULTORA`, ler `contexto_geral.md`, `decisoes.md`, `arquitetura.md`, `erros_e_solucoes.md` e `proximos_passos.md`.

## Restrições

- Não criar banco de dados, servidor ou MCP agora.
- Não implementar infraestrutura complexa ou autoaperfeiçoamento.
- Manter tudo em Markdown.
- Priorizar síntese útil.
