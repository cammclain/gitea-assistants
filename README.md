My intention is to learn more about AI by creating a python based agent that can interact with your Gitea environment. 

The agents should have a comparable level of “read write access” within the Gitea instance.

The agents are able to query the Gitea API & create a pretty good understanding of what you are up to in the Gitea application 

They can assist you in research on relevant subjects, and provide you not only with cited sources but and development, documentation enhancement, project management and much more 

The goal is to make what feels like a really dumb remote assistant that is capable of making intelligent decisions within its environment 

 you Gitea environment 


# gitea-assistants
## Experiments with building a fully self hosted AI assistant within your Gitea instance
---

---

## 1. Project Overview

My intention is to learn more about `Git`, `AI` & `Machine learning` & more by creating a `python based` platform capable of managing `a team of customized self hosted AI agents` that can interact with a private `Gitea instance` via an extremely comprehensive integration with `Gitea's HTTP API`. 

In addition to the `Gitea API information` & information from conversations you can have with the agents via [Telegram](https://telegram.org) Bot integration, the agents also have a wide variety of tools such as:
- search engine
- Document Stores (markdown formatted documents with relevant information)
- Databases (primarily SQL based via `SQLAlchemy` & `advanced_sqlalchemy`)

These systems allowing the to act as a coordinated `dev team`. 

## 2. Technical Overview

### 2.1. Technical Expectations (Goals & Objectives / Non-Goals & Anti-Objectives)
#### 2.1.1. Goals & Objectives
- Create a platform where can manage a team of AI agents acting as a highly coordinated team that can interact with a Gitea instance
- Develop primarily in strongly typed Python.
- Use a variety of AI & machine learning models to assist in a variety of tasks
- design the files to be modular and easy to understand. the goal is to make it easy to edit files as they are relatively short in length and easy to understand, but large in quantity. This allows you to have a high degree of flexibility with how you can add the files to an agent's context. This means more lightweight models can still be useful when given a smaller scope for the context of whatever it is developing.
#### 2.1.2. Anti-Goals & non objectives of the project
- we are not typically concerned with the speed of the LLMs. we focus on slow detailed refinement of our AI output & enhancement of information via iterative improvements approached in a 
### 2.2. Project Structure

#### 2.2.1. Core Platform
a [MicroK8s](https://microk8s.io) based deployment system, as this allows you to scale with minimal effort. just add more hosts to (ideally something like a Tailscale tailnet) & then add the worker to the Microk8s cluster. The platform is highly compatible with major operating systems, including Windows, MacOS, and Linux.

Application "Backend" or "Core", "Logic Handler", whatever i decide to call it. it is a strongly typed python based ASGI framework called [Litestar](https://litestar.dev) (formerly known as `Starlite`) based `API` that is responsible for managing the agents, the agents interaction with both Gitea instance, and the Telegram bots.
####2.2.2. AI Agents
##### 2.2.2.1. AI Frameworks & Runtimes
All self hosted, local AI & machine learning models.

- [**Ollama**](https://ollama.com)
- [**Hugging Face**](https://huggingface.co)
- [**vLLM**](https://github.com/vllm-project/vllm)

##### 2.1.2.2. Additional Libraries & Tooling
- [**outlines**](https://github.com/outlines-dev/outlines)

## 2. User Experience

your primary means of interacting with the agents will be you noticing them making changes to your `Gitea environment`. At the moment, rather than interfere with the task queue by making some mechanism for signaling an agent to pay attention to something,  related to the Gitea development & research, you can directly interact with the agents via individual `Telegram Bots` within an organization group chat. There will be multiple bots, each agent get's its own bot that is integrated with the agent.

The agents can assist in research and development, documentation enhancement, project management and much more 

The goal is to make what feels like a really quiet group of remote assistants that is capable of making intelligent decisions within their environment. 

Generally speaking, i think the problem with most AI tools like Devin. Not like autocomplete like Codeium or Copilot, but like a full on AI assistant that can do a lot of things. The problem is the teams are working on a OpenAI token budget so they limit the scope of the project to "this assistant is a junior dev"

We are using all self hosted AI models, & have a large number of machines. 

so we can just run the machines on constantly, and have assistants regularly.

## WORK IN PROGRESS