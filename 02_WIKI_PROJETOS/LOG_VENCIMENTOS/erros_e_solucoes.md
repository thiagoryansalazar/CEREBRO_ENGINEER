# Erros e soluções - LOG_VENCIMENTOS

## Consultar continuamente o ERP sem necessidade

- **Problema:** polling constante aumenta carga, custo e acoplamento com a fonte.
- **Solução:** priorizar eventos; quando não existirem, usar consulta agendada ou
  importação de arquivo conforme a capacidade da fonte.
- **Prevenção:** definir explicitamente o gatilho e a frequência de cada
  integração.

## Projetar a integração pela linguagem do sistema de origem

- **Problema:** PHP, Java, Node.js, Elixir, Delphi ou .NET não determinam como o
  LOG deve integrar.
- **Solução:** projetar pela porta disponível: webhook, API, banco, arquivo ou
  fila.
- **Prevenção:** levantar contratos, autenticação, estabilidade e autorização da
  interface antes de escolher o conector.

## Tornar webhook obrigatório

- **Problema:** sistemas legados ou restritos podem não publicar eventos.
- **Solução:** manter três modos compatíveis: evento, consulta agendada e
  importação de arquivo.
- **Prevenção:** fazer todos os modos convergirem para a mesma validação e
  normalização.

## Generalizar o contrato executável cedo demais

- **Problema:** campos genéricos podem apagar regras já validadas para produto,
  lote e validade.
- **Solução:** tratar `entidade_monitorada`, `tipo_vencimento` e `data_limite`
  como proposta até validação.
- **Prevenção:** separar visão futura do contrato realmente implementado.

## Tratar a Arquitetura Geral apenas como fluxo temporal

- **Problema:** reduz o desenho a uma sequência de eventos e esconde
  dependências, fronteiras e responsabilidades.
- **Solução:** apresentar o artefato como Arquitetura Geral, separando mundo
  físico, ERP, LOG_VENCIMENTOS e operação humana.
- **Prevenção:** usar setas com verbos explícitos, como `consulta dados`, `envia
  alerta`, `informa resultado` e `atualiza ERP`.

## Nomear o adaptador como “Atuador PY”

- **Problema:** o nome descreve uma possível tecnologia, mas não explica a
  responsabilidade do componente.
- **Solução:** usar `Adaptador de Consulta ERP`.
- **Prevenção:** nomear blocos da arquitetura geral pela função; escolher
  linguagem e framework no fluxo técnico.

## Inverter a seta de consulta ao ERP

- **Problema:** uma seta saindo do banco sugere que o ERP inicia o envio.
- **Solução:** representar `Adaptador de Consulta ERP → consulta dados →
  Repositório de Lotes do ERP`.
- **Prevenção:** identificar quem inicia cada interação antes de desenhar a
  seta.

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
- **Solução:** manter a Arquitetura Geral separada do fluxo técnico interno do
  software.

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
