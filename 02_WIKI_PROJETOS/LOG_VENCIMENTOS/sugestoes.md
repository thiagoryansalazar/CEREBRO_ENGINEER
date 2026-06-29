# Sugestões - LOG_VENCIMENTOS

Estas ideias não são compromisso de implementação.

## Integração

- Criar catálogo de conectores por ERP ou tipo de fonte.
- Permitir mapeamento assistido de colunas CSV/XLSX.
- Versionar contrato de dados e mapeamentos.
- Oferecer diagnóstico de qualidade antes de ativar o monitoramento.

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
