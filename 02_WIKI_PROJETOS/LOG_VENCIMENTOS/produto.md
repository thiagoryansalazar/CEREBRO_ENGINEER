# Produto - LOG_VENCIMENTOS

## Proposta

Adicionar uma camada preventiva sobre os dados operacionais que a empresa já
possui, transformando lotes e datas de validade em risco visível e ação
orientada.

## Usuários

- **Gestor:** acompanha indicadores, recebe alertas e decide prioridades.
- **Conferente:** valida entrada ou situação física dos lotes.
- **Repositor/equipe operacional:** localiza o risco e executa a ação.
- **Responsável pela integração:** autoriza a fonte e mantém o mapeamento.

## Valor entregue

- antecipação de perdas por vencimento;
- menor dependência de conferências sem prioridade;
- visão centralizada de riscos;
- alertas acionáveis para gestores;
- rastreabilidade das conferências e decisões;
- adoção com menor mudança na operação existente.

## Requisitos essenciais

- conectar-se a uma fonte de dados autorizada;
- admitir evento, consulta agendada ou arquivo conforme a porta disponível;
- normalizar diferentes formatos;
- validar lote e data de validade;
- configurar regras e janelas de alerta;
- monitorar continuamente;
- notificar responsáveis;
- registrar conferência, decisão e ação;
- exibir indicadores;
- manter histórico e trilha operacional.

## Escopo atual e visão futura

O produto atual atende o setor alimentício e monitora produtos, lotes e datas de
validade. Essa especialização deve ser preservada durante a validação do MVP.

A visão futura é transformar o núcleo em um monitor de vencimentos, prazos,
conformidade e risco aplicável também à construção civil, indústria química,
indústria em geral, saúde e qualidade. Essa evolução depende de evidência de
produto e da validação de um contrato de dados mais genérico.

## Critérios de produto

Cada melhoria deve responder:

1. Resolve uma dor de vencimento?
2. Gera uma ação clara para gestor ou operação?
3. Respeita o fluxo físico da empresa?
4. Cabe no produto atual ou é evolução futura?
5. Cria risco de transformar o LOG em ERP?

## Diretriz de backlog

- **Agora:** integração, contrato de dados, monitoramento, alertas e feedback.
- **Depois:** conectores adicionais e captura assistida para fontes precárias.
- **Futuro:** generalização multissetorial validada, OCR/IA, scanner integrado,
  IoT e sinalização física.

## Indicadores a definir

- lotes monitorados e com dados válidos;
- produtos por faixa de criticidade;
- alertas reconhecidos e pendentes;
- tempo entre alerta e conferência;
- ações tomadas;
- perdas evitadas ou reduzidas;
- falhas de sincronização e qualidade de dados.
