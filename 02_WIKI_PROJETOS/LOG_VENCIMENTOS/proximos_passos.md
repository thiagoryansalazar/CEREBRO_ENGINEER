# Próximos passos - LOG_VENCIMENTOS

## Concluído em 2026-07-01

- [x] Criar o repositório público `thiagoryansalazar/LOG_VENCIMENTOS`.
- [x] Criar a base executável com Python, Django e Django REST Framework.
- [x] Separar rotas, validação, entidade de lote, regras de vencimento e fronteira
      de futuras integrações.
- [x] Implementar `GET /health` e `POST /lotes/validar`.
- [x] Implementar e testar faixas técnicas iniciais de risco.
- [x] Registrar o primeiro ciclo PDCA e executar sete testes automatizados.

## Prioridade alta

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
- [ ] Atualizar o diagrama técnico detalhando conector, mapeamento, validação e
      normalização.
- [ ] Confirmar com o primeiro ERP se o adaptador usará API, banco somente
      leitura ou exportação de arquivo.

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
