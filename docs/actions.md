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

This is one of the most fundamnetal actions contained within the toolkit. In which, by using this action one may trigger a response from an AI model (ChatGPT or one of the many OpenRouter models) given a specific prompt. This action has a multitude of parameters one may configure. 






### Chat Completion (Non-Streaming) - V2

(documentation coming soon)

### Clear Message History

(documentation coming soon)

### Clear Current Message

(documentation coming soon)

### Set System Message

(documentation coming soon)

### Add Function

(documentation coming soon)

### Set Functions

(documentation coming soon)

### Set Parameters

(documentation coming soon)

### Stop Streaming

(documentation coming soon)

### Execute Function Call

(documentation coming soon)


## Assistants (OpenAI)

### List Assistants

(documentation coming soon)

### Create Assistant

(documentation coming soon)

### Upload File

(documentation coming soon)

### Retrieve File

(documentation coming soon)

### Delete File

(documentation coming soon)

### Retrieve File Content

(documentation coming soon)

### Modify Assistant

(documentation coming soon)

### Delete Assistant

(documentation coming soon)

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

(documentation coming soon)

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
