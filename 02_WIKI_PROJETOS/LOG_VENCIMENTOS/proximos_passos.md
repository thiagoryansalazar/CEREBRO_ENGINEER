# Próximos passos - LOG_VENCIMENTOS

## Prioridade alta

- [ ] Validar com uma empresa real qual é a fonte de verdade dos lotes.
- [ ] Escolher o primeiro caminho de integração: API, banco somente leitura ou
      CSV/XLSX exportado.
- [ ] Definir obrigatoriedade, tipos, chaves e semântica do contrato canônico.
- [ ] Decidir a estratégia da memória operacional: projeção, cache, frequência
      de sincronização e retenção.
- [ ] Definir como divergências físicas retornam ao fluxo sem corromper a fonte.
- [ ] Atualizar os diagramas geral e técnico com a fonte externa e a camada de
      integração.

## Prioridade média

- [ ] Definir regras e faixas de criticidade.
- [ ] Modelar estados do alerta e da conferência.
- [ ] Definir requisitos de segurança, credenciais, auditoria e isolamento por
      empresa.
- [ ] Criar critérios para falha, atraso e recuperação de sincronização.
- [ ] Definir métricas de produto e operação.
- [ ] Transformar requisitos validados em backlog priorizado.

## Futuro

- [ ] Avaliar scanner e OCR/IA para fontes sem dados estruturados.
- [ ] Executar laboratório de comunicação com ESP32 somente após os alertas
      digitais funcionarem.
- [ ] Se o IoT for aprovado, validar endereçamento por gôndola antes de comprar
      componentes de sinalização.

## Responsáveis a definir

- decisão de produto: Product Owner;
- contrato e integração: arquitetura/backend;
- validação do processo: operação da empresa;
- segurança e acesso: responsável técnico da empresa.
