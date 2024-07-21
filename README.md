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
- we are not typically concerned with the speed of the LLMs. we focus on slow detailed refinement of our AI output & enhancement of information via iterative improvements applied to the response that the AI is generating.
### 2.2. Project Structure

#### 2.2.1. Core Platform
a [MicroK8s](https://microk8s.io) based deployment system, as this allows you to scale with minimal effort. just add more hosts to (ideally something like a Tailscale tailnet) & then add the worker to the Microk8s cluster. The platform is highly compatible with major operating systems, including Windows, MacOS, and Linux.

Application "Backend" or "Core", "Logic Handler", whatever i decide to call it. it is a strongly typed python based ASGI framework called [Litestar](https://litestar.dev) (formerly known as `Starlite`) based `API` that is responsible for managing the agents, the agents interaction with both Gitea instance, and the Telegram bots.
####2.2.2. AI Agents
##### 2.2.2.1. AI Frameworks & Runtimes
All self hosted, local AI & machine learning models.

###### 2.2.2.1.1. [**Ollama**](https://ollama.com)

###### 2.2.2.1.2. [**Hugging Face**](https://huggingface.co)
###### 2.2.2.1.3. [**vLLM**](https://github.com/vllm-project/vllm)

##### 2.1.2.2. Additional Libraries & Tooling
###### 2.2.2.2.1. [**outlines**](https://github.com/outlines-dev/outlines)
`Outlines` is primarily used for structured text generation, which we will use in combination with [Fabric Patterns](https://github.com/danielmiessler/fabric). However the main reason we are using `Outlines` is to provide information about the current state of development to a `Hugging Face Model` & using `Outlines` this model can be used to [make choices](https://github.com/outlines-dev/outlines?tab=readme-ov-file#multiple-choices) from a list of predefined options by returning hyperspecific strings which you can evaluate using if-else chains to respond accordingly.

Example: 
```python
import outlines

model = outlines.models.transformers("mistralai/Mistral-7B-Instruct-v0.2")

prompt = """You are a sentiment-labelling assistant.
Is the following review positive or negative?

Review: This restaurant is just awesome!
"""

generator = outlines.generate.choice(model, ["Positive", "Negative"])
answer = generator(prompt)
```
## 2. User Experience

your primary means of interacting with the agents will be you noticing them making changes to your `Gitea environment`. At the moment, rather than interfere with the task queue by making some mechanism for signaling an agent to pay attention to something,  related to the Gitea development & research, you can directly interact with the agents via individual `Telegram Bots` within an organization group chat. There will be multiple bots, each agent get's its own bot that is integrated with the agent.

The agents can assist in research and development, documentation enhancement, project management and much more 

The goal is to make what feels like a really quiet group of remote assistants that is capable of making intelligent decisions within their environment. 

Generally speaking, i think the problem with most AI tools like Devin. Not like autocomplete like Codeium or Copilot, but like a full on AI assistant that can do a lot of things. The problem is the teams are working on a OpenAI token budget so they limit the scope of the project to "this assistant is a junior dev"

We are using all self hosted AI models, & have a large number of machines. 

so we can just run the machines on constantly, and have assistants regularly.


The use of multiple local agents is primarily to increase the capabilities of the full team of agents by dividing the responsibilities up across the teams accordingly 

Part of each agents “soul” in addition to basic personality traits, includes their specific skills & expertise, similar to how one might describe their skills on a resume.

For example, you will have 1-3 agents who primarily coordinate & develop the database of your application. Their job is to work with each other to best develop a database that works with your project. Then they will provide the rest of the team with information & documentation based on what they have planned & created

The goal is to emulate a real life software development team, where the actual human user(s) act primarily as overseers & project managers, providing instructions & information to the agents, and the Gitea environment

something that I think is rather unfortunate but must be accepted is that, if you want to create something good, there is no way a brief explanation with minimal context will get you the results you want. 

Unfortunately / fortunately (depending on your opinion) I think the best way to achieve your goals is to first set up a base for the Gitea Repository you intend to have your team working in. I don’t just mean set up the Gitea project & some issues. I mean clone the repo to your machine & set up the basics of the file system 

- Provide a `<directory_name>.md` file in each directory that explains what you intend to use the directory for in the application.
- Set up important files for the project
- Provide some empty functions the “pass” + a description of the functions job as a comment
- import tools you intend to use to use for specific tasks to indicate to the agents what you intend to use for the job so they don’t try to decide on something else themselves
- Create a detailed [README.md](http://README.md) but also a [goals.md](http://goals.md) or [project.md](http://project.md) or something that explains things specifically for the team of agents
- Provide access to an index of locally downloaded documentation for dependencies & tools that the project uses so the team can reference them without needing to visit the web

Agent tasking will be handled by giving each agent a unique simple asynchronous queue (SAQ)

While I will likely include functionality to allow humans to directly manipulate tasks within a queue, it is imperative that the agents themselves are the ones who create the majority of the tasks themselves. 

Agents need to be able to manipulate text in files in a hyper specific way. Ideally I would be able to give them access to neovim + a python interpreter 

Agents need to have the ability to append tasks to their own queue as well as assign tasks to the correct team member

File Manipulation:

Utilize Python's standard library (e.g., os, pathlib, fileinput) for basic file operations like reading, writing, and appending.
Employ more specialized libraries (e.g., ast) for complex code manipulations when necessary.
AI-Generated Changes:

Leverage Ollama models to analyze project state, goals, and documentation, generating detailed tasks.
Feed these tasks to Hugging Face models to produce the desired file content changes.
Git Integration:

Employ a Python Git library (e.g., gitpython) to interact with the local Git repository.
Stage modified files using the Git library.
Commit changes with a descriptive message generated by the AI or provided by the user.
Optionally, configure automatic signing of commits.