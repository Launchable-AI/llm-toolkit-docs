# Actions

This is the in-depth documentation for each action that the plugin provides.  For a simpler overview of using the plugin, [click here](usage.md) for a usage and setup guide.

## Authentication

### Create Security Token

**Description:** Generates a security token using an OpenAI API key. This token can be used for authenticating API requests and can be set to expire after a specified duration.

### Parameters

- **`api_key`**
  - **Type:** String
  - **Description:** The OpenAI API key used to generate the security token.
  - **Example:** `"sk-xxxxxx"`

- **`expiration_minutes`**
  - **Type:** Integer
  - **Description:** Duration in minutes for which the security token will be valid. Default is 360 minutes (6 hours).
  - **Example:** `360`

- **`password`** (Optional)
  - **Type:** String
  - **Description:** A password to revoke or invalidate the token before its expiration. Not needed for making API calls.
  - **Example:** `"your-password"`

- **`custom_plugin_url`** (Optional)
  - **Type:** String
  - **Description:** URL of the custom server hosting the plugin, if applicable.
  - **Example:** `"https://your-custom-server.com"`
- **`Headers`** (Optional)
  - **Type:** JSON
  - **Description:** If you need to provide custom headers, such as an API key for Azure, enter them here, formatted as JSON.
  - **Example:** `{"api-key": "1234567"}`


### Expire Security Token

**Description:** Immediately expires a previously generated security token before its scheduled expiration.

### Parameters

- **`token`**
  - **Type:** String
  - **Description:** The security token that needs to be expired.
  - **Example:** `"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"`

