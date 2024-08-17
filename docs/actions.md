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

**Description:** This action allows you to define a function by specifying its name, description, and properties. The function can then be used within a model to perform specific tasks based on the input provided.

### Parameters

- **`Element`**
  - **Type:** Element Selector
  - **Description:** The element in your application where the function is defined, typically related to a data container or a specific element that will use this function.
  - **Example:** `ChatGPTToolkit-DataContainer`

- **`Name`**
  - **Type:** String
  - **Description:** The name of the function to be called. The name must consist of letters (a-z, A-Z), numbers (0-9), underscores (_), or dashes (-), with a maximum length of 64 characters.
  - **Example:** `calculate_total`

- **`Description`**
  - **Type:** Rich Text
  - **Description:** A description of what the function does. This description helps the model determine when and how to call the function.
  - **Example:** `This function calculates the total amount after applying discounts and taxes.`

- **Property Structure:**
  Each property follows the same structure as detailed below. You can define multiple properties (e.g., Property 1, Property 2, Property 3, Property 4, Property 5) with these attributes:

  - **`Property X - Name`**
    - **Type:** String
    - **Description:** The name of the property, which maps to an input argument expected by the function.
    - **Example:** `price`, `discount`, `tax_rate`, `quantity`, `unit`

  - **`Property X - Type`**
    - **Type:** String
    - **Description:** The data type of the property. Valid types include `string`, `number`, `integer`, `object`, `array`, `boolean`, `null`.
    - **Example:** `number`, `string`, `boolean`

  - **`Property X - Description`**
    - **Type:** Rich Text
    - **Description:** A description of the property. This helps the model understand the role of the property in the function call.
    - **Example:** `The original price of the item before applying any discounts.`, `The discount percentage to be applied.`, `The number of items purchased.`

  - **`Property X - Required?`**
    - **Type:** Boolean
    - **Description:** Specifies whether the property is required for the function call. Must be set to either `yes` or `no`.
    - **Example:** `yes`, `no`

### Set Functions

**Description:** This action allows you to set a list of functions to be loaded into a Data Container. The functions must be defined in a specific format and are used by models to perform designated tasks based on input parameters.

### Parameters

- **`Element`**
  - **Type:** Element Selector
  - **Description:** The element in your application where the functions will be loaded, typically a data container or a similar element that requires the use of these functions.
  - **Example:** `ChatGPTToolkit-DataContainer`

