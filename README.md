# Awesome LLM JSON List

This awesome list is dedicated to resources for using Large Language Models (LLMs) to generate JSON or other structured outputs.
  
## Table of Contents  
  
* [Terminology](#terminology)  
* [Hosted Models](#hosted-models)
* [Local Models](#local-models)
* [Python Libraries](#python-libraries)
* [Blog Articles](#blog-articles)
* [Videos](#videos) 
* [Jupyter Notebooks](#jupyter-notebooks)
* [Leaderboards](#leaderboards)
  
## Terminology  
  
Unfortunately, generating JSON goes by a few different names that roughly mean the same thing:  
  
* Structured Outputs: Using an LLM to generate any structured output including JSON, XML, or YAML regardless of technique (e.g. function calling, guided generation).
* [Function Calling](https://www.promptingguide.ai/applications/function_calling): Providing an LLM a hypothetical (or actual) function definition for it to "call" in it's chat or completion response. The LLM doesn't actually call the function, it just provides an indication that one should be called via a JSON message.
* [JSON Mode](https://platform.openai.com/docs/guides/text-generation/json-mode): Specifying that an LLM must generate valid JSON. Depending on the provider, a schema may or may not be specified and the LLM may create an unexpected schema.
* [Tool Usage](https://python.langchain.com/docs/modules/agents/agent_types/openai_tools): Giving an LLM a choice of tools such as image generation, web search, and "function calling".  The functional calling parameter in the API request is now called "tools".
* [Guided Generation](https://arxiv.org/abs/2307.09702): For constraining an LLM model to generate text that follows a prescribed specification such as a [Context-Free Grammar](https://en.wikipedia.org/wiki/Context-free_grammar).
* [GPT Actions](https://platform.openai.com/docs/actions/introduction): ChatGPT invokes actions (i.e. API calls) based on the endpoints and parameters specified in an [OpenAPI specification](https://swagger.io/specification/). Unlike the capability called "Function Calling", this capability will indeed call your function hosted by an API server.

None of these names are great, that's why I named this list just "Awesome LLM JSON".
  
## Hosted Models

| Provider     | Models                                                                             | Links                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------|------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AnyScale     | Mistral-7B-Instruct-v0.1<br>Mixtral-8x7B-Instruct-v0.1                             | [Function Calling](https://docs.endpoints.anyscale.com/text-generation/function-calling)<br>[JSON Mode](https://docs.endpoints.anyscale.com/text-generation/json-mode)<br>[Pricing](https://docs.endpoints.anyscale.com/pricing/)<br>[Announcement (2023)](https://www.anyscale.com/blog/anyscale-endpoints-json-mode-and-function-calling-features)                                                                                     |
| Azure        | gpt-4<br>gpt-4-turbo<br>gpt-35-turbo<br>mistral-large-latest<br>mistral-large-2402 | [Function Calling](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/function-calling?tabs=python)<br>[OpenAI Pricing](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/openai-service/#pricing)<br>[Mistral Pricing](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/000-000.mistral-ai-large-offer?tab=PlansAndPrice)                                                                |
| Cohere       | Command-R                                                                          | [Function Calling](https://docs.cohere.com/docs/tool-use)<br>[Pricing](https://cohere.com/pricing)<br>[Announcement (2024-03-11)](https://txt.cohere.com/command-r/)                                                                                                                                                                                                                                                                     |
| Fireworks.ai | firefunction-v1                                                                    | [Function Calling](https://readme.fireworks.ai/docs/function-calling)<br>[JSON Mode](https://readme.fireworks.ai/docs/structured-response-formatting)<br>[Grammar mode](https://readme.fireworks.ai/docs/structured-output-grammar-based)<br>[Pricing](https://fireworks.ai/pricing)<br>[Announcement (2023-12-20)](https://blog.fireworks.ai/fireworks-raises-the-quality-bar-with-function-calling-model-and-api-release-e7f49d1e98e9) |
| Google       | gemini-1.0-pro                                                                     | [Function Calling](https://cloud.google.com/vertex-ai/docs/generative-ai/multimodal/function-calling#rest)<br>[Pricing](https://ai.google.dev/pricing?authuser=1)                                                                                                                                                                                                                                                                        |
| Mistral      | mistral-large-latest                                                               | [Function Calling](https://docs.mistral.ai/guides/function-calling/)<br>[Pricing](https://docs.mistral.ai/platform/pricing/)                                                                                                                                                                                                                                                                                                             |
| OpenAI       | gpt-4<br>gpt-4-turbo<br>gpt-35-turbo                                               | [Function Calling](https://openai.com/blog/openai-api/)<br>[JSON Mode](https://platform.openai.com/docs/guides/text-generation/json-mode)<br>[Pricing](https://openai.com/pricing)<br>[Announcement (2023-06-13)](https://openai.com/blog/function-calling-and-other-api-updates)                                                                                                                                                        |
| Together AI  | Mixtral-8x7B-Instruct-v0.1<br>Mistral-7B-Instruct-v0.1<br>CodeLlama-34b-Instruct   | [Function Calling](https://docs.together.ai/docs/function-calling)<br>[JSON Mode](https://docs.together.ai/docs/json-mode)<br>[Pricing](https://together.ai/pricing/)<br>[Announcement 2024-01-31](https://www.together.ai/blog/function-calling-json-mode)                                                                                                                                                                              |

**Parallel Function Calling**

Below is a list of hosted API models that support multiple parallel function calls. This could include checking the weather in multiple cities or first finding the location of a hotel and then checking the weather at it's location.

- azure/openai
	- gpt-4-turbo-preview
	- gpt-4-1106-preview
	- gpt-4-0125-preview
	- gpt-3.5-turbo-1106
	- gpt-3.5-turbo-0125
- cohere
	- command-r
- together_ai
	- Mixtral-8x7B-Instruct-v0.1
	- Mistral-7B-Instruct-v0.1
	- CodeLlama-34b-Instruct
 
## Local Models

[Gorilla OpenFunctions v2](https://gorilla.cs.berkeley.edu//blogs/7_open_functions_v2.html) (2024-02-27, Apache 2.0 license, [Charlie Cheng-Jie Ji et al.](https://gorilla.cs.berkeley.edu//blogs/7_open_functions_v2.html)) is an open-source language model that interprets and executes functions or plugins, handling parallel or serial function calls based on JSON Schema Objects. It supports multiple programming languages (Python, Java, JavaScript, and REST API) and detects function relevance.

[NexusRaven-V2](https://nexusflow.ai/blogs/ravenv2) (2023-12-05, Nexusflow) is an open-source 13B language model that outperforms GPT-4 in zero-shot function calling, enabling copilots and agents to use software tools effectively. It surpasses GPT-4 by up to 7% in function calling success rates for human-generated use cases involving nested and composite functions, despite never being trained on the evaluation functions. The model is further instruction-tuned on Meta's CodeLlama-13B-instruct using curated data from open-code corpora.

[Functionary](https://functionary.meetkai.com/) (2023-08-04, [MeetKai](https://meetkai.com/)) interprets and executes functions or plugins, handling parallel or serial function calls based on JSON Schema Objects. It offers models with varying compute requirements, supporting single, parallel, and nested function calls, as well as multi-turn conversations. Compatible with OpenAI-python and llama-cpp-python, Functionary enables developers to efficiently execute functions within JSON generation tasks, making it a versatile tool for a wide range of applications.

## Python Libraries


[DSPy](https://github.com/stanfordnlp/dspy/) (MIT) is a framework for algorithmically optimizing LM prompts and weights. DSPy introduced [typed predictor and signatures](https://github.com/stanfordnlp/dspy/blob/main/docs/docs/building-blocks/8-typed_predictors.md) to leverage Pydantic for enforcing type constraints on inputs and outputs, improving upon string-based fields. This feature streamlines the generation of accurate and type-safe function calls, supports decorator usage, and integrates with DSPy's pipeline composition.

[FuzzTypes](https://github.com/genomoncology/FuzzTypes) (MIT) expands Pydantic's data conversion capabilities by introducing autocorrecting annotation types for enhanced data normalization, including named entity linking and fuzzy string matching. It allows for the transformation of "dumb strings" into "smart things," facilitating the handling of complex data types such as emails, dates, and custom entities with ease.

[guidance](https://github.com/guidance-ai/guidance) (Apache-2.0) supports constrained generation, interleaving Python logic with LLM calls, an abstract chat interface that works across model types, reusable functions, and calling external tools from the LLM. Guidance automatically optimizes prompts to make generation faster than naive approaches and works with many model providers including local models (via Transformers or llama.cpp) and APIs (OpenAI, Anthropic, Cohere, VertexAI, etc).

[Instructor](https://github.com/JasonLiu-DL/instructor) (MIT) is a Python library that simplifies generating structured data like JSON from Large Language Models (LLMs) using Function Calling, Tool Calling, and constrained sampling modes like JSON mode and JSON Schema. Built on top of Pydantic, Instructor offers a user-friendly API for managing validation context, retries, and streaming responses. It supports various LLMs, including GPT-3.5, GPT-4, GPT-4-Vision, and open-source models like Mistral, Ollama, and llama-cpp-python.

[LangChain](https://github.com/langchain-ai/langchain) (MIT) provides an interface for chains, integrations with other tools, and chains for applications. LangChain offers [chains for structured outputs](https://python.langchain.com/docs/guides/structured_output) and [function calling](https://python.langchain.com/docs/modules/model_io/chat/function_calling) across models.

[LlamaIndex](https://github.com/run-llama/llama_index) (MIT) provides a suite of tools for structuring data, loading indices, and querying those indices with LLMs to obtain structured outputs. LlamaIndex provides [modules for structured outputs](https://docs.llamaindex.ai/en/stable/module_guides/querying/structured_outputs/structured_outputs.html) at different levels of abstraction, including output parsers for text completion endpoints, [Pydantic programs](https://docs.llamaindex.ai/en/stable/module_guides/querying/structured_outputs/pydantic_program.html) for mapping prompts to structured outputs using function calling or output parsing, and pre-defined Pydantic programs for specific output types.

[Marvin](https://github.com/PrefectHQ/marvin) (Apache-2.0) is a lightweight AI toolkit for building reliable, scalable, and easy-to-trust natural language interfaces. It offers a collection of self-documenting tools for common AI tasks like entity extraction, classification, synthetic data generation, and multi-modal support for images and audio. Marvin focuses on developer experience, enabling the integration of tightly-scoped "AI magic" into traditional software projects with minimal code.

[Outlines](https://github.com/outlines-dev) (Apache-2.0) facilitates structured text generation by integrating multiple models and using the Jinja templating engine for prompt construction. It supports generating text that adheres to specific formats, such as regex patterns, JSON schemas, Pydantic models, and context-free grammars. Outlines provides features like type constraints, dynamic stopping, caching, batch inference, and various sampling algorithms.

[Pydantic](https://github.com/pydantic/pydantic) (MIT) is a powerful and efficient data validation library for Python that simplifies the process of working with data structures and JSON. It allows developers to define data models using Python type annotations, ensuring that data is consistently validated and serialized. Pydantic's key features include the ability to define custom data types, perform automatic data validation, generate JSON schemas from models, and seamlessly parse and serialize JSON data.

[SGLang](https://github.com/sgl-project/sglang) (MPL-2.0) flexible frontend allows developers to specify JSON schemas using regular expressions or Pydantic models, enabling constrained decoding and ensuring the generation of valid JSON outputs. SGLang's high-performance runtime, powered by RadixAttention, accelerates JSON decoding speeds by up to 3x through automatic KV cache reuse across multiple calls.

## Blog Articles

[Structured Generation Improves LLM performance: GSM8K Benchmark](https://blog.dottxt.co/performance-gsm8k.html) (2024-03-15, .txt Engineering) demonstrates that structured generation leads to consistent and substantial improvements in LLM performance on the GSM8K benchmark across 8 different models. The article highlights additional benefits of structured generation, such as "prompt consistency" and "thought-control," and suggests that structured generation is worth using even if structured output is not essential to a project.

[LoRAX + Outlines: Better JSON Extraction with Structured Generation and LoRA](https://predibase.com/blog/lorax-outlines-better-json-extraction-with-structured-generation-and-lora) (2024-03-03, Predibase Blog by Jeffrey Tang and Travis Addair) combines the Outlines library with LoRAX v0.8 to improve JSON output structuring and schema adherence through structured generation, fine-tuning, and LoRA adapters. This method significantly enhances extraction accuracy and schema fidelity in JSON generation from LLMs.

[FU, Show Me The Prompt. Quickly understand inscrutable LLM frameworks by intercepting API calls](https://hamel.dev/blog/posts/prompt/) (2023-02-14, [Hamel Husain](https://twitter.com/HamelHusain)) provides a practical guide to intercepting API calls made by various LLM libraries like guardrails, guidance, langchain, instructor, and DSPy using mitmproxy. By inspecting the prompts and API calls, developers can gain insights into how these tools work under the hood, assess their necessity, and make informed decisions about adopting or discarding them. The article emphasizes the importance of minimizing accidental complexity and maintaining a close connection with the underlying LLMs to avoid getting lost in framework-specific abstractions.

[Getting Started with Function Calling](https://www.promptingguide.ai/applications/function_calling) (2024-01-11, [Elvis Saravia](https://twitter.com/omarsar0)) introduces function calling, a technique enabling LLMs to connect with external tools and APIs by outputting JSON arguments. The article, part of a larger [Prompt Engineering Guide](https://www.promptingguide.ai/), provides an example of using OpenAI's API to build a conversational agent that answers questions about weather in a given location. It also highlights potential applications of function calling in natural language understanding, math problem-solving, API integration, and information extraction.

[Pushing ChatGPT's Structured Data Support To Its Limits](https://minimaxir.com/2023/12/chatgpt-structured-data/) (2023-12-21, [Max Woolf](https://twitter.com/minimaxir)) delves into leveraging ChatGPT's structured data capabilities using the paid API, JSON schemas, and the Pydantic library. Key insights include using prompt engineering and system prompts to improve output quality, employing Pydantic to simplify schema definition, and applying techniques like two-pass generation, optional inputs, structured input data, nested schemas, and chain-of-thought reasoning. The article highlights the cost efficiency and determinism benefits of structured data support, even with smaller models.

[Why use Instructor?](https://github.com/JasonLiu-DL/instructor/blob/main/docs/why.md) (2023-11-18, [Jason Liu](https://twitter.com/jxnlco)) explains the benefits of using the library for structured data extraction from LLMs. Built on top of Pydantic and OpenAI, Instructor offers a familiar and readable approach compared to raw JSON schemas. The library supports partial extraction, iterables, lists, and simple types, making it easy to try and install. Instructor also includes a self-correcting mechanism using Pydantic's validation model, allowing developers to add validators to the model to correct data without relying solely on prompts. After reading this article, be sure to read the [Instructor Cookbook](https://jxnl.github.io/instructor/examples/) and the [non-Instructor-Related Blog](https://jxnl.github.io/instructor/blog/) content on the [Instructor website](https://jxnl.github.io/instructor/).

[Using grammars to constrain llama.cpp output](https://www.imaurer.com/llama-cpp-grammars/) (2023-09-06, [Ian Maurer](https://twitter.com/imaurer)) integrates context-free grammars with llama.cpp to refine LLM outputs, particularly for biomedical data. Employing Grammar Builder and a JSON schema to grammar conversion script, this approach yields more accurate and schema-compliant responses, bypassing the need for extensive prompt engineering.

[Using OpenAI functions and their Python library for data extraction](https://til.simonwillison.net/gpt3/openai-python-functions-data-extraction) (2023-07-09, [Simon Willison](https://simonwillison.net/)) demonstrates how to extract structured data from text using the OpenAI Python library and function calling in a single API call. The article provides a code example that defines an `extract_locations()` function to extract location names and country ISO codes from a given text. It also discusses the limitations of using streaming with function calls and suggests using the `ijson` library for parsing streamed JSON chunks when necessary to provide visible feedback during long-running API calls.

## Videos


[Mistral AI Function Calling](https://www.youtube.com/watch?v=eOo4GfHj3ZE) (2024-02-24, [Sophia Yang](https://twitter.com/sophiamyang) [Mistral AI](https://mistral.ai/)) demonstrates how Mistral AI's function calling feature allows LLMs to connect to external tools, such as user-defined functions and APIs. By specifying tools and providing a query, users can leverage the LLM to generate function arguments, execute the selected function, and obtain results. While the video example focuses on retrieving payment information from a pandas DataFrame, this function calling capability could be extended to generate or manipulate JSON data by defining appropriate tools and functions.

[Function Calling in Ollama vs OpenAI](https://www.youtube.com/watch?v=RXDWkiuXtG0) (2024-02-13, [Matt Williams](https://twitter.com/Technovangelist)) compares the implementation of function calling in Ollama and OpenAI models. It clarifies that function calling is a misnomer, as the model itself does not call functions but rather generates output in a structured format like JSON, which the calling program can then parse to invoke functions. The video demonstrates how to achieve this using Python with both APIs, highlighting Ollama's simpler approach using the `format_json` parameter and a JSON schema. It also touches on using few-shot prompts to improve consistency in the model's responses.

[LLM Engineering: Structured Outputs](https://www.youtube.com/watch?v=1xUeL63ymM0) (2024-02-12, [Jason Liu](https://twitter.com/jxnlco), [Weights & Biases Course](https://www.wandb.courses/)) Author of the Instructor library, offers a concise course on handling structured JSON output, function calling, and complex validations using Pydantic. This course covers the essentials of extracting and validating structured data from LLMs, making machine learning pipelines more robust and reliable, and integrating complex models and pipelines into production environments efficiently.

[Why Pydantic became indispensable for LLMs](https://www.factsmachine.ai/p/how-pydantic-became-indispensable) (2024-01-19, [Adam Azzam](https://twitter.com/aaazzam)) explains how the Pydantic data validation library has emerged as a critical tool for working with LLMs. Pydantic enables sharing data models via standardized JSON schemas, which LLMs have been trained on extensively. This allows LLMs to reason between unstructured and structured data effectively. The article highlights the importance of quantizing the decision space for LLMs by using standards like JSON schemas that they understand well. However, it also notes potential issues due to LLMs being overfit to older JSON schema versions.

[Pydantic is all you need](https://www.youtube.com/watch?v=yj-wSRJwrrc) (2023-10-10, [Jason Liu](https://twitter.com/jxnlco), [AI Engineer Conference](https://www.ai.engineer/)) discusses the importance of using Pydantic for structured prompting and output validation when working with large language models (LLMs). The talk introduces the Instructor library, which integrates Pydantic with OpenAI's function calling, enabling type-safe and modular prompts. Liu also showcases advanced applications like building knowledge graphs, query planning, and fact extraction, demonstrating how structured prompting can lead to more reliable and maintainable LLM-powered applications.

## Jupyter Notebooks

[Function Calling with llama-cpp-python and OpenAI Python Client](https://github.com/abetlen/llama-cpp-python/blob/main/examples/notebooks/Functions.ipynb) demonstrates the integration of function calling with llama-cpp-python and the OpenAI Python Client, including setup using the Instructor library. The notebook provides examples of retrieving weather information and extracting user details.

[Function Calling with Mistral Models](https://colab.research.google.com/github/mistralai/cookbook/blob/main/function_calling.ipynb) demonstrates how to use function calling to connect Mistral models with external tools, enabling users to build applications for specific use cases. The notebook walks through a simple example involving a payment transactions dataframe, defining two Python functions to retrieve payment status and date.

[chatgpt-structured-data](https://github.com/minimaxir/chatgpt-structured-data) by [Max Woolf](https://twitter.com/minimaxir) provides a collection of Jupyter Notebook demos showcasing ChatGPT's function calling and structured data support. The notebooks cover various use cases such as generating blog post summaries, solving sister problems, retrieving current weather data, working with simple and nested schemas, and handling structured input data.

## Leaderboards

[Berkeley Function-Calling Leaderboard (BFCL)](https://gorilla.cs.berkeley.edu/blogs/8_berkeley_function_calling_leaderboard.html) is an evaluation framework for LLMs' function-calling capabilities, covering diverse programming languages and complex use cases. The BFCL includes over 2k question-function-answer pairs across languages like Python, Java, JavaScript, SQL, and REST API, focusing on simple, multiple, and parallel function calls, as well as function relevance detection.
