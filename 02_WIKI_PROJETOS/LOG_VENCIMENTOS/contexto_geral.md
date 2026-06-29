# Contexto geral - LOG_VENCIMENTOS

## Definição

O LOG_VENCIMENTOS é um sistema especializado em consultar dados de lotes já
registrados pelas empresas, monitorar prazos de validade, detectar riscos e
orientar ações preventivas.

Ele não é um ERP, não substitui o sistema de estoque e não deve ser o dono
principal dos dados de produtos e lotes.

## Público-alvo

Empresas do setor alimentício que armazenam, distribuem ou comercializam
produtos com prazo de validade:

- supermercados e atacadistas;
- distribuidoras e centros de distribuição;
- varejistas e redes alimentícias.

Essas operações trabalham com muitos produtos perecíveis, múltiplos lotes e
conferências periódicas. Precisam de visibilidade antecipada sem adotar um
sistema operacional excessivamente complexo.

## Problema

A falta de acompanhamento sistemático dificulta a identificação antecipada de
produtos em risco de vencimento. Isso aumenta perdas financeiras, desperdício,
ações emergenciais e o risco de produtos vencidos chegarem ao consumidor.

## Hipótese

Um monitor dedicado, conectado às fontes de dados existentes e combinado com
alertas e conferência humana, pode reduzir perdas e melhorar a tomada de
decisão.

## Objetivos

- Consultar e normalizar informações de produtos e lotes.
- Monitorar continuamente datas de validade.
- Detectar lotes que exigem atenção.
- Alertar gestores com antecedência.
- Direcionar conferências físicas.
- Registrar o resultado das ações e recalcular o risco.
- Apoiar promoção, remanejamento, bloqueio, destinação ou descarte.
- Produzir indicadores para decisões operacionais e gerenciais.

## Ciclo operacional

`detectar risco → alertar gestor → direcionar conferência → verificar
fisicamente → registrar resultado → atualizar estado → recalcular risco`

O sistema interpreta dados e gera alertas, mas a situação física do produto
continua dependendo da confirmação humana.

## Escopo atual

- integração com fontes externas;
- normalização de dados;
- monitoramento de vencimentos;
- alertas digitais;
- apoio à conferência e à decisão;
- memória operacional e histórico.

## Fora do escopo atual

- substituir o ERP ou controlar todo o estoque;
- automação física com ESP32 e LEDs;
- RFID, sensores ou endereçamento detalhado por prateleira;
- IA/OCR sem validação humana.