- **`Functions (text)`**
  - **Type:** Rich Text
  - **Description:** The raw text of the functions to be loaded into the Data Container. Functions should be formatted as a JSON array, enclosed in square brackets `[]`, with each function separated by a comma. The format must adhere to the specifications outlined in the [OpenAI API documentation](https://platform.openai.com/docs/api-reference/chat/create#chat/create-functions).
  - **Example:** 
    ```json
    [
      {
        "name": "calculate_total",
        "description": "Calculates the total amount after applying discounts and taxes.",
        "parameters": {
          "type": "object",
          "properties": {
            "price": {
              "type": "number",
              "description": "The original price of the item."
            },
            "discount": {
              "type": "number",
              "description": "The discount percentage to apply."
            },
            "tax_rate": {
              "type": "number",
              "description": "The tax rate to apply to the discounted price."
            },
            "quantity": {
              "type": "integer",
              "description": "The number of items purchased."
            }
          },
          "required": ["price", "quantity"]
        }
      },
      {
        "name": "convert_currency",
        "description": "Converts an amount from one currency to another.",
        "parameters": {
          "type": "object",
          "properties": {
            "amount": {
              "type": "number",
              "description": "The amount of money to convert."
            },
            "from_currency": {
              "type": "string",
              "description": "The currency code of the source currency."
            },
            "to_currency": {
              "type": "string",
              "description": "The currency code of the target currency."
            }
          },
          "required": ["amount", "from_currency", "to_currency"]
        }
      }
    ]
    ```

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

**Description:** This action allows you to execute a function call by sending a request to a specified endpoint, using a chosen model and optionally including user-provided API keys and custom headers.

### Parameters

- **`Function Call`**
  - **Type:** Rich Text
  - **Description:** The body of the function call, usually set to the "Data Container's Latest Function Call". This is the JSON representation of the function call including the function name and its parameters.
  - **Example:** 
    ```json
    {
      "name": "calculate_total",
      "arguments": {
        "price": 100,
        "discount": 10,
        "tax_rate": 7,
        "quantity": 2
      }
    }
    ```

- **`Model`**
  - **Type:** String
  - **Description:** Specifies which ChatGPT model to use for executing the function call. Supported options are `"gpt-3.5-turbo"`, `"gpt-4"`, `"gpt-3.5-turbo-16k"`, and `"gpt-4-32k"`. The default is `"gpt-3.5-turbo"`, which is faster and cheaper, while `"gpt-4"` is more powerful but slower and more expensive.
  - **Example:** `gpt-3.5-turbo`

- **`User OpenAI API Key`**
  - **Type:** String (Optional)
  - **Description:** If you want to dynamically provide an API key or allow users to input their own API key, set this value. If the API key remains constant, it can be configured in the plugins tab.
  - **Example:** `sk-XXXXXXX`

- **`Endpoint/API URL`**
  - **Type:** String
  - **Description:** The URL of the endpoint that will handle the function call. This could be the URL of the API you are interacting with, such as `https://api.weather.com`, or the URL of your own server.
  - **Example:** `https://api.yourservice.com/function-call`

- **`Headers`**
  - **Type:** Rich Text
  - **Description:** Include any necessary headers required by the API. These should be formatted as a JSON string, typically including things like authorization tokens and content type.
  - **Example:** 
    ```json
    {
      "Authorization": "Bearer sk-XXXXXXX",
      "Content-Type": "application/json"
    }
    ```

- **`HTTP Method`**
  - **Type:** String
  - **Description:** The HTTP method to use when making the request. Usually, this will be either `"POST"` or `"GET"`, depending on the API endpoint's requirements.
  - **Example:** `POST`

- **`Custom Plugin URL`**
  - **Type:** String (Optional)
  - **Description:** If you are hosting your own plugin server, enter its address here.
  - **Example:** `https://my-plugin-server.com`


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

**Description:** This action initiates a new thread with a specified assistant. It allows you to start a conversation by providing an initial set of messages and resources for the assistant's tools.

### Parameters

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the media type of the request. This should be set to `"application/json"` to ensure that the server processes the request as JSON.
  - **Example:** `"application/json"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** The API key or token used for authorization. This header is essential for authenticating the request, ensuring that only authorized users can start a thread with the assistant.
  - **Example:** `"Bearer sk-..."`

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** This allows one to specify which version of assistants is being utilized.
  - **Example:** `"assistants=v2"`

- **`(body) messages`**
  - **Type:** Array of Objects
  - **Description:** A list of messages that will be used to start the thread. These messages can include system messages, user inputs, or assistant responses to initialize the conversation.
  - **Example:** `[{"role": "system", "content": "You are a helpful assistant."}, {"role": "user", "content": "Tell me a joke."}]`

- **`(body) tool resources`**
  - **Type:** Object
  - **Description:** A set of resources made available to the assistant's tools in this thread. The resources are specific to the type of tool being used. For example, the `code_interpreter` tool requires a list of file IDs, while the `file_search` tool requires a list of vector store IDs.
  - **Example:** `{"code_interpreter": {"file_ids": ["file-abc123"]}, "file_search": {"vector_store_ids": ["vector-xyz789"]}}`

- **`(body) metadata`**
  - **Type:** Object
  - **Description:** A set of up to 16 key-value pairs that can be attached to the thread. This is useful for storing additional information about the thread in a structured format. Each key can be a maximum of 64 characters long, and each value can be up to 512 characters long.
  - **Example:** `{"project_id": "proj_12345", "session_id": "sess_67890"}`

### Create Thread And Run (Streaming)


**Description:** This action initiates a thread with a specified assistant and runs it using provided messages, tools, and configurations (whilst streaming the response).

### Parameters

- **`(path) Assistant ID`**
  - **Type:** String
  - **Description:** The ID of the Assistant you want to use for the run.
  - **Example:** `"asst_oULbF3tvVtvnEzDIxoO00eJW"`

- **`(body) Messages (List)`**
  - **Type:** Array of Strings
  - **Description:** A list of messages provided as text. Note that you can only use this field OR `"Messages (JSON)"`, but not both. If both are set, `"Messages (JSON)"` will take precedence.
  - **Example:** `["Hello, how are you?", "Tell me about AI."]`

- **`(body) Messages (JSON)`**
  - **Type:** JSON Object
  - **Description:** Messages provided as a JSON object. This field takes precedence over `"Messages (List)"` if both are set.
  - **Example:** `{"messages": [{"role": "user", "content": "Tell me a joke."}]}`

- **`(body) Thread Metadata`**
  - **Type:** JSON Object
  - **Description:** Metadata about the thread, formatted as key-value pairs, such as `{"key1": "value1", "key2": "value2"}`. You can attach up to 16 key-value pairs. Each key can be up to 64 characters, and each value can be up to 512 characters.
  - **Example:** `{"session_id": "sess_12345", "project_id": "proj_67890"}`

- **`(body) Run Metadata`**
  - **Type:** JSON Object
  - **Description:** Metadata about the run, formatted as key-value pairs, such as `{"key1": "value1", "key2": "value2"}`. Up to 16 key-value pairs can be attached. Each key can be a maximum of 64 characters, and each value can be a maximum of 512 characters.
  - **Example:** `{"run_id": "run_abc123", "context": "test"}`

- **`(body) Model`**
  - **Type:** String
  - **Description:** The model you would like the Assistant to use for this run.
  - **Example:** `"gpt-3.5-turbo"`

- **`(body) Version (v2 or v1)`**
  - **Type:** String
  - **Description:** Specifies which version of the Assistants API to use. Must be either `"v2"` or `"v1"`. `"v2"` is the current default.
  - **Example:** `"v2"`

- **`(body) Tools`**
  - **Type:** JSON Array
  - **Description:** A JSON array specifying the tools available to the Assistant during the run. For example: `[{"type": "code_interpreter"}, {"type": "retrieval"}]`.
  - **Example:** `[{"type": "code_interpreter"}, {"type": "file_search"}]`

- **`(body) Instructions`**
  - **Type:** String
  - **Description:** Override the Assistant's default instructions by providing specific instructions here.
  - **Example:** `"Always provide detailed explanations."`

- **`(body) Custom Body`**
  - **Type:** JSON Object
  - **Description:** If you'd like to provide your own request payload as JSON, you can do so here. This will override most of the properties above.
  - **Example:** `{"custom": "value"}`

- **`(body) User OpenAI API Key`**
  - **Type:** String
  - **Description:** If your user is providing their own API key, enter it here. Otherwise, you may create a Security Token and use that.
  - **Example:** `"sk-..."`

- **`(body) Security Token`**
  - **Type:** String
  - **Description:** If you are using your own API key and want to protect it from users, first create a security token using the action `"Create Security Token"`. Then provide that token here instead of your API key.
  - **Example:** `"token_abc123"`

### Create Thread And Run (Non-Streaming)

**Description:** This action creates a thread for a specified assistant and runs it (non-streaming)

### Parameters

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** The content type of the request. This should be set to `"application/json"`.
  - **Example:** `"application/json"`

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** The version of the OpenAI Assistants API to use. This should be set to `"assistants=v2"`.
  - **Example:** `"assistants=v2"`

- **`(body) Assistant ID`**
  - **Type:** String
  - **Description:** The ID of the assistant to use for this run.
  - **Example:** `"asst_OSRwVyQ3frGKa3OJN"`

- **`(body) Model`**
  - **Type:** String
  - **Description:** The ID of the model to be used for this run. If provided, this will override the model associated with the assistant. If not provided, the model associated with the assistant will be used.
  - **Example:** `"gpt-4-turbo"`

- **`(body) Instructions`**
  - **Type:** String
  - **Description:** Overrides the default instructions of the assistant. This is useful for modifying the behavior on a per-run basis.
  - **Example:** `"Provide a detailed summary of the input text."`

- **`(body) Tools`**
  - **Type:** JSON Array
  - **Description:** Overrides the tools the assistant can use for this run. Useful for customizing the assistant's capabilities for specific tasks.
  - **Example:** `[{"type": "code_interpreter"}, {"type": "file_search"}]`

- **`(body) Metadata`**
  - **Type:** JSON Object
  - **Description:** A set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format. Keys can be a maximum of 64 characters long and values can be a maximum of 512 characters long.
  - **Example:** `{"session_id": "sess_12345", "context": "test"}`

- **`(body) Temperature`**
  - **Type:** Float
  - **Description:** The sampling temperature to use, between 0 and 2. Higher values will make the output more random, while lower values will make it more focused and deterministic.
  - **Example:** `0.7`

- **`(body) Top_p`**
  - **Type:** Float
  - **Description:** An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. For example, `0.1` means only the tokens comprising the top 10% probability mass are considered.
  - **Example:** `0.9`

- **`(body) Max Prompt Tokens`**
  - **Type:** Integer
  - **Description:** Controls the maximum number of tokens to be used for the prompt. This helps in managing the initial context window of the run.
  - **Example:** `4096`

- **`(body) Max Completion Tokens`**
  - **Type:** Integer
  - **Description:** The maximum number of tokens allowed for the completion generated by the model.
  - **Example:** `512`

- **`(body) Truncation Strategy`**
  - **Type:** String
  - **Description:** Controls how a thread will be truncated prior to the run. This is useful for managing the context window and ensuring that relevant information is retained.
  - **Example:** `"truncate_to_max_context"`

- **`(body) Response Form`**
  - **Type:** JSON Object
  - **Description:** Specifies the format that the model must output. Setting to `{"type": "json_object"}` enables JSON mode, which guarantees that the message the model generates is valid JSON.
  - **Example:** `{"type": "json_object"}`

- **`(body) Tool Choice`**
  - **Type:** JSON Object
  - **Description:** Controls which (if any) tool is called by the model. Options include `"none"` (no tools called), `"auto"` (default, allows the model to choose), and specific tools like `{"type": "file_search"}`.
  - **Example:** `{"type": "code_interpreter"}`

- **`(body) Tool Resources`**
  - **Type:** JSON Object
  - **Description:** A set of resources that are used by the assistant's tools. The resources are specific to the type of tool. For example, the code_interpreter tool requires a list of file IDs, while the file_search tool requires a list of vector store IDs.
  - **Example:** `{"file_ids": ["file-123", "file-456"]}

### Retrieve Thread

**Description:** This action retrieves a specific thread by using it's ID, using the specified assistant's API.

### Parameters

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread to retrieve.
  - **Example:** `"thread_Kejsk1txfpFfcbI6Um501qd6"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** The content type of the request. This should be set to `"application/json"`.
  - **Example:** `"application/json"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** The API key or token used to authorize the request. Typically passed as a Bearer token.
  - **Example:** `"Bearer YOUR_API_KEY"`

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** The version of the OpenAI Assistants API to use. This should be set to `"assistants=v2"`.
  - **Example:** `"assistants=v2"`

### Modify Thread

**Description:** This action modifies a specific thread by its ID, allowing updates to the tools and metadata associated with the thread.

### Parameters

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread to modify.
  - **Example:** `"thread_Kejsk1txfpFfcbI6Um501qd6"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants version.
  - **Example:** `"assistants=v2"`

- **`(body) Tool Resources`**
  - **Type:** JSON Object
  - **Description:** A set of resources that are made available to the assistant's tools in this thread. The resources are specific to the type of tool. For example, the `code_interpreter` tool requires a list of file IDs, while the `file_search` tool requires a list of vector store IDs.
  - **Example:** `{"file_ids": ["file_ABC123", "file_DEF456"]}`

- **`(body) Metadata`**
  - **Type:** JSON Object
  - **Description:** Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format. Keys can be a maximum of 64 characters long and values can be a maximum of 512 characters long.
  - **Example:** `{"key1": "value1", "key2": "value2"}`


### Delete Thread

**Description:** This action deletes a specific thread by its ID, using the specified assistant's API.

### Parameters

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread to delete.
  - **Example:** `"thread_aCw6WwYNAS1V7umohsZWw9m"`

### Create Message

**Description:** This action creates a message within a specific thread by its ID, including the role, content, and optional attachments or metadata.

### Parameters

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread where the message will be created.
  - **Example:** `"thread_MV1AfPOZriOqNwcVKTdjMZpS"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants version.
  - **Example:** `"assistants=v2"`

- **`(body) Role`**
  - **Type:** String
  - **Description:** Specifies the role of the message sender. Common roles include `"user"`, `"assistant"`, and `"system"`.
  - **Example:** `"user"`

- **`(body) Content`**
  - **Type:** String or Array
  - **Description:** The content of the message. For text, the content must be enclosed in quotes, e.g., `"hello"`. For arrays, the content can include a mix of text and images, with images being supported on Vision-compatible models.
  - **Example:** `"How does AI work? Explain it in simple terms."`

- **`(body) Attachments`**
  - **Type:** Array
  - **Description:** A list of files attached to the message, specifying which tools these attachments should be added to.
  - **Example:** `[{ "file_id": "file_ABC123", "tool": "code_interpreter" }]`

- **`(body) Metadata`**
  - **Type:** JSON Object
  - **Description:** Set of 16 key-value pairs that can be attached to the message. This can be useful for storing additional information about the message in a structured format. Keys can be a maximum of 64 characters long, and values can be a maximum of 512 characters long.
  - **Example:** `{"key1": "value1", "key2": "value2"}`

### List Messages

**Description:** This action retrieves a list of messages from a specified thread, allowing for filtering and ordering of the results based on various parameters.

### Parameters

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread from which messages will be retrieved.
  - **Example:** `"thread_pGkCyBUoF9WfwG3g7bY1cSN3"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants version
  - **Example:** `"assistants=v2"`

- **`(param) Limit`**
  - **Type:** Integer
  - **Description:** The maximum number of messages to retrieve.
  - **Example:** `"100"`

- **`(param) Order`**
  - **Type:** String
  - **Description:** The order in which to retrieve the messages, either `"asc"` for ascending or `"desc"` for descending.
  - **Example:** `"desc"`

- **`(param) After`**
  - **Type:** String (Timestamp)
  - **Description:** Retrieves messages sent after the specified timestamp.
  - **Example:** `"2024-08-16T12:00:00Z"`

- **`(param) Before`**
  - **Type:** String (Timestamp)
  - **Description:** Retrieves messages sent before the specified timestamp.
  - **Example:** `"2024-08-16T14:00:00Z"`

- **`(param) Run ID`**
  - **Type:** String
  - **Description:** Filters messages by the specific run ID within the thread.
  - **Example:** `"run_aBcD1234EfGh"`

### Retrieve Message

**Description:** This action retrieves a specific message from a thread using the message's unique identifier.

### Parameters

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread from which the message will be retrieved.
  - **Example:** `"thread_MV1AfPOZriOqNwcVKTdjMZpS"`

- **`(path) Message ID`**
  - **Type:** String
  - **Description:** The unique identifier of the message to retrieve.
  - **Example:** `"msg_HuE7P6AYzHxkiZKqPzAaLIhv"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants version
  - **Example:** `"assistants=v2"`

### Modify Message

**Description:** This action modifies a specific message in a thread using the message's unique identifier.

### Parameters

- **`(path) Message ID`**
  - **Type:** String
  - **Description:** The unique identifier of the message to modify.
  - **Example:** `"msg_HuE7P6AYzHxkiZKqPzAaLIhv"`

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread containing the message.
  - **Example:** `"thread_MV1AfPOZriOqNwcVKTdjMZpS"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants version
  - **Example:** `"assistants=v2"`

- **`(body) Metadata`**
  - **Type:** Object
  - **Description:** A set of 16 key-value pairs that can be attached to the message. This is useful for storing additional information in a structured format. Keys can be a maximum of 64 characters long and values can be a maximum of 512 characters long.


### Delete Message 

**Description:** This action deletes a specific message in a thread using the message's unique identifier.

### Parameters

- **`(path) Message ID`**
  - **Type:** String
  - **Description:** The unique identifier of the message to delete.
  - **Example:** `"msg_HuE7P6AYzHxkiZKqPzAaLlhv"`

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread containing the message.
  - **Example:** `"thread_MV1AfPOZriOqNwcVKTdjMZpS"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants version
  - **Example:** `"assistants=v2"`

### Create Run (Non-Streaming)

**Description:** This action creates a run for a specified thread (non-streaming).

### Parameters

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread to run.
  - **Example:** `"thread_MV1AfPOZriOqNwcVKTdjMZpS"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the API version and other headers relevant to the OpenAI Beta.

- **`(body) Assistant ID`**
  - **Type:** String
  - **Description:** The ID of the assistant to use to execute this run.
  - **Example:** `"asst_OSRwVyQ3frGKa|30JNPjMmPJ"`

- **`(body) Model`**
  - **Type:** String
  - **Description:** The ID of the Model to be used to execute this run. If provided, it overrides the model associated with the assistant. If not provided, the model associated with the assistant will be used.

- **`(body) Instructions`**
  - **Type:** String
  - **Description:** Overrides the instructions of the assistant. Useful for modifying behavior on a per-run basis.

- **`(body) Tools`**
  - **Type:** Array
  - **Description:** Overrides the tools the assistant can use for this run. Useful for modifying behavior on a per-run basis.

- **`(body) Additional Instructions`**
  - **Type:** String
  - **Description:** Appends additional instructions at the end of the instructions for the run. Useful for modifying behavior without overriding other instructions.

- **`(body) Metadata`**
  - **Type:** JSON Object
  - **Description:** A set of key-value pairs that can be attached to the run. Useful for storing additional information in a structured format.

- **`(body) Temperature`**
  - **Type:** Number
  - **Description:** Controls the randomness of the model's responses. Higher values mean more random outputs.

- **`(body) Top P`**
  - **Type:** Number
  - **Description:** Controls the diversity of the model’s responses by sampling from the top tokens.

- **`(body) Max Prompt Tokens`**
  - **Type:** Integer
  - **Description:** The maximum number of tokens in the prompt.

- **`(body) Max Completion Tokens`**
  - **Type:** Integer
  - **Description:** The maximum number of tokens in the completion.

- **`(body) Truncation Strategy`**
  - **Type:** String
  - **Description:** Controls how the thread will be truncated prior to the run. This affects the initial context window of the run.

- **`(body) Additional Messages`**
  - **Type:** Array
  - **Description:** Adds additional messages to the thread before creating the run.

- **`(body) Response Format`**
  - **Type:** JSON Object
  - **Description:** Specifies the format that the model must output. Compatible with GPT-4 and GPT-3.5 models. Setting to `{ "type": "json_object" }` enables JSON mode, ensuring the message generated is valid JSON. When using JSON mode, you must also instruct the model to produce JSON via a system or user message to avoid unending streams of whitespace.

- **`(body) Tool Choice`**
  - **Type:** String
  - **Description:** Controls which tool, if any, is called by the model. `none` means the model generates a message without calling any tools. `auto` allows the model to choose between generating a message or calling tools. `required` means the model must call one or more tools. Specifying a tool directly forces the model to call that tool.


### Create Run (Streaming)

**Description:** This action creates a run with streaming for a specified thread.

### Parameters


- **`Element`**
  - **Type:** Element
  - **Description:** The AssistantContainer for which the run should be conducted

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread you want to use for the run.
  - **Example:** `"thread_MV1AfPOZriOqNwcVKTdjMZpS"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the API version and other headers relevant to the OpenAI Beta.

- **`(body) Assistant ID`**
  - **Type:** String
  - **Description:** The ID of the Assistant you want to use for the run.
  - **Example:** `"asst_OSRwVyQ3frGKa|30JNPjMmPJ"`

- **`(body) Model`**
  - **Type:** String
  - **Description:** Override the default model for the Assistant.
  - **Example:** `"gpt-4-turbo"`

- **`(body) Version`**
  - **Type:** String
  - **Description:** Which version of the Assistants API to use. Must be either `"v2"` or `"v1"`. `"v2"` is the current default.
  - **Example:** `"v2"`

- **`(body) Instructions`**
  - **Type:** String
  - **Description:** Overrides the instructions of the assistant. Useful for modifying the behavior on a per-run basis.
  - **Example:** `"Provide a detailed explanation of the topic."`

- **`(body) Tools`**
  - **Type:** Array
  - **Description:** Override the tools the assistant can use for this run. Useful for modifying the behavior on a per-run basis.
  - **Example:** `["tool1", "tool2"]`

- **`(body) Run Metadata`**
  - **Type:** JSON Object
  - **Description:** Metadata about the run, formatted as key-value pairs, like `{"key1": "value1", "key2": "value2"}`. Useful for storing additional information about the run in a structured format. Keys can be a maximum of 64 characters long and values can be a maximum of 512 characters long.
  - **Example:** `{"context": "example run", "priority": "high"}`

- **`(body) Custom Body`**
  - **Type:** JSON Object
  - **Description:** If you'd like to provide your own request payload as JSON, you can do it here. This will override most of the properties above.

- **`(body) User OpenAI API Key`**
  - **Type:** String
  - **Description:** If your user is providing their own API key, enter it here. If you are providing your own API key, you will want to create a Security Token using the action `"Create Security Token"`.

- **`(body) Security Token`**
  - **Type:** String
  - **Description:** If you are using your own API key and want to protect it from users, first create a security token using the action `"Create Security Token"`. Provide that here instead of your API key.
  - **Example:** `"security_token_example"`


### Retrieve Run

**Description:** This action retrieves details of a specific run within a thread using the run's unique identifier.

### Parameters

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread that was run.
  - **Example:** `"thread_mtzLulifswZGCOdfn0gXHHx"`

- **`(path) Run ID`**
  - **Type:** String
  - **Description:** The ID of the run to retrieve.
  - **Example:** `"run_Kj1h06UXVis6RJEM3W1BVUOR"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** Override the Authorization header set in the plugin tab.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants API version.
  - **Example:** `"assistants=v2"`

### Submit Tool Outputs To Run

**Description:** This action submits the outputs of tools used in a specific run within a thread.

### Parameters

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread to which this run belongs.
  - **Example:** `"thread_MV1AfPOZriOqNwcVKTdiMZpS"`

- **`(path) Run ID`**
  - **Type:** String
  - **Description:** The ID of the run that requires the tool output submission.
  - **Example:** `"run_8|cR2UArOaAKOnBhWiumejRq"`

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants API version.
  - **Example:** `"assistants=v2"`

- **`(body) Tool Outputs`**
  - **Type:** JSON Array
  - **Description:** A list of tools for which the outputs are being submitted. Each entry includes the tool call ID and the output.
  - **Example:**
    ```json
    [
      {
        "tool_call_id": "call_001",
        "output": "70 degrees and sunny."
      }
    ]
    ```
### Cancel A Run

**Description:** This action cancels a specific run within a thread using the run's unique identifier.

### Parameters

- **`(path) Thread ID`**
  - **Type:** String
  - **Description:** The ID of the thread to which this run belongs.
  - **Example:** `"thread_cwx6UirqzGInZeVChY7UBlo"`

- **`(path) Run ID`**
  - **Type:** String
  - **Description:** The ID of the run to cancel.
  - **Example:** `"run_W3YXVAEZV6pMc8E/Otoes9wl"`

### Retrieve Vector Store

**Description:** This action retrieves details of a specific vector storage using its unique identifier.

### Parameters

- **`(path) Vector Store ID`**
  - **Type:** String
  - **Description:** The ID of the vector storage to retrieve.
  - **Example:** `"vs_7cUgi46PXsEZWRM67mwdR8r"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** Authorization header to access the resource.

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants API version.
  - **Example:** `"assistants=v2"`

### Modify Vector Store

**Description:** This action modifies the details of a specific vector storage using its unique identifier.

### Parameters

- **`(path) Vector Store ID`**
  - **Type:** String
  - **Description:** The ID of the vector storage to modify.
  - **Example:** `"vs_7cUgi46PXsEZWVRM67mwdR8r"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** Authorization header to access the resource.

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the API version and other headers relevant to the OpenAI Beta.
  - **Example:** `"assistants=v2"`

- **`(body) Name`**
  - **Type:** String
  - **Description:** The name of the vector store.
  - **Example:** `"test"`

- **`(body) Expires After`**
  - **Type:** JSON Object
  - **Description:** The expiration policy for a vector store. See here for more: [Expiration Policy Documentation](https://platform.openai.com/docs/api-reference/vector-stores/modify).
  - **Example:** 
    ```json
    {
      "anchor": "last_active_at",
      "days": 7
    }
    ```

- **`(body) Metadata`**
  - **Type:** JSON Object
  - **Description:** Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format. Keys can be a maximum of 64 characters long and values can be a maximum of 512 characters long.
  - **Example:** 
    ```json
    {
      "description": "Vector store for customer data",
      "created_by": "user123",
      "department": "sales",
      "last_updated": "2024-08-15T12:34:56Z",
      "version": "v1.0",
      "tags": ["customer", "sales", "data"]
    }
    ```

### Delete Vector Store

**Description:** This action deletes a specific vector storage using its unique identifier.

### Parameters

- **`(path) Vector Store ID`**
  - **Type:** String
  - **Description:** The ID of the vector storage to delete.
  - **Example:** `"vs_7cUgi46PXsEZWRM67mwdR8r"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** Authorization header to access the resource.

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants API version.
  - **Example:** `"assistants=v2"`

### Retrieve Vector Store File

**Description:** This action retrieves a specific file from a vector store using its unique identifiers.

### Parameters

- **`(path) Vector Store ID`**
  - **Type:** String
  - **Description:** The ID of the vector store that the file belongs to.
  - **Example:** `"vS_2E1|nsF9nAaPLQjiUBOsOqVF"`

- **`(path) File ID`**
  - **Type:** String
  - **Description:** The ID of the file being retrieved.
  - **Example:** `"file-MqxLjHeey1R05WYdNuUZRJnR"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** Authorization header to access the resource.

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants API version.
  - **Example:** `"assistants=v2"`



### Retrieve Vector Store File Batch

**Description:** This action retrieves a specific batch of files from a vector store using their unique identifiers.

### Parameters

- **`(path) Vector Store ID`**
  - **Type:** String
  - **Description:** The ID of the vector store that the file batch belongs to.
  - **Example:** `"vS_2E1|nsF9nAaPLQjiUBOsOqVF"`

- **`(path) Batch ID`**
  - **Type:** String
  - **Description:** The ID of the file batch being retrieved.
  - **Example:** `"vsfb_557015d986d4aca8393c7e7458c8a5b"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** Authorization header to access the resource.

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants API version.
  - **Example:** `"assistants=v2"`

### Delete Vector Store File

**Description:** This action deletes a specific file from a vector store using its unique identifiers.

### Parameters

- **`(path) Vector Store ID`**
  - **Type:** String
  - **Description:** The ID of the vector store that the file belongs to.
  - **Example:** `"vs_2E1/nsF9nAaPLQjiUBOSOqVF"`

- **`(path) File ID`**
  - **Type:** String
  - **Description:** The ID of the file being deleted.
  - **Example:** `"file-MqxLjHeey1R05WYdNuUZRJnR"`

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** Authorization header to access the resource.

- **`(header) Content-Type`**
  - **Type:** String
  - **Description:** Specifies the content type of the request. Should be set to `"application/json"`.

- **`(header) OpenAI-Beta`**
  - **Type:** String
  - **Description:** Specifies the assistants API version.
  - **Example:** `"assistants=v2"`

### Delete Vector Store File Batch

(documentation coming soon)

### Load Assistant Thread Messages

**Description:** This action loads messages into an assistant thread. You can provide messages as JSON objects or as a list of texts, and specify the order in which they should be processed.

### Parameters

- **`Element`**
  - **Type:** Element
  - **Description:** The specified front-end AssistantsContainer
  - **Example:** `"ChatGPTToolkit-AssistantsContainer A."`
    
- **`Messages (as JSON)`**
  - **Type:** JSON Object
  - **Description:** Use this field to load a list of messages as a JSON object. Must use EITHER this or the `messages_list` field, but not both.
  - **Example:** `[{"role": "user", "content": "What is the weather like?"}, {"role": "assistant", "content": "It's sunny and warm."}]`

- **`Messages (as list)`**
  - **Type:** List of Texts
  - **Description:** Use this field to load a list of messages as a list of texts. Must use EITHER this or the `messages_json` field, but not both.
  - **Example:** `["What is the weather like?", "It's sunny and warm."]`

- **`Newest First? (sort)`**
  - **Type:** String
  - **Description:** By default, the OpenAI API will return the newest messages first. If you're feeding messages in with the OLDEST message first, set this to `"no"`. Defaults to `"yes"`.
  - **Example:** `"yes"`

## Data Utilities - Web, Files

### Create Embeddings Of Text (OpenAI)

**Description:** This action creates embeddings from the provided text input using a specified model and encoding format.

### Parameters

- **`(header) Authorization`**
  - **Type:** String
  - **Description:** The authorization header for accessing the API. Should be in the format `Bearer YOUR_API_KEY`.
  - **Example:** `"Bearer sk-proj-RGouO8sgCOYg53c6PBrI3BIbkFJApTjoJEapO7ueqR6nAIH"`

- **`(body) Input`**
  - **Type:** String or Array of Strings
  - **Description:** Input text to embed, encoded as a string or array of tokens. If passing a single string, you MUST wrap it in double quotes, e.g., `"Hello"`. To embed multiple inputs, pass an array of strings or token arrays. The input must not exceed the max input tokens for the model (8192 tokens for `text-embedding-ada-002`), cannot be an empty string, and any array must be 2048 dimensions or less.
  - **Example:** `"Hello"`

- **`(body) Model`**
  - **Type:** String
  - **Description:** Name of the model to use. Options include: `"text-embedding-3-large"` (default and most performant), `"text-embedding-3-small"`, and `"text-embedding-ada-002"`. For more information, see: [OpenAI Models](https://platform.openai.com/docs/models/embeddings).
  - **Example:** `"text-embedding-3-large"`

- **`(body) Encoding`**
  - **Type:** String
  - **Description:** The format to return the embeddings in. Can be either `"float"` or `"base64"`.
  - **Example:** `"float"`

### Extract Text From File (V2)

**Description:** This action extracts text from a specified file using the given URL.

### Parameters

- **`(path) base_url`**
  - **Type:** String
  - **Description:** The URL to use for the request. If you are using your own server, put its domain name here, e.g., `toolkit.mydomain.com`. Otherwise, leave this as `v6.chatgpt.launchable.ai`. DO NOT include "https://" at the start of the domain, as this will be added automatically.
  - **Example:** `v6.chatgpt.launchable.ai`

- **`(param.) file_url`**
  - **Type:** String
  - **Description:** The file from which to extract text. Should be a "File Uploader's value" or a file saved to your database. Supported file types include: pdf, doc, docx, csv, xlsx, ppt, pptx, odt, epub, tsv, txt, html, json, xml, md, rst, rtf, eml, msg, jpeg, png.
  - **Example:** `https://arxiv.org/pdf/1706.03762`

- **`(param.) embedding`**
  - **Type:** String
  - **Description:** The embedding model to use for extracting text. 
  - **Example:** `text-embedding-3-large`

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

**Description:** This action performs a vector similarity search to find relevant context based on input text.

### Parameters

- **`Input Text`**
  - **Type:** Rich text editor
  - **Description:** The text for which you want to find relevant context using vector similarity search. For example, if a user wants a specific piece of information from a long document, you can use this input text (e.g., from an input field) and match it against embeddings from previously extracted chunks.
  - **Example:** `"What is the main theme of the book?"`

- **`User OpenAI API Key`**
  - **Type:** String
  - **Description:** If your user is providing their own OpenAI API key, set it here. If you are providing your own key, set it in the plugin tab, and leave this blank.
  - **Example:** `sk-proj-RGouO8sgCOYg53c6PBrI3BIbkFJApTjoJEapO7ueqR6nAIH`

- **`Num Results`**
  - **Type:** Number
  - **Description:** How many results to return. This function returns the top N matches. If set to 10, you will get the top 10 most relevant matches to your input text.
  - **Example:** `5`

- **`Data API URL`**
  - **Type:** String
  - **Description:** The URL of your app's Data API. You can find this in the Settings -> API section of your app. It will look something like this: `https://your-app-name/version-test/api/1.1/obj`.
  - **Example:** `https://your-app-name/version-test/api/1.1/obj`

- **`Chunk Data Type`**
  - **Type:** String
  - **Description:** The Data Type you've created for Chunks. This should be set up in your Data tab and include at least 2 text fields for Text and Embedding. 
  - **Example:** `text_chunks`

- **`Chunk Unique IDs`**
  - **Type:** List
  - **Description:** The unique IDs of up to 500 items in your database that you want to search against. If the expression returns more than 500 items, this action may fail. Your expression should look like: `(Search for Chunks :items until 500) :each item's unique ID`.
  - **Example:** `[item1_id, item2_id, item3_id]`

- **`Constraint - Type`**
  - **Type:** String
  - **Description:** Filter your Chunk types based on a constraint. Constraints include options such as "equals", "not equals", "is in", etc. More details about constraints can be found [here](https://manual.bubble.io/core-resources/api/the-bubble-api/the-data-api/data-api-requests#constraint-types).
  - **Example:** `equals`

- **`Constraint - Value`**
  - **Type:** String
  - **Description:** The value to match Chunks against based on the specified constraint. For example, to match against user emails, set this field to "Current User's email". For tags, set it to a text value like "Science" or "Education".
  - **Example:** `"Current User's email"`

- **`Custom Plugin URL`**
  - **Type:** String
  - **Description:** If hosting your own plugin server, enter its address here.
  - **Example:** `https://custom-plugin.example.com`

- **`Embedding Model`**
  - **Type:** String
  - **Description:** The name of the OpenAI model to use for embedding the text. Options include: "text-embedding-3-large" (default and most performant), "text-embedding-3-small", and "text-embedding-ada-002".
  - **Example:** `text-embedding-3-large`

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

**Description:** This action performs a vector similarity search to find relevant context based on input text.

### Parameters

- **`Element`**
  - **Type:** String
  - **Description:** The ID or identifier of the element where the action is being performed.
  - **Example:** `LLMToolkit-AudioConta...`

- **`Input Text`**
  - **Type:** Rich text editor
  - **Description:** The text for which you want to find relevant context using vector similarity search. For example, if a user wants a specific piece of information from a long document, you can use this input text (e.g., from an input field) and match it against embeddings from previously extracted chunks.
  - **Example:** `"What is the main theme of the book?"`

- **`User OpenAI API Key`**
  - **Type:** String
  - **Description:** If your user is providing their own OpenAI API key, set it here. If you are providing your own key, set it in the plugin tab, and leave this blank.
  - **Example:** `sk-proj-RGouO8sgCOYg53c6PBrI3BIbkFJApTjoJEapO7ueqR6nAIH`

- **`Num Results`**
  - **Type:** Number
  - **Description:** How many results to return. This function returns the top N matches. If set to 10, you will get the top 10 most relevant matches to your input text.
  - **Example:** `5`

- **`Data API URL`**
  - **Type:** String
  - **Description:** The URL of your app's Data API. You can find this in the Settings -> API section of your app. It will look something like this: `https://your-app-name/version-test/api/1.1/obj`.
  - **Example:** `https://your-app-name/version-test/api/1.1/obj`

- **`Chunk Data Type`**
  - **Type:** String
  - **Description:** The Data Type you've created for Chunks. This should be set up in your Data tab and include at least 2 text fields for Text and Embedding. 
  - **Example:** `text_chunks`

- **`Chunk Unique IDs`**
  - **Type:** List
  - **Description:** The unique IDs of up to 500 items in your database that you want to search against. If the expression returns more than 500 items, this action may fail. Your expression should look like: `(Search for Chunks :items until 500) :each item's unique ID`.
  - **Example:** `[item1_id, item2_id, item3_id]`

- **`Constraint - Type`**
  - **Type:** String
  - **Description:** Filter your Chunk types based on a constraint. Constraints include options such as "equals", "not equals", "is in", etc. More details about constraints can be found [here](https://manual.bubble.io/core-resources/api/the-bubble-api/the-data-api/data-api-requests#constraint-types).
  - **Example:** `equals`

- **`Constraint - Value`**
  - **Type:** String
  - **Description:** The value to match Chunks against based on the specified constraint. For example, to match against user emails, set this field to "Current User's email". For tags, set it to a text value like "Science" or "Education".
  - **Example:** `"Current User's email"`

- **`Custom Plugin URL`**
  - **Type:** String
  - **Description:** If hosting your own plugin server, enter its address here.
  - **Example:** `https://custom-plugin.example.com`

- **`Embedding Model`**
  - **Type:** String
  - **Description:** The name of the OpenAI model to use for embedding the text. Options include: "text-embedding-3-large" (default and most performant), "text-embedding-3-small", and "text-embedding-ada-002".
  - **Example:** `text-embedding-3-large`

### Stop Audio Capture A ChatGPT/LLM Toolkit - Audio Container

**Description:** This action stops the audio capture process for a specified audio container.

### Parameters

- **`Element`**
  - **Type:** String
  - **Description:** The ID or identifier of the element where the action is being performed.
  - **Example:** `LLMToolkit-AudioContainerA`

## Miscellaneous

### Retrieve OpenAI Status

**Description:** This action retrieves the current operational status of OpenAI's services. It provides information about the health and availability of various components and endpoints of the OpenAI API.

### Truncate Messages

**Description:** This action truncates a list of messages to fit within a specified token limit or model's input limit.

### Parameters

- **`Messages`**
  - **Type:** String
  - **Description:** Pass a list (array) of messages, each formatted as JSON. For example, you can pass the "Message History" of the Data Container, which will be a list of messages formatted like this: `[{"role": "system", "content": "You are a helpful assistant"}, {"role": "user", "content": "Hello!"}]`. The list must be formatted as a single long string/text, so you may need to format it as ":data source formatted as text", with a comma (,) as separator.
  - **Example:** `[{"role": "system", "content": "You are a helpful assistant"}, {"role": "user", "content": "Hello!"}]`

- **`Model`**
  - **Type:** String (Optional)
  - **Description:** Specify the model you are targeting. If you specify a model here and do not set a value for "Max Tokens", the plugin will attempt to truncate messages to the model's input limit.
  - **Example:** `text-davinci-003`

- **`Max Tokens`**
  - **Type:** Number
  - **Description:** Set a limit on how many tokens to return. This parameter defines the maximum number of tokens that the output should not exceed.
  - **Example:** `150`

- **`Custom Server URL`**
  - **Type:** String
  - **Description:** If using your own server, enter its URL here. This is optional and is used if you have a custom server setup.
  - **Example:** `https://my-custom-server.com/api`
