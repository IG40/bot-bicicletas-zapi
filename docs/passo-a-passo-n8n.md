# Passo a passo do fluxo no n8n com Z-API

Este documento descreve como o fluxo foi montado manualmente no n8n.

## 1. Criar o Webhook

O primeiro nó criado no n8n foi o Webhook.

Função do nó:

- Receber as mensagens enviadas pela Z-API.
- Iniciar automaticamente o fluxo sempre que chegar uma nova mensagem.
- Capturar dados como número do cliente, nome, mensagem e identificador da conversa.

Configuração sugerida:

```text
Node: Webhook
Método: POST
Path: atendimento-bicicletas-zapi
Response Mode: Respond Later
```

## 2. Receber dados da Z-API

A Z-API encaminha para o Webhook os dados recebidos pelo WhatsApp.

Exemplo de informações utilizadas pelo fluxo:

```text
Nome do cliente
Número do WhatsApp
Texto da mensagem
ID da conversa
Tipo da mensagem
Data e hora do envio
```

## 3. Filtrar mensagens inválidas

Depois do Webhook, foi criado um filtro para impedir que mensagens inválidas avancem no atendimento.

O filtro verifica:

- Se existe texto na mensagem.
- Se a mensagem não está vazia.
- Se não é mensagem de grupo, quando o atendimento for individual.
- Se o conteúdo pode ser tratado pelo agente.
- Se não é uma mensagem duplicada.

Caso a mensagem seja válida, ela segue para o AI Agent.

Caso contrário, o fluxo pode ser encerrado.

## 4. Adicionar memória da conversa

A memória é usada para manter o contexto do atendimento.

Exemplo:

```text
Cliente: Quero alugar uma bicicleta.
Bot: Para qual dia você gostaria?

Cliente: Amanhã.
Bot: Perfeito. Você prefere aluguel por hora ou diária?
```

Sem memória, o atendimento poderia perguntar novamente informações já enviadas pelo cliente.

## 5. Configurar o AI Agent

O AI Agent é responsável por interpretar a mensagem do cliente e gerar uma resposta adequada.

O agente considera:

- Mensagem atual do cliente.
- Histórico da conversa.
- Dados armazenados na memória.
- Regras do negócio.
- Prioridade dos atendimentos.

Ordem de prioridade:

```text
1. Aluguel de bicicleta
2. Manutenção
3. Venda
```

## 6. Conectar o AI Agent ao OpenRouter

O OpenRouter é utilizado como provedor de inteligência artificial.

Ele recebe o contexto enviado pelo AI Agent e retorna uma resposta natural para o cliente.

A resposta deve ser curta, clara e voltada para resolver a solicitação do cliente.

## 7. Criar regra de transferência para humano

Quando o atendimento automático não for suficiente, o agente deve retornar exatamente:

```text
[TRANSFERIR_ATENDIMENTO]
```

Esse retorno é usado pelo n8n para acionar um fluxo separado de atendimento humano.

A transferência deve ocorrer quando:

- O cliente pedir um atendente.
- A pergunta estiver fora do escopo.
- Houver reclamação complexa.
- Faltarem informações importantes.
- A solicitação exigir análise humana.
- A dúvida for técnica demais.

## 8. Tratar a resposta gerada

Após a resposta do AI Agent, o n8n verifica se o texto retornado é uma resposta comum ou se é o marcador de transferência.

Se for uma resposta comum, o fluxo envia a mensagem ao cliente.

Se for `[TRANSFERIR_ATENDIMENTO]`, o fluxo encaminha para atendimento humano.

## 9. Enviar resposta pela Z-API

O último nó envia a resposta para o cliente via WhatsApp utilizando a Z-API.

Dados usados no envio:

```text
Número do cliente
Mensagem gerada
ID da instância configurada na Z-API
Token da instância configurado no n8n
Client Token configurado no n8n
```

## 10. Testar o fluxo

Testes recomendados:

```text
Cliente: Quero alugar uma bicicleta.
Cliente: Preciso de manutenção.
Cliente: Vocês vendem bike?
Cliente: Quero falar com atendente.
Cliente: Tenho uma reclamação.
```

O fluxo deve responder automaticamente nos casos simples e transferir para humano nos casos complexos.
