---
title: "Building a Free bot-based message extension agent for Microsoft Teams Without Microsoft 365 Copilot: Leveraging Ollama with Llama3.2"
description: ""
date: 2025-01-20T17:07:40.206Z
preview: ""
draft: false
tags: ["Microsoft Teams", "Bot", "Message Extension", "Ollama", "Agent", "teams toolkit", "Llama3.2", "Docker", "Copilot","M365", "Teams app test Tool"]
categories: []
types: ""
---

In this blog post, I will guide you through creating a bot-based message extension for Microsoft Teams, without the necessity of the [Microsoft 365 Copilot license](https://learn.microsoft.com/en-us/microsoftteams/platform/sbs-messagingextension-searchcommand-plugin?tutorial-step=1) or waiting until joining the Microsoft 365 Developer Technology Adoption Program [(TAP)](https://developer.microsoft.com/en-us/microsoft-365/tap)

While Microsoft 365 Copilot provides enhanced features for enterprise users, you can still build powerful bots using Ollama, a locally run model like Llama3.2, to handle natural language processing.

### 1. Setting Up Ollama Locally Using Docker Compose
In this section, I’ll walk you through setting up Ollama locally using Docker Compose. This step-by-step guide will show you how to run Ollama with the `Llama3.2` model, providing you with a `local environment` to process natural language queries for your Microsoft Teams bot.

My approach to setting up a local environment is inspired by the [n8n self-hosted AI starter kit](https://github.com/n8n-io/self-hosted-ai-starter-kit).

The main idea behind was to separate the main Ollama service from the initialization service that pulls models.


{{< mermaid >}}
graph TD
    A[Ollama_Main_API_Service] -->|Port 11434| B[Ollama_Model_Server_Llama_Models]
    B --> C[Ollama_Pull_Models_Service]
    C --> D[Downloads_Models_llama3.2_llama2_nomic_embed_text]
    A -->|Exposes_API| B
    C -->|Depends_on| A
    C -->|Downloads_Models| B
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#ccf,stroke:#333,stroke-width:2px
    style C fill:#cfc,stroke:#333,stroke-width:2px
    style D fill:#fcf,stroke:#333,stroke-width:2px
{{< /mermaid >}}

The main Ollama (`API service`) runs the Ollama model server and exposes the API on port 11434.

The second instance (`init-ollama`) is responsible for pulling the models (e.g., `llama3.2`) when the container starts.

The steps to run environment is quite simple, [download](blob:https://github.com/39c48482-85a2-4b6c-8971-7e80e548b580) the Docker Compose YAML file and run:

```sh
docker compose --profile cpu up
```
![alt text](/images/post4/image-2.png)

{{< alert "circle-info" >}}
**Note** If you are interested to GPU you can upgrade this or inspiring from the n8n template
{{< /alert >}}


#### 1.1 check model pulling

After a while, we can check our service by running the curl command:

```sh
curl -X GET http://localhost:11434/v1/models
```
If the model(s) are available, we should get a response as shown below:

![alt text](/images/post4/image.png)

#### 1.2 check completions endpoint

After the model loads successfully, we can proceed with running some prompts:
```sh
 curl -X POST http://localhost:11434/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "llama3.2:latest",
    "messages": [{"role": "system", "content": "You are a helpful assistant."}, {"role": "user", "content": "Hello, Ollama!"}]
  }'
```
![alt text](/images/post4/image-1.png)

### 2. Updating the LlamaModel.ts
After setting up Ollama, we will go through the necessary updates to the [original `LlamaModel.ts` file](https://github.com/microsoft/teams-ai/blob/main/js/packages/teams-ai/src/models/LlamaModel.ts).

I’ve overridden the `completePrompt` method to adjust the payload structure to properly interact with Ollama’s API endpoints.  

The most important change is in the payload used to communicate with the service endpoint. I’ve modified it from:

```ts
{
  input_data: {
                    input_string: result.output,
                    parameters: template.config.completion
                }
}
```
to use the right format

```ts
 const adjustedPayload = {
            model: "llama3.2:latest", // Use the correct model identifier
            prompt: result.output.map(msg => msg.content).join(' '), // Flatten messages into a single prompt string
            max_tokens: template.config.completion.max_tokens || 50,
            temperature: template.config.completion.temperature || 0.7,
            //completion_type: "chat",
        };
```
And instead of making the existing request:
```ts
  await this._httpClient.post<{ output: string }>(this.options.endpoint, {
                input_data: {
                    input_string: result.output,
                    parameters: template.config.completion
                }
            });
```
I use my adjustedPayload 
```ts
await this.llamaModel['_httpClient'].post(this.llamaModel.options.endpoint, adjustedPayload);
``` 

And that's it! 😉

### 3. Integrating with Microsoft Teams Samples
To simplify my testing, I used the existing [concept sample](https://github.com/microsoft/teams-ai/tree/main/js/samples/03.ai-concepts/e.customModel-LLAMA) provided by the Microsoft Teams AI team.  
This sample typically requires an Azure subscription and use Azure Open AI Studio to create a Llama model. However, in our case, we're doing it for free 😁 by using our local platform and updating the code to make it work seamlessly.

To start using `LlamaModelLocal` with your MS Teams agent, just [download](blob:https://github.com/9f48bb95-8f70-4989-af9e-19c80e752913) the file, add it to your project's `src` directory, and import the new `LlamaModelLocal` instead of the original `LlamaModel`:

```ts
import { LlamaModelLocal } from "./oLlamaModel";
```

Next, replace ```ts const model = new LlamaModel ``` with ```ts const model = new LlamaModelLocal ```

Finally, define  `LLAMA_ENDPOINT` in your .env file to point to `v1/completions`
```sh
LLAMA_ENDPOINT= http://localhost:11434/v1/completions
```


### 4. Testing and Debugging with Microsoft Teams Developer Tools

Finally, we will be able to go through testing and debugging our bot using the Teams app test tool. 

![alt text](/images/post4/image-3.png) 

We can start debugging by simply hitting `F5` or click start debugging in RUN menu in VsCode.

{{< alert "circle-info" >}}
**Note:** Make sure to run `npm i` or `yarn i` before starting debugging.
{{< /alert >}}

And here we go! An instance of the Teams app test tool should open at `http://localhost:some_port_number/`.

![alt text](/images/post4/image-4.png)
![alt text](/images/post4/image-5.png)


Now, let's dive into testing our agent!  
Since I've enabled the `logRequests` feature and I'm running in debug mode, I have access to the secret word. Yes, I know it's a bit like cheating, but I couldn't resist 😇.

![alt text](/images/post4/image-6.png)

![alt text](/images/post4/image-8.png)

![alt text](/images/post4/image-7.png)





Because cost matters, this approach allows us to start developing a Microsoft Teams Agent using natural language processing locally with Ollama, without relying on Microsoft 365 Copilot licenses. It’s a cost-effective, easy-to-setup solution for building and testing Teams agents.

### Demo and Code Sources:
The complete source code used in this demo can be found in this [GitHub repository](https://github.com/agentifyanchor/ollama-teams-agent-llama32). 

In the next post, we’ll explore how to create a custom engine agent, deploy it to Microsoft Teams, and use [Dev Tunnel SDK](https://learn.microsoft.com/en-us/azure/developer/dev-tunnels/) to expose publicly our local Ollama endpoint to the internet.

Stay tuned! 👋