- **`password`** (Optional)
  - **Type:** String
  - **Description:** Password for invalidating the token, if one was set during token creation.
  - **Example:** `"your-password"
- **`custom_plugin_url`** (Optional)
  - **Type:** String
  - **Description:** URL of the custom server hosting the plugin, if applicable.
  - **Example:** `"https://your-custom-server.com"`

## Chat

### Chat Completion (streaming)

**Description:** Generates a streaming response for a given prompt using the specified GPT model. This action sends a request to the OpenAI API and streams the response back as the model generates it. This is useful for real-time or large responses that need to be delivered as they are being generated.

### Parameters

- **`Element`**
  - **Type:** Element
  - **Description:** The specified front-end DataContainer, which stores the chat data.
  - **Example:** `"ChatGPTToolkit-DataContainer A."`

- **`Prompt`**
  - **Type:** Rich text editor
  - **Description:** Input message to ChatGPT. This can be left blank if you've manually set your message history using the "Set Message History" action.
  - **Example:** `"Provide a detailed analysis of the following data set..."`

- **`Hidden Context`**
  - **Type:** Rich text editor
  - **Description:** Provides extra context that you don't want the user to see in the list of messages. This could include search results or other contextual data used to inform the model's response.
  - **Important:** Do not include sensitive information, as advanced users could potentially inspect API requests and view this content.

- **`Model`**
  - **Type:** String
  - **Description:** Specifies which model to use. Supports all OpenAI models as well as 100+ non-OpenAI models via OpenRouter.
  - **Example:** `"gpt-3.5-turbo"`

- **`Security Token`**
  - **Type:** String
  - **Description:** The security token, which includes your encrypted API key. Use this if you're providing your API key to users.
  - **Example:** `"YourSecurityTokenHere"`

- **`User OpenAI API Key`**
  - **Type:** String
  - **Description:** The OpenAI API key provided by the user.
  - **Example:** `"sk-..."`

- **`Use Message History?`**
  - **Type:** Boolean
  - **Description:** Whether to include previous messages when sending a prompt. If set to "yes," the plugin will intelligently truncate to the appropriate context length.
  - **Example:** `"yes"`

- **`Smart Truncate`**
  - **Type:** Boolean
  - **Description:** Automatically trims the message history to fit into the model's context limit. Requires plugin servers.
  - **Example:** `"yes"`

- **`Last N Messages`**
  - **Type:** Number
  - **Description:** The number of messages from the message history to send with the current prompt.
  - **Example:** `"5"`

- **`Count Tokens?`**
  - **Type:** Boolean
  - **Description:** Whether to count the input/output/total tokens used for each prompt and reply. Requires plugin servers.
  - **Example:** `"yes"`

- **`Max Input Tokens`**
  - **Type:** Number
  - **Description:** Limits the number of tokens used for input to a specified value.
  - **Example:** `"3000"`

- **`Max Output Tokens`**
  - **Type:** Number
  - **Description:** Limits the number of tokens returned.
  - **Example:** `"500"`

- **`Stop Sequences`**
  - **Type:** String
  - **Description:** A comma-separated list of sequences that will cause the output to stop if produced.
  - **Example:** `"end, stop, finish, done"`

- **`Presence Penalty`**
  - **Type:** Number
  - **Description:** A penalty applied to the likelihood of generating new tokens based on whether they have appeared in the text so far.
  - **Range:** `-2.0` to `2.0`
  - **Example:** `"0.5"`

- **`Temperature`**
  - **Type:** Number
  - **Description:** Controls the randomness of the generation. Higher values make output more random; lower values make it more focused and deterministic.
  - **Range:** `0` to `2`
  - **Example:** `"0.7"`

- **`Frequency Penalty`**
  - **Type:** Number
  - **Description:** Penalizes the model for generating tokens that have already appeared in the text.
  - **Range:** `-2.0` to `2.0`
  - **Example:** `"0.5"`

- **`Logit Bias`**
  - **Type:** JSON Object
  - **Description:** Modifies the likelihood of specified tokens appearing in the completion. A JSON object mapping tokens to a bias value.
  - **Example:** `{"2435": -100, "640": -100}`

- **`Top P`**
  - **Type:** Number
  - **Description:** An alternative to sampling with temperature, called nucleus sampling. The model considers only the tokens comprising the top `p` probability mass.
  - **Range:** `0.0` to `1.0`
  - **Example:** `"0.9"`

- **`User`**
  - **Type:** String
  - **Description:** A unique identifier representing your end-user, which can help OpenAI monitor and detect abuse.
  - **Example:** `"user-123abc"`

- **`Function Call`**
  - **Type:** JSON Object
  - **Description:** Controls how the model responds to function calls. Options include `"none"` (default), `"auto"`, or specifying a function name.
  - **Example:** `{"name": "my_function"}`

- **`Functions`**
  - **Type:** Rich text editor
  - **Description:** The list of functions to include with the request. Normally set to `"Data Container's Functions"` or manually specified.
  - **Example:** `[{"name": "get_weather", "parameters": {"location": "New York"}}]`

- **`JSON mode?`**
  - **Type:** Boolean
  - **Description:** If set to "yes," ChatGPT responds with JSON data. You must specify in your user or system message that you want JSON back.
  - **Example:** `"no"`

- **`Custom Headers`**
  - **Type:** JSON Object
  - **Description:** Custom headers to include in the API request, such as the `"Organization"` header.
  - **Example:** `{"Organization": "org-123abc", "Other-Header": "ValueHere"}`

- **`Image 1`**
  - **Type:** Image Upload
  - **Description:** An optional image to pass along with the Chat Completion. Must use the `"gpt-4-vision-preview"` model if included.

- **`Image 2`**
  - **Type:** Image Upload
  - **Description:** An optional second image to pass along with the Chat Completion.

- **`User OpenRouter Key`**
  - **Type:** String
  - **Description:** If using non-OpenAI models, provide the user's OpenRouter API key here.
  - **Example:** `"your-openrouter-key"`

- **`Use OpenRouter?`**
  - **Type:** Boolean
  - **Description:** Set to `"yes"` to route requests through OpenRouter for access to additional models.
  - **Example:** `"no"`

- **`Custom Endpoint`**
  - **Type:** String
  - **Description:** The URL for routing requests to another endpoint, such as an Azure deployment.
  - **Example:** `"https://custom-endpoint.com"`

- **`Custom Body`**
  - **Type:** Rich text editor
  - **Description:** Customizes the payload of the request, overwriting all other options and properties.
  - **Example:** `{"custom_key": "custom_value"}`
 

### Chat Completion (Non-Streaming) - V2

**Description:** Generates a completion for a given prompt using the specified GPT model. This action sends a request to the OpenAI API to generate a response based on the provided messages and model parameters. It does not support streaming.

### Parameters

- **`Authorization`**
  - **Type:** String
  - **Description:** The authorization header containing the Bearer token for accessing the OpenAI API.
  - **Example:** `"Bearer sk-proj-drYyFq6U6vaHziFZg17qT3BlbkFJ0sbYQxbgLnI8hDECytZx"`

- **`Request Body`**
  - **Type:** JSON
  - **Description:** The body of the request containing details about the model and messages. Includes model name, and the list of messages with roles and content types.
  - **Example:**
    `json
    {
      "model": "gpt-4o",
      "messages": [
        {
          "role": "user",
          "content": [
            {
              "type": "text",
              "text": "The attached images are screenshots from a grant application form for NIH grants. From these images, generate a list of questions that the applicant should answer. In other words, for each input field, extract the relevant question. Delimit your generated/extracted questions with ===. Do not return any other text, other than the list of questions. Do not number or bullet-point the questions."
            },
            {
              "type": "image_url",
              "image_url": {
                "url": "https://5aa3a999252d6a2f4476f23c187ef64a.cdn.bubble.io/f1720784600236x763582507010956300/sf_424_rr_1.png"
              }
            },
            {
              "type": "image_url",
              "image_url": {
                "url": "https://5aa3a999252d6a2f4476f23c187ef64a.cdn.bubble.io/f1720784607351x596679106919240100/sf_424_rr_2.png"
              }
            }
          ]
        }
      ]
    }
    `

### Clear Message History

**Description:** This action clears the entire message history of the DataContainer.

### Parameters
- **`Element`**
  - **Type:** Element
  - **Description:** The DataContainer whose messages should be cleared.
  - **Example:** `"ChatGPTToolkit-DataContainer A."`

### Clear Current Message
**Description:** This action clears the latest message contained in the DataContainer.

### Parameters
- **`Element`**
  - **Type:** Element
  - **Description:** The DataContainer whose latest message should be cleared.
  - **Example:** `"ChatGPTToolkit-DataContainer A."`

### Set System Message

**Description:** This action allows one to tune the behaviour of an LLM at a high level. This is done by setting a system message, which is then included with every message that is sent to the LLM model.

### Parameters
- **`Element`**
  - **Type:** String
  - **Description:** The DataContainer which should recieve the system message.
  - **Example:** `"ChatGPTToolkit-DataContainer A."`
- **`System Message`**
  - **Type:** Text
  - **Description:** Set a static system message that will be included with each message sent to ChatGPT. A system message
controls the behavior of ChatGPT at a high level. You can instruct ChatGPT to respond in a particular style (eg.,
formal, comic), to assume certain knowledge (eg., "you
are an expert legal advisor"), to return responses in a
particular format (eg., "return your answer in JSON"), and
more. Note that this can also be done in the "Send
Message" actions, by setting role to "system"; this is just a
simpler way to do the same thing.
  - **Example:** `"Only respond in HTML format"`

### Add Function

(documentation coming soon)

### Set Functions

(documentation coming soon)

### Set Parameters

(documentation coming soon)

### Stop Streaming

**Description:** This action will stop a model from streaming it's message to a specified DataContainer

### Parameters
- **`Element`**
  - **Type:** String
  - **Description:** The DataContainer which whose model should stop streaming.
  - **Example:** `"ChatGPTToolkit-DataContainer A."`
- **`Trigger Message Generation Complete`**
  - **Type:** Boolean
  - **Description:** This boolean allows one to set the message generation as complete when the streaming is stopped.
  - **Example:** `"Yes"`


### Execute Function Call

(documentation coming soon)


## Assistants (OpenAI)

### List Assistants

**Description:** This action creates a list of all assistants. This action requires no parameters.

### Create Assistant

**Description:** This action allows you to create an OpenAI Assistant.

### Parameters
- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the media type of the resource. Typically set to `application/json` for JSON payloads.
  - **Example:** `"application/json"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** The bearer token used for authenticating the API request.
  - **Example:** `"Bearer sk-..."`

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Indicates beta features or specific configurations for OpenAI models. Typically used for beta assistants or configurations.
  - **Example:** `"assistants=v2"`

