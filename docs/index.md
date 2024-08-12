# Introduction

LLM Toolkit helps you build full-featured AI-powered apps quickly on Bubble.io.

This site covers what you need to know to setup and use the plugin.

(Note: this documentation is still largely incomplete.  We're working on it! - Aug 12, 2024)

[Click Here](https://bubble.io/plugin/chatgptllm-toolkit---w-streaming-1670531100735x105135745568079870) for the plugin page.

## Features

- 🚫 **NO More Waiting:** Experience real-time streaming of responses, reminiscent of the official ChatGPT interface. Say goodbye to timeouts and prolonged waits!

- 💪 **Support for 100+ Models:** Including OpenAI, Anthropic/Claude, Llama, Mistral, Google Gemini, and more! Unlock unparalleled versatility and scalability for your applications!

- 🤖 **Assistants API with Streaming:** Create and use OpenAI Assistants in real-time by streaming your runs. Also supports all other functions of the API.

- 🧠 **Enhanced Memory:** Multi-turn conversations made easy with our intuitive message history. Perfect memory that just works.

- 🛠 **Function Calling & API Execution:** Supercharge your apps with custom ChatGPT plugins or integrate third-party data sources from APIs.

- 👁️‍🗨️ **Multi-modal support (eg GPT-4o)** Elevate your AI experience by integrating GPT-4o, enabling your applications to understand and interpret visual and auditory data alongside text, broadening the scope of interaction and functionality.

- ⏳ **Token Monitoring:** Keep an eye on your token consumption for every request you make.

- ✂ **Automatic Truncation:** Effortlessly manage messages without worrying about input length.

- 🛑 **Stream Interruption:** Regain control and steer the conversation when ChatGPT goes off-course.

- 🌐 **Web Search Capabilities:** Built-in web search enables you to extract relevant information from the web in real-time using Google search, or paste URLs/links directly for sites you are interested in.

- 📂 **File Uploads:** Seamlessly extract text from uploaded files (.pdf, .pptx, .docx, .csv, and many more types). It's easier than ever to add your own data sources to chats.

- 📌 **Bubble-native Vector Storage & Search:** Super-charge your app with "Retrieval Augmented Generation". Introducing Bubble-native embedding vector storage and search, so that you can search through your data without requiring Pinecone, Weaviate, or another third-party vector database service.

- 🔍 **Enhanced Error Handling:** With clearer and simpler mechanisms, we've made it easier to troubleshoot and navigate unexpected events.

- 📌 **Custom Headers & bodies:** For advanced users, you have full control over the payload and headers of your request.

- ⚙ **Comprehensive API Parameters:** Fine-tune your requests using all available parameters, including frequency penalty, presence penalty, and logit bias.

- 🏠 **Custom endpoints** Use Microsoft Azure deployments or other hosting providers.

- 🏠 **Self-Hosting:** Host your own backend server for complete control over your data.



## Quickstart

The simplest way to add ChatGPT-powered streaming to your Bubble app is to add a "Data Container" element to your page.  Note that this quick overview is *not* recommended for production use cases in which you are providing an OpenAI API key.