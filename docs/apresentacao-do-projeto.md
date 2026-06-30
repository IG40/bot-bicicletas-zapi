# Apresentação do projeto

## Nome do projeto

Automação de Atendimento via WhatsApp para Aluguel de Bicicletas usando n8n e Z-API

## Problema identificado

O negócio recebe aproximadamente 20 novos clientes por dia pelo WhatsApp. Parte das vendas é perdida porque os clientes demoram a receber uma resposta.

## Solução proposta

Foi criada uma automação no n8n para receber mensagens do WhatsApp, interpretar a solicitação do cliente com inteligência artificial e responder automaticamente.

## Ferramentas utilizadas

```text
n8n
Z-API
OpenRouter
AI Agent
Webhook
Memória de conversa
WhatsApp
```

## Funcionamento

O cliente envia uma mensagem pelo WhatsApp. A Z-API encaminha essa mensagem para um Webhook no n8n. O n8n filtra a mensagem, consulta o histórico da conversa, envia os dados para o AI Agent e recebe uma resposta gerada com apoio do OpenRouter. Depois, a resposta é enviada ao cliente pela Z-API.

## Benefícios

```text
Redução do tempo de resposta
Menor abandono de clientes
Mais chances de fechar aluguéis
Atendimento padronizado
Encaminhamento de casos complexos para humanos
Organização do processo comercial
```

## Casos atendidos

```text
Aluguel de bicicletas
Manutenção de bicicletas
Venda de bicicletas
Encaminhamento para atendimento humano
```

## Conclusão

O projeto demonstra como o n8n pode ser usado para criar uma automação prática de atendimento via WhatsApp, integrando Z-API, inteligência artificial e regras de negócio.