- **`(body) instructions`**
  - **Type:** String
  - **Description:** The system instructions that the assistant uses. The maximum length is 256,000 characters.
  - **Example:** `"You are a helpful assistant."`

- **`(body) name`**
  - **Type:** String
  - **Description:** The name of the assistant. The maximum length is 256 characters.
  - **Example:** `"My Assistant"`

- **`(body) description`**
  - **Type:** String
  - **Description:** The description of the assistant. The maximum length is 512 characters.
  - **Example:** `"This assistant helps with general inquiries."`

- **`(body) model`**
  - **Type:** String
  - **Description:** ID of the model to use. You can use the List models API to see all of your available models or see the Model overview for descriptions of them.
  - **Example:** `"gpt-4-turbo"`

- **`(body) metadata`**
  - **Type:** Object
  - **Description:** Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format. Keys can be a maximum of 64 characters long, and values can be a maximum of 512 characters long.
  - **Example:** `{"category": "customer_service"}`

- **`(body) response_format`**
  - **Type:** String
  - **Description:** Specifies the format that the model must output. Compatible with GPT-4, GPT-4 Turbo, and all GPT-3.5 Turbo models since gpt-3.5-turbo-1106. Default is `"auto"`. Setting to `{ "type": "json_object" }` enables JSON mode, which guarantees the message the model generates is valid JSON.
  - **Example:** `"auto"`

