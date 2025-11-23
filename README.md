# Weaver – Azure AI Mentor Bot
## Overview
Weaver é um agente dedicado a guiar estudantes e interessados em Azure e inteligência artificial. Oferece respostas atualizadas, adaptadas à experiência técnica do usuário. Envia respostas longas por email.

Por: Adriana Crespo Ruco


## História
Bot nascido de minha própria necessidade de estudar inteligência artificial e Azure, e da minha completa frustração com os modelos comuns quando suas respostas se confundiam (e me confundiam) entre diferentes tecnologias. Conforme eu aprendia a aprimorá-lo, ele foi se tornando um companheiro mais e mais útil em meus estudos, acelerando meu aprendizado e tornando tudo mais divertido e interessante. 


## Key features
- Orientação específica sobre serviços Azure, assistência na criação de recursos, identificação de erros, otimização de custos
- Respostas calibradas para promover o aprendizado independente e personalizado
- Preocupação com o uso responsável da IA, apoiado por uma Knowledge Base rigorosa
- Envio de respostas mais aprofundadas (estruturadas em HMTL, em prol da legibilidade) por email, a pedido do usuário


## Público-alvo
- Estudantes focados em Azure   
- Professores e mentores buscando auxílio na produção de aulas e materiais didáticos 
- Usuários experientes com dúvidas sobre o novo portal da Azure Foundry
- Interessados em IA responsável e ética
- Candidatos a vagas de TI/IA buscando aprender e praticar para entrevistas de emprego


## Arquitetura
- Weaver, agente IA criado em gpt-4o-mini com engenharia de prompt (comportamento esperado, workflow) 
- Knowledge Base formada por documentos em PDF, oficiais e recentes, sobre Azure e sobre IA responsável
- emailSending_Tool (Logic App Action webhook)


## Testes
Incluídos desde o começo do projeto, os casos de teste partiram das Key Features, do Público-alvo e dos Casos de Uso para avaliar e comparar a eficiência de diferentes iterações do bot. Alguns dos casos de teste utilizados:

### Caso de Teste 1: **Respostas Relevantes e Atualizadas**
    - Objetivo: Testar a habilidade do bot de buscar respostas relevantes na Knowledge Base.
    - Entrada: "Quais as diferenças entre as versões nova e clássica do Azure Foundry?"
    - Ação Esperada: O bot deve buscar na Knowledge Base e responder comparando as versões do Azure AI Foundry.
    - Resultado Esperado: Uma resposta com informações atualizadas sobre as versões corretas do software.
 
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/32d8c600-a406-453b-8ba4-0d45913e7da3" />
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/0965659f-ea3d-4a6c-8014-8a861f239be9" />

### Caso de Teste 2: **Envio de Email**
    - Objetivo: Avaliar a funcionalidade de envio de email.
    - Entrada: "Me envie por email um plano detalhado de uma única aula universitária sobre ética e responsabilidade na IA, para alunos do último ano de ciências da computação, com discussões recentes e relevantes em 2025."
    - Ação Esperada: O bot gera, converte para HTML e envia por email um plano de aula sobre o tema pedido. Confirma o envio e sumariza o email.
    - Resultado Esperado: Um email com um plano de aula estruturado, lógico e legível. Ums resposta confirmando e sumarizando o email.
 
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/ee007625-5f2b-41ce-9870-da72a0d9b770" />
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/4dc06da2-ee13-4782-bec2-3cfc4749d2f5" />
<img width="1322" height="297" alt="Image" src="https://github.com/user-attachments/assets/89e29ac0-b938-43d4-9df1-d7f789be89ab" />

### Caso de Teste 3: **Personalização de Resposta - Júnior**
    - Objetivo: Testar a personalização das respostas de acordo com o nível de experiência do usuário.
    - Entrada: "Olá, tudo bom? Sou nova por aqui 🌟 Como posso criar uma Máquina Virtual no Azure?"
    - Ação Esperada: O bot deve responder corretamente e de acordo com o contexto apresentado, de uma iniciante.
    - Resultado Esperado: Resposta com informações adequadas a iniciantes, começando do começo.
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/e9c18c84-75ec-42e2-a7a9-dc9d63502501" />
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/93643f92-5b00-4fed-8e0c-8431eb554fb7" />

### Caso de Teste 4: **Personalização da Resposta - Senior**
    - Objetivo: Testar a personalização das respostas de acordo com o nível de experiência do usuário.
    - Entrada: "Como você lidaria com a governança e compliance ao implantar VMs e quais ferramentas do Azure ajudariam neste cenário?"
    - Ação Esperada: O bot deve responder corretamente e de acordo com o contexto apresentado, de uma veterana.
    - Resultado Esperado: Resposta com informações adequadas a seniors, presumindo conhecimento prévio.
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/91419f3d-88ca-4907-92f8-a7a01ff7e346" />
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/ba57af2c-2768-4a9f-9cf2-ef97d6a8362d" />



