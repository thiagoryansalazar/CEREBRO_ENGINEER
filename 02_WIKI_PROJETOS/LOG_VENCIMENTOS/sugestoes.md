# Sugestões - LOG_VENCIMENTOS

Estas ideias não são compromisso de implementação.

## Integração externa

- Criar interfaces e mocks para conectores antes de integrar fornecedores reais.
- Organizar o catálogo de conectores por categoria de sistema: ERP, WMS, MES,
  LIMS, CMMS/EAM, QMS, DMS/GED, arquivos e APIs externas.
- Considerar endpoints como `/integrations/webhook`, `/integrations/import` e
  `/integrations/test-connection` somente após definir autenticação e contrato.
- Validar se o evento carrega apenas identificador e dados mínimos ou o registro
  completo.
- Criar catálogo de conectores por ERP ou tipo de fonte.
- Permitir mapeamento assistido de colunas CSV/XLSX.
- Versionar contrato de dados e mapeamentos.
- Oferecer diagnóstico de qualidade antes de ativar o monitoramento.

## Contrato genérico futuro

- Avaliar `entidade_monitorada`, `tipo_vencimento` e `data_limite` como campos
  comuns para outros domínios.
- Manter tradução explícita entre esse modelo e o contrato atual de produto,
  lote e validade.
- Não alterar o contrato executável até validar casos reais fora do setor
  alimentício.

## Captura assistida

- Scanner para localizar produto, sem presumir que código de barras contenha
  lote e validade.
- Foto de etiqueta com OCR/IA e confirmação humana.
- Cadastro manual assistido como contingência, não como fluxo principal.

## Inteligência e análise

- previsão de perdas;
- sugestão de promoção, remanejamento ou destinação;
- análise de recorrência por produto, fornecedor ou unidade;
- indicadores de aderência às conferências.

## IoT futuro

- ESP32 como cliente IoT e interface física de alerta, nunca como entrada
  principal do lote.
- Primeiro laboratório sem LED: API simulada → Wi-Fi → ESP32 → Serial Monitor.
- Primeiro modelo de comunicação: consulta periódica à API.
- Evolução possível: eventos por MQTT.
- Sinalização por gôndola com poucos estados de criticidade.

## Regra de avaliação

Antes de mover uma sugestão para decisões ou backlog, validar valor operacional,
custo, dependências, risco de escopo e evidência de necessidade.