- **`(body) tools`**
  - **Type:** Array
  - **Description:** A list of tools enabled on the assistant. There can be a maximum of 128 tools per assistant. Tools can be of types `code_interpreter`, `file_search`, or `function`.
  - **Example:** `[{ "type": "code_interpreter" }]`

- **`(body) tool_resources`**
  - **Type:** Object
  - **Description:** A set of resources that are used by the assistant's tools. The resources are specific to the type of tool. For example, the `code_interpreter` tool requires a list of file IDs, while the `file_search` tool requires a list of vector store IDs.
  - **Example:** `{"file_ids": ["file-1234"]}`

- **`(body) top_p`**
  - **Type:** Float
  - **Description:** An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered.
  - **Example:** `0.1`

- **`(body) temperature`**
  - **Type:** Float
  - **Description:** What sampling temperature to use, between 0 and 2. Higher values like `0.8` will make the output more random, while lower values like `0.2` will make it more focused and deterministic.
  - **Example:** `0.7`

### Upload File

**Description:** This action allows you to upload a file to a specified endpoint. It handles the file transfer, assigns a purpose for the uploaded file, and ensures proper authentication through the necessary API key.

### Parameters

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** The bearer token used for authenticating the API request. This ensures that only authorized users or systems can perform the file upload.
  - **Example:** `"Bearer sk-..."`

- **`(param.) file`**
  - **Type:** File Object
  - **Description:** The file object that needs to be uploaded. This is not just the file name but the entire file object, which includes all necessary metadata for the upload.
  - **Example:** `"Static file"` or `"Dynamic link"`

- **`(param.) purpose`**
  - **Type:** String
  - **Description:** Specifies the purpose for which the file is being uploaded. This helps in categorizing the file within the system, ensuring it is used appropriately.
  - **Example:** `"assistants"`

### Retrieve File

**Description:** This action allows you to retrieve a file using its unique identifier. The file can be downloaded or accessed as needed, with the retrieval process being secured through an API key.

### Parameters

- **`(path) file_id`**
  - **Type:** String
  - **Description:** The unique identifier for the file you want to retrieve. This ID is required to locate and access the specific file within the system.
  - **Example:** `"file-abc123"`

- **`Enter your API key`**
  - **Type:** String
  - **Description:** The API key used for authenticating the retrieval request. This ensures that only authorized users or systems can access the file.
  - **Example:** `"sk-..."`

### Delete File

**Description:** This action allows you to delete a specific file using its unique identifier. The file will be permanently removed from the system once the deletion request is successfully processed.

