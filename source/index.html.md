---
title: API Reference

language_tabs:
  - javascript
  - shell
---
# Text Generation Endpoint
#### **HTTP Method**: `POST`

>### **Sample Request**

```javascript
const fetch = require('node-fetch');

const body = {
  prompt: "Describe the future of technology.",
  title: "The Dawn of a New Technological Era",
  temperature: 0.5,
  frequency_penalty: 0,
  presence_penalty: 0
};

fetch('domain.com/v1/generate', {
  method: 'POST',
  headers: {
    'Authorization': 'YOUR_AUTH_TOKEN',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(body)
})
.then(response => response.json())
.then(data => console.log(data));
```

```shell
curl -X POST "domain.com/v1/generate" \
     -H "Authorization: YOUR_AUTH_TOKEN" \
     -H "Content-Type: application/json" \
     -d '{
           "prompt": "Describe the future of technology.",
           "title": "The Dawn of a New Technological Era",
           "temperature": 0.5,
           "frequency_penalty": 0,
           "presence_penalty": 0
         }'
```

>### **Example Response**

>The response will contain a message with the generated text.

```json
{
  "message": "The future of technology is bright..."
}
```

## Generate Text using OpenAI's Model

Use this endpoint to pass in specific prompts and retrieve generated text from OpenAI's model. This can be particularly useful for generating creative content, completing texts, or generating various versions of a text based on a theme.

### HTTP Request


POST https://ylpllmtfjfrxkrpojixz.supabase.co/functions/v1/generate


### Headers

- Authorization: Your authorization token
- Content-Type: application/json

### Request Body

The following fields can be included in the request body:

Field | Type | Description
----- | ---- | -----------
`prompt_id` | Integer | An optional ID that corresponds to a saved prompt in the database. If provided, this takes precedence over the `prompt` field.
`prompt` | String | The prompt text you want to generate from. Only required if `prompt_id` is not provided.
`context` | String (Optional) | Additional context for the prompt.
`title` | String (Optional) | Title for the text to be generated.
`outline` | String (Optional) | An outline structure you want the generated text to follow.
`selected_text` | String (Optional) | A specific section of the text that you want to emphasize or build upon.
`temperature` | Number (Optional) | The randomness of the output. A higher value makes the output more random. Default is `0.5`.
`frequency_penalty` | Number (Optional) | Penalty for frequent tokens. Default is `0`.
`presence_penalty` | Number (Optional) | Penalty for new tokens. Default is `0`.
`stream` | Boolean (Optional) | A flag that if set to true, the response from OpenAI will be streamed. Default is `false`.

<aside class="notice">
Ensure you have the necessary authentication tokens and are abiding by rate limits when making requests.
</aside>

### Errors

The API will return specific error messages for various issues, such as:

- Unauthorized requests.
- Missing `prompt` or `prompt_id` fields.
- Invalid or non-existent `prompt_id`.
- Errors retrieving context or other issues with the request.

<aside class="warning">
Always check the error message in the response for specifics on what might have gone wrong with your request.
</aside>
---

# Citation Generator
Generate citations in various styles using provided BibTeX input.

#### **HTTP Method**: `POST`

>### **Example Request**:

```shell
curl -X POST 'https://yourdomain.com/citation' \
     -H 'Authorization: Bearer your_token' \
     -H 'Content-Type: application/json' \
     -d '{
           "bibtexs": "@article{
            sample2021, 
            title={Sample Title}, 
            author={Author Name}, 
            journal={Sample Journal}, 
            year={2021}
            }",
           "styles": ["apa", "modern-language-assosiation"]
         }'
```

>### **Example Response**:

```json
[
  {
    "name": "apa",
    "bibliography": "...",
    "citations": "..."
  },
  {
    "name": "mla",
    "bibliography": "...",
    "citations": "..."
  }
]
```

#### **Headers**:

- **X-Service-Key**: Service key for administrative access (Optional, if not using `Authorization` header).
- **Authorization**: Auth token for user-level access.

#### **Request Payload**:

| Parameter | Type                             | Description                                      | Required |
| --------- | -------------------------------- | ------------------------------------------------ | -------- |
| `bibtexs` | string or string[]               | BibTeX data for which the citation is generated. | Yes      |
| `styles`  | string or string[]               | Array of citation styles to generate. Should be one of the styles from this repository.           | Yes      |

#### **Response**:

Returns an array of objects, each containing:

| Field         | Type   | Description                                      |
| ------------- | ------ | ------------------------------------------------ |
| `name`        | string | The citation style used.                         |
| `bibliography`| string | The generated bibliography in the chosen style.  |
| `citations`   | string | The generated citations in the chosen style.     |

#### **Errors**:

- **400**: Missing bibtexs or styles in the request.
- **401**: Unauthorized.



---
