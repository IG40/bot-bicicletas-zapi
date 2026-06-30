# Fluxo da automação com Z-API

## Visão geral

A automação foi criada para funcionar como um atendente virtual no WhatsApp.

O cliente envia uma mensagem, a Z-API recebe essa mensagem e encaminha para o n8n. Dentro do n8n, a mensagem passa por filtros, memória de conversa, AI Agent e OpenRouter. Depois disso, a resposta é enviada novamente ao WhatsApp pela Z-API.

## Diagrama textual

```text
WhatsApp do cliente
↓
Z-API recebe a mensagem
↓
Webhook do n8n captura o evento
↓
Filtro valida o conteúdo recebido
↓
Memória recupera contexto anterior
↓
AI Agent interpreta a solicitação
↓
OpenRouter gera a resposta
↓
n8n verifica se precisa transferir
↓
Z-API envia a resposta
↓
Cliente recebe a mensagem
```

## Entradas do fluxo

O fluxo pode receber:

```text
Texto da mensagem
Nome do cliente
Número do WhatsApp
Histórico da conversa
Dados adicionais enviados pelo Webhook
Informações armazenadas na memória
```

## Saídas do fluxo

O fluxo retorna apenas uma mensagem de texto para o cliente.

Exemplos:

```text
Claro! Para qual dia você gostaria de alugar a bicicleta?
```

```text
Temos opções para manutenção. Qual problema sua bicicleta está apresentando?
```

```text
[TRANSFERIR_ATENDIMENTO]
```

## Critérios de sucesso

O fluxo é considerado funcional quando:

- Recebe mensagens pelo Webhook.
- Filtra mensagens inválidas.
- Gera respostas coerentes.
- Mantém contexto entre mensagens.
- Envia respostas pelo WhatsApp usando Z-API.
- Transfere para humano quando necessário.