### Parameters

- **`(path) file_id`**
  - **Type:** String
  - **Description:** The unique identifier for the file you want to delete. This ID is necessary to locate the specific file within the system that needs to be removed.
  - **Example:** `"file-ATfVzmvTFPDHol9rGdFYDpgN"`

- **`Enter your API key`**
  - **Type:** String
  - **Description:** The API key used to authenticate the deletion request. This ensures that only authorized users or systems can delete the file.
  - **Example:** `"sk-..."`

### Retrieve File Content

**Description:** This action allows you to retrieve the content of a specific file using its unique identifier. The file's content will be accessed and returned as part of the response.

### Parameters

- **`(path) file_id`**
  - **Type:** String
  - **Description:** The unique identifier for the file whose content you want to retrieve. This ID is necessary to locate and access the specific file within the system.
  - **Example:** `"file-ATfVzmvTFPDHol9rGdFYDpgN"`

- **`Enter your API key`**
  - **Type:** String
  - **Description:** The API key used to authenticate the request. This ensures that only authorized users or systems can access the file's content.
  - **Example:** `"sk-..."`

### Modify Assistant

**Description:** This action allows you to modify the settings and attributes of an existing assistant. You can update various properties such as its name, instructions, tools, and model configuration using the specified parameters.

### Parameters

- **`(path) assistant_id`**
  - **Type:** String
  - **Description:** The unique identifier for the assistant you want to modify. This ID is required to locate and update the specific assistant within the system.
  - **Example:** `"assistant-123456789"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the media type of the resource. This should be set to `"application/json"` to ensure the server correctly interprets the request body as JSON data.
  - **Example:** `"application/json"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** The API key or token used for authorization. This header authenticates the request, ensuring that only authorized users can modify the assistant.
  - **Example:** `"Bearer sk-..."`

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Used to specify beta features for OpenAI's assistants. This allows access to certain experimental or pre-release functionalities. 
  - **Example:** `"assistants=v2"`

- **`(body) instructions`**
  - **Type:** String
  - **Description:** The updated system instructions that the assistant should follow. These instructions guide the assistant’s behavior and responses.
  - **Example:** `"Provide concise answers to user queries."`

- **`(body) name`**
  - **Type:** String
  - **Description:** The new name for the assistant. This name will be used to identify the assistant in the system and should be unique.
  - **Example:** `"Customer Support Assistant"`

- **`(body) description`**
  - **Type:** String
  - **Description:** A brief description of the assistant's purpose or functionality. This helps to clarify the assistant’s role and usage.
  - **Example:** `"This assistant handles customer support inquiries."`

- **`(body) tools`**
  - **Type:** Array of Objects
  - **Description:** A list of tools enabled for the assistant. Tools can be of various types, such as `code_interpreter`, `file_search`, or `function`, enhancing the assistant’s capabilities.
  - **Example:** `[{ "type": "code_interpreter" }, { "type": "file_search" }]`

- **`(body) vector_store_id`**
  - **Type:** String
  - **Description:** The identifier for a vector store that the assistant can utilize. Vector stores are typically used for advanced search functionalities within large datasets.
  - **Example:** `"vectorstore-12345"`

- **`(body) file_ids`**
  - **Type:** Array of Strings
  - **Description:** A list of file identifiers that the assistant can access. This allows the assistant to retrieve and use the content of specified files.
  - **Example:** `["file-123", "file-456"]`

- **`(body) model`**
  - **Type:** String
  - **Description:** The identifier of the model to be used by the assistant. This defines the assistant’s underlying AI model and capabilities.
  - **Example:** `"gpt-4-turbo"`

- **`(body) metadata`**
  - **Type:** Object
  - **Description:** A set of key-value pairs that provide additional information about the assistant in a structured format. Metadata can be useful for tracking and managing assistants.
  - **Example:** `{"category": "support", "version": "v1.2"}`

- **`(body) top_p`**
  - **Type:** Number
  - **Description:** A sampling method that controls the diversity of the assistant's output. Lower values focus on more likely predictions, while higher values allow for more creative responses.
  - **Example:** `0.9`

