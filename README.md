# Automação de Atendimento via WhatsApp com n8n e Z-API

Projeto desenvolvido para demonstrar uma automação de atendimento via WhatsApp utilizando n8n, Z-API, OpenRouter, AI Agent, memória de conversa e regras de transferência para atendimento humano.

## Objetivo

Criar um fluxo automatizado capaz de atender clientes de um negócio de aluguel, manutenção e venda de bicicletas pelo WhatsApp, reduzindo o tempo de resposta e diminuindo a perda de vendas causada pela demora no atendimento.

## Fluxo da automação

```text
Cliente no WhatsApp
↓
Z-API
↓
Webhook do n8n
↓
Filtro de mensagens
↓
Memória da conversa
↓
AI Agent
↓
OpenRouter
↓
Tratamento da resposta
↓
Z-API
↓
Resposta no WhatsApp
```

## Funcionalidades

- Receber mensagens do WhatsApp por meio da Z-API.
- Capturar mensagens no n8n através de Webhook.
- Filtrar mensagens inválidas, vazias, repetidas ou fora do escopo.
- Manter contexto usando memória de conversa.
- Gerar respostas automáticas com AI Agent conectado ao OpenRouter.
- Priorizar atendimentos de aluguel de bicicleta.
- Auxiliar em dúvidas sobre manutenção e venda.
- Encaminhar casos complexos para atendimento humano.
- Enviar a resposta final ao cliente pelo WhatsApp usando Z-API.

## Estrutura do repositório

```text
projeto-n8n-atendimento-bicicletas-zapi/
├── workflows/
│   └── atendimento-bicicletas-zapi.json
├── docs/
│   ├── passo-a-passo-n8n.md
│   ├── fluxo-da-automacao.md
│   ├── regras-de-atendimento.md
│   └── apresentacao-do-projeto.md
├── assets/
│   └── fluxo-automacao.mmd
├── .env.example
├── .gitignore
└── README.md
```

## Como importar o workflow no n8n

1. Abra o n8n.
2. Clique em `Import from File`.
3. Selecione o arquivo `workflows/atendimento-bicicletas-zapi.json`.
4. Revise os nós do fluxo.
5. Configure as credenciais dentro do próprio n8n.
6. Ative o Webhook.
7. Configure a Z-API para enviar as mensagens recebidas para o Webhook do n8n.
8. Teste enviando uma mensagem pelo WhatsApp.

## Observação de segurança

Este repositório não inclui API Keys, tokens, QR Code, senhas ou credenciais reais.

As configurações sensíveis devem ser feitas diretamente no painel do n8n, Z-API e OpenRouter.

## Variáveis esperadas

O arquivo `.env.example` mostra apenas os nomes das variáveis usadas como referência.

```text
ZAPI_BASE_URL
ZAPI_INSTANCE_ID
ZAPI_TOKEN
ZAPI_CLIENT_TOKEN
OPENROUTER_API_URL
OPENROUTER_API_KEY
OPENROUTER_MODEL
```

## Tecnologias utilizadas

- n8n
- Z-API
- OpenRouter
- AI Agent
- Webhook
- WhatsApp
- Memória de conversa

## Resultado esperado

Ao receber uma mensagem de um cliente pelo WhatsApp, o fluxo identifica a solicitação, processa o contexto, gera uma resposta automática e envia a resposta de volta pelo WhatsApp usando a Z-API.

Quando o caso exige atendimento humano, o fluxo retorna o marcador:

```text
[TRANSFERIR_ATENDIMENTO]
```

Esse marcador pode ser usado pelo n8n para acionar outro fluxo de atendimento manual.
