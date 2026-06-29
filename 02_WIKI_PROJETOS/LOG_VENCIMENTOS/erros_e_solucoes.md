# Erros e soluções - LOG_VENCIMENTOS

## Tratar o LOG como banco principal do estoque

- **Problema:** duplica o trabalho que o ERP já executa.
- **Solução:** consultar a fonte existente e guardar somente memória operacional.
- **Prevenção:** representar a fonte externa antes da camada de integração.

## Esperar que qualquer XLSX tenha o mesmo formato

- **Problema:** nomes, tipos e estrutura variam por empresa.
- **Solução:** conector e mapeamento por fonte, convertendo para contrato canônico.
- **Prevenção:** validar arquivo e versão do mapeamento antes de processar.

## Assumir XML da NF-e como caminho principal

- **Problema:** foi uma hipótese, não uma decisão; lote e validade podem não
  aparecer de forma confiável ou padronizada.
- **Solução:** tratar XML apenas como possível fonte futura e exigir validação.

## Misturar fluxo operacional e fluxo técnico

- **Problema:** tecnologias e decisões humanas ficam ambíguas.
- **Solução:** manter um fluxo geral de negócio e outro interno do software.

## Desenhar DRF como serviço separado do Django

- **Problema:** cria um componente inexistente.
- **Solução:** representar `Django + DRF` no mesmo bloco de backend.

## Mostrar o banco criando JSON

- **Problema:** o banco retorna dados; não produz a resposta HTTP.
- **Solução:** deixar serialização e resposta JSON no backend.

## Usar RabbitMQ/Celery em GET simples

- **Problema:** complexidade sem benefício em consulta síncrona.
- **Solução:** reservar fila e workers para processamento assíncrono.

## Desenhar retorno direto do worker ao Django

- **Problema:** acopla componentes e representa incorretamente a fila.
- **Solução:** o worker atualiza a persistência/estado; o cliente consulta depois.

## Automatizar OCR sem confirmação

- **Problema:** etiqueta ruim ou leitura incorreta pode gerar uma validade falsa.
- **Solução:** IA sugere e uma pessoa confirma.

## Endereçar hardware por prateleira cedo demais

- **Problema:** mudança física de produtos exige manutenção detalhada e sujeita a
  erro.
- **Solução:** adiar a camada física e, no primeiro estágio, sinalizar por
  gôndola.