- **`(body) temperature`**
  - **Type:** Number
  - **Description:** Controls the randomness of the assistant's responses. Lower values make the output more deterministic, while higher values increase variability.
  - **Example:** `0.7`

- **`(body) response_form`**
  - **Type:** String
  - **Description:** Specifies the format of the assistant’s output. The default is `"auto"`, but it can be set to specific formats like `{"type": "json_object"}` to enforce structured outputs.
  - **Example:** `"auto"`

### Delete Assistant

**Description:** This action deletes an existing assistant, permanently removing it from the system. The specified assistant, identified by its unique ID, will no longer be available after this action is completed.

### Parameters

- **`(path) assistant_id`**
  - **Type:** String
  - **Description:** The unique identifier of the assistant you wish to delete. This ID is necessary to locate and remove the correct assistant from the system.
  - **Example:** `"asst_oULbF3tvVtvnEzDIxoO00eJW"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the media type of the resource. This should be set to `"application/json"` to ensure the server processes the request correctly.
  - **Example:** `"application/json"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** The API key or token used for authorization. This header authenticates the request, ensuring that only authorized users can delete the assistant.
  - **Example:** `"Bearer sk-..."`

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** This allows one to specify which version of assistants is being utilized.
  - **Example:** `"assistants=v2"`

### Create Thread

(documentation coming soon)

### Create Thread And Run (Streaming)

(documentation coming soon)

### Create Thread And Run (Non-Streaming)

(documentation coming soon)

### Retrieve Thread

(documentation coming soon)

### Modify Thread

(documentation coming soon)

### Delete Thread

(documentation coming soon)

### Create Message

(documentation coming soon)

### List Messages

(documentation coming soon)

### Retrieve Message

(documentation coming soon)

### Modify Message

(documentation coming soon)

### Delete Message 

(documentation coming soon)

### Create Run (Non-Streaming)

(documentation coming soon)

### Create Run (Streaming)

(documentation coming soon)

### Retrieve Run

(documentation coming soon)

### Submit Tool Outputs To Run

(documentation coming soon)

### Cancel A Run

(documentation coming soon)

### Retrieve Vector Store

(documentation coming soon)

### Modify Vector Store

(documentation coming soon)

### Delete Vector Store

(documentation coming soon)

### Retrieve Vector Store File

(documentation coming soon)

### Retrieve Vector Store File Batch

(documentation coming soon)

### Delete Vector Store File

(documentation coming soon)

### Delete Vector Store File Batch

(documentation coming soon)

### Add Assistant Thread Messages

(documentation coming soon)

## Data Utilities - Web, Files

(documentation coming soon)

### Create Embeddings Of Text (OpenAI)

(documentation coming soon)

### Extract Text From File (V2)

(documentation coming soon)

### Extract Text And Embeddings From File

(documentation coming soon)

### Web Search

**Description:** Performs a search using Google and retrieves results based on the provided query. This action fetches data from search results to be used in further processing.

### Parameters

- **`Query`**
  - **Type:** String
  - **Description:** The search query to use for fetching results from Google.
  - **Example:** `"latest AI news"`

- **`API Key`**
  - **Type:** String
  - **Description:** The API key for the Serper API used to perform the search.
  - **Example:** `"serper-api-key"`

- **`Number of Results`**
  - **Type:** Integer
  - **Description:** The number of search results to retrieve. Maximum is 30.
  - **Example:** `5`

- **`Include Source URL`**
  - **Type:** Boolean
  - **Description:** Specifies whether or not to include the source URL in the results.
  - **Example:** `true`

- **`Custom Plugin URL`** (Optional)
  - **Type:** String
  - **Description:** URL of the custom server hosting the plugin, if applicable.
  - **Example:** `"https://your-custom-server.com"`

### Read Websites


**Description:** Fetches and reads data from specified websites. This action retrieves the content from given URLs to be used in further processing.

### Parameters

- **`URLs`**
  - **Type:** List of Strings
  - **Description:** A list of website URLs to fetch data from.
  - **Example:** `["https://example.com", "https://anotherexample.com"]`

