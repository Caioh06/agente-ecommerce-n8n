# 🤖 Agente de IA para Atendimento de E-commerce (n8n & Gemini)

Este projeto é um fluxo de orquestração de Inteligência Artificial construído no **n8n** para automatizar o atendimento ao cliente em um e-commerce. Utilizando o modelo LLM do **Google Gemini**, o agente atua como um assistente virtual capaz de interpretar solicitações, consultar uma base de dados externa e informar o status de pedidos em tempo real.

## 🎯 Problema de Negócio Resolvido
Em operações de e-commerce, o volume de chamados de suporte do tipo *"Onde está meu pedido?"* consome dezenas de horas semanais da equipe de atendimento. 
Este Agente de IA (AI Builder) resolve esse gargalo: ele identifica a intenção do cliente, extrai a chave de busca (e-mail ou número do pedido) e consulta a base de dados autonomamente, reduzindo o tempo de resposta a segundos e liberando a equipe humana para casos complexos.

## 🛠️ Tecnologias e Orquestração
*   **n8n:** Plataforma principal de orquestração do fluxo (vibe coding e integração de APIs).
*   **Google Gemini (LLM):** Motor cognitivo do agente para processamento de linguagem natural e tomada de decisão.
*   **Redis (Memória):** Gerenciamento de contexto da conversa, permitindo que a IA lembre o histórico do chat.
*   **Google Sheets Tool:** Integração que atua como banco de dados (ERP/Logística simulado) para busca estruturada das informações do pedido.

## 🧠 Estratégia de Prompt Engineering
Para garantir um atendimento humanizado e preciso, o *System Prompt* foi estruturado com regras estritas de comportamento e uso de ferramentas:

> *"Você é o assistente virtual de atendimento ao cliente responsável por consultar informações de pedidos... Quando o usuário solicitar informações, verifique se ele já forneceu o número do pedido ou o e-mail. Se não, peça gentilmente. Assim que receber o dado, acione a ferramenta de busca na planilha (lookup_order). Não invente informações que não estejam retornadas pela ferramenta."*

## 🔄 Como o fluxo funciona:
1. **Gatilho (Trigger):** O usuário envia uma mensagem no chat.
2. **Interpretação (AI Agent):** O Gemini analisa a mensagem com base no histórico armazenado no Redis.
3. **Uso de Ferramenta (Tool):** Se o usuário fornecer um e-mail ou número de pedido, a IA aciona autonomamente o nó do Google Sheets.
4. **Devolução (Output):** O agente estrutura os dados encontrados (Status, Valor, Data de Entrega, Rastreio) em uma resposta amigável no mesmo idioma do usuário.

## 🚀 Como testar este fluxo (Reprodução)
Como o n8n permite a portabilidade completa de fluxos via JSON:
1. Baixe o arquivo `Projeto Agente E-commerce.json` deste repositório.
2. Na sua instância do n8n (Local ou Cloud), clique em *Import from File* ou simplesmente arraste o arquivo para o canvas.
3. Configure as suas próprias credenciais (Google Gemini API, Redis e Google Sheets) nos nós correspondentes.
