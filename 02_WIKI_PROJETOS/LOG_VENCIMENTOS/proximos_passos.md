# Próximos passos - LOG_VENCIMENTOS

## Concluído em 2026-07-01

- [x] Criar o repositório público `thiagoryansalazar/LOG_VENCIMENTOS`.
- [x] Criar a base executável com Python, Django e Django REST Framework.
- [x] Separar rotas, validação, entidade de lote, regras de vencimento e fronteira
      de futuras integrações.
- [x] Implementar `GET /health` e `POST /lotes/validar`.
- [x] Implementar e testar faixas técnicas iniciais de risco.
- [x] Registrar o primeiro ciclo PDCA e executar sete testes automatizados.
- [x] Registrar a arquitetura orientada a eventos e suas alternativas de
      integração na Wiki.

## Prioridade alta

- [ ] Definir o contrato canônico do evento: identificador, dados mínimos,
      versão, origem, data e chave de idempotência.
- [ ] Definir autenticação, autorização, repetição, replay e tratamento de evento
      duplicado ou fora de ordem.
- [ ] Escolher a primeira categoria de sistema e o primeiro modo real de
      integração: evento, consulta agendada ou arquivo.
- [ ] Atualizar o diagrama técnico com receptor de eventos, fila e Camada de
      Integração Externa.
- [ ] Validar `entidade_monitorada`, `tipo_vencimento` e `data_limite` antes de
      qualquer alteração no contrato executável.
- [ ] Validar com uma empresa real qual é a fonte de verdade dos lotes.
- [ ] Escolher o primeiro caminho de integração: API, banco somente leitura ou
      CSV/XLSX exportado.
- [ ] Definir obrigatoriedade, tipos, chaves e semântica do contrato canônico.
- [ ] Decidir se `status` entra no contrato executável, de qual fonte vem e quem
      pode alterá-lo.
- [ ] Decidir a estratégia da memória operacional: projeção, cache, frequência
      de sincronização e retenção.
- [ ] Definir como divergências físicas retornam ao fluxo sem corromper a fonte.
- [x] Atualizar a Arquitetura Geral com ERP, Repositório de Lotes e Adaptador de
      Consulta ERP.
- [x] Atualizar a documentação técnica detalhando eventos, conectores,
      mapeamento, validação e normalização.
- [ ] Confirmar com o primeiro sistema de origem qual porta autorizada será
      usada.

## Prioridade média

- [x] Implementar regras e faixas técnicas iniciais de criticidade.
- [ ] Validar as faixas de criticidade com usuários e regras reais de negócio.
- [ ] Modelar estados do alerta e da conferência.
- [ ] Definir requisitos de segurança, credenciais, auditoria e isolamento por
      empresa.
- [ ] Criar critérios para falha, atraso e recuperação de sincronização.
- [ ] Definir métricas de produto e operação.
- [ ] Transformar requisitos validados em backlog priorizado.
- [ ] Substituir SQLite por PostgreSQL quando a memória operacional for
      modelada.
- [ ] Introduzir RabbitMQ e Celery somente quando existir uma tarefa assíncrona
      concreta.

## Futuro

- [ ] Validar um segundo domínio antes de generalizar o produto para outros
      setores.
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