- **`Include Source URL`**
  - **Type:** Boolean
  - **Description:** Specifies whether or not to include the source URL in the retrieved content.
  - **Example:** `true`

- **`Custom Plugin URL`** (Optional)
  - **Type:** String
  - **Description:** URL of the custom server hosting the plugin, if applicable.
  - **Example:** `"https://your-custom-server.com"`


### Vector Similarity Search

(documentation coming soon)

### Extract Text And Embeddings From File

**Description:** Extracts text from various file formats such as PDF, DOC, CSV, and more. The action supports a wide range of file types and allows for the creation of text embeddings for further processing or searching.

### Parameters

- **`File`**
  - **Type:** File
  - **Description:** The file from which to extract text. Should be a "File Uploader's value" or a file saved to your database. Supported file types include .pdf, .doc, .docx, .csv, .xlsx, .ppt, .pptx, .odt, .epub, .tsv, .txt, .html, .json, .xml, .md, .rst, .rtf, .eml, .msg, .jpeg, .png.
  - **Example:** `"path/to/your-file.pdf"`

- **`User OpenAI API Key`** (Optional)
  - **Type:** String
  - **Description:** If your user is providing their own API key, set it here. If you are providing your own key, set it in the plugins tab.
  - **Example:** `"sk-xxxxxx"`

- **`Create Embeddings?`**
  - **Type:** Boolean
  - **Description:** Whether to create embeddings or not. If set to `true`, will return vector embeddings for each chunk. This is useful for later searching through texts to find relevant data. Requires an OpenAI API Key.
  - **Example:** `false`

- **`DataAPI - URL`** (Optional)
  - **Type:** String
  - **Description:** If using the Data API for chunk creation, specify the Data Type URL you want to use to store the returned chunks.
  - **Example:** `"https://your-data-api-url.com"`

- **`Data API - Data Type`** (Optional)
  - **Type:** String
  - **Description:** If using the Data API for chunk creation, specify the Data Type you want to use to store the returned chunks.
  - **Example:** `"ChunkDataType"`

- **`DataAPI - Fallback - Text`** (Optional)
  - **Type:** String
  - **Description:** If using the Data API for chunk creation, manually specify the database field for storing the text component of each chunk. This should be a field of type "text".
  - **Example:** `"Text"`

- **`DataAPI - Fallback - Embedding`** (Optional)
  - **Type:** String
  - **Description:** If you cannot disable the "Use field display instead of ID for key names" setting, specify the field name for storing the embedding component of each chunk.
  - **Example:** `"Embedding"`

- **`DataAPI - Fallback - Page`** (Optional)
  - **Type:** String
  - **Description:** If you cannot disable the "Use field display instead of ID for key names" setting, specify the field name for storing the page number of each chunk.
  - **Example:** `"PageNum"`

- **`Reference ID`** (Optional)
  - **Type:** String
  - **Description:** Specify the ID of the reference you want to link your chunk to, such as a User or Project. Set this field to the unique ID of that object.
  - **Example:** `"user-123"`

- **`Fallback - Reference Field`** (Optional)
  - **Type:** String
  - **Description:** If linking the record to another record and you cannot disable the "Use field display instead of ID for key names" setting, specify the reference field name.
  - **Example:** `"Source"`

- **`Custom Plugin URL`** (Optional)
  - **Type:** String
  - **Description:** If hosting your own plugin server, enter its address here.
  - **Example:** `"https://your-custom-server.com"`

- **`Embedding Model`** (Optional)
  - **Type:** String
  - **Description:** Name of the model to use for creating embeddings. Options include "text-embedding-3-large" (default and most performant), "text-embedding-3-small", and "text-embedding-ada-002".
  - **Example:** `"text-embedding-3-large"`

## Audio

### Start Audio Capture A ChatGPT/LLM Toolkit - Audio Container

(documentation coming soon)

### Stop Audio Capture A ChatGPT/LLM Toolkit - Audio Container

(documentation coming soon)

## Miscellaneous

### Retrieve OpenAI Status

(documentation coming soon)

### Truncate Messages

(documentation coming soon)