## Bot Prompt
    # Introduction
    You are Weaver, a perceptive Azure AI guide. Provide actionable, witty, empathetic, and professional Azure expertise. Be warm and enthusiastic with beginners; precise and deeply technical with experts. Celebrate wins, acknowledge struggles, and affirm growth.

    ## Core Focus
    - Azure services (compute, storage, security, networking, AI/ML)
    - Ethical AI by default: contextually suggest bias checks, diverse data testing, and logging. Use information from the PDFs uploaded to Knowledge Base when helpful.
    - Meta-AI: open, positive, collaborative
    - Only concise job-like simulations when explicitly requested

    ## Response Rules (strict)
    - Max 300 words per response
    - PG tone, inclusive & diverse examples
    - Clear numbered/bulleted steps
    - Secure, minimal Python, HTML, or CSS snippets only
    - Breadth-first (give the 20% that solves 80% first), go deeper only if asked
    - Max 1 clarifying question per turn

    ## Email Workflow
    - Whenever deeper detail would be helpful (e.g., study guides, full tutorials, long references, or when the assistant hints there's much more to cover), the assistant should ask:
    “Would you like me to send a longer, structured version by email?” 
    - If the user requests email:
    1. Ask for their address (if not known).
    2. Generate the full content formatted in HTML.
    3. Call emailSending_Tool.
    4. Provide a ≥70-word confirmation summary (not the full content).

    ## Goals
    1. Learning: simple steps + analogies
    2. Implementation: ready-to-use DevOps YAML, ARM/Bicep, CLI
    3. Experimentation: scaling, cost-optimization, advanced patterns when requested
    4. Outcomes: short progress recap + self-audit prompts

    ## Opening (first message only)
    Friendly contextual greeting → introduce yourself as their Azure companion → one quick ethical dev tip (<70 words) → suggest 2-3 dynamic next topics (e.g., “AKS setup”, “Responsible AI checklist”, “GitHub Actions pipeline”)

    ## Principles
    Human-first. If off-scope, politely redirect to official docs. Probe ambiguity once, then proceed with best assumption. Email address requests do not count as clarifying questions. Monitor interaction quality to guide improvements and support a learning environment that helps the user grow.

    ## Closure
    - 1-2 sentence summary of progress/key takeaway
    - End every response with a brief follow-up question inviting the user’s next step.
    - Invite feedback occasionally, every few responses.


## Email Workflow
1. Quando o assunto rende uma resposta mais longa, o bot oferece enviá-la por email
2. Se o usuário aceita, ou sempre que o próprio usuário pedir pelo envio de um email
3. Pede o email do usuário, caso já não saiba
4. Gera o conteúdo formatado em HTML
5. Chama emailSending_Tool, produzido via Logic Apps, que envia o conteúdo formatado para o email informado
6. Confirma o envio no chat, apresentando um sumário do conteúdo enviado

<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/c1edab96-62bf-4c69-8571-5da63dbda2bc" />


## Knowledge Base
Para atualizar e melhorar as respostas do Weaver nos temas Azure e IA responsável. Contém os seguintes documentos:
- 2025 Responsible AI Transparency Report. https://www.microsoft.com/en-us/corporate-responsibility/responsible-ai-transparency-report
- Ethics guidelines for trustworthy AI. https://digital-strategy.ec.europa.eu/en/library/ethics-guidelines-trustworthy-ai
- Fairlearn: a toolkit for assessing and improving fairness in ai. https://fairlearn.org/v0.13/user_guide/further_resources.html
- Guidance for Developers and Deployers New to Public Engagement. https://partnershiponai.org/guidance-for-inclusive-ai-new-practitioners/
- Recommendation on the Ethics of Artificial Intelligence. https://unesdoc.unesco.org/ark:/48223/pf0000381137
- What is Microsoft Foundry (classic)? https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-azure-ai-foundry?view=foundry-classic
- What is Microsoft Foundry (new)? https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-azure-ai-foundry?view=foundry
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/22b6f3e9-b913-4d7c-95e0-e951bc3aa6a6" />
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/c233b67c-413b-46bd-b11d-fe74a54285cc" />


## Roadmap
Para que outros usuários possam acessar o bot, o próximo passo no projeto seria a conexão dele com, por exemplo, WhatsApp ou Microsoft Teams. Passos seguintes poderiam incluir:
1. o estabelecimento de um fluxo de feedback mais sólido entre bot e usuário; 
2. a produção e envio de arquivos pdf por email; e 
3. a conexão a outros serviços, como Language Services e Machine Learning, para o constante aprimoramento das respostas.

Estou aberta a sugestões de todos os que chegaram até aqui! Envie para dricrespo@gmail.com comentários, críticas e histórias de uso. Seu feedback manterá o Weaver ativo e relevante.


## Agradecimentos e créditos
Projeto realizado com o pontual auxílio do próprio Weaver, rodando no gpt-4o-mini e no Grok 4 (xAI), a partir do [Azure AI Foundry](https://ai.azure.com/).

Agradeço aos mentores e às companheiras do projeto de mentoria [Azure Frontier Girls](https://www.maismulheres.tech/courses/azure-frontier-girls). Uma honra estar com vocês nesta jornada.

Agradeço a meus companheiros de vida pela inspiração constante.


## Licença
Este projeto está licenciado sob a [Licença MIT](https://opensource.org/license/MIT). Você pode usar, copiar, modificar e distribuir o código, desde que atribua ao autor original. 
