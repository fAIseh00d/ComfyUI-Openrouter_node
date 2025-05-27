# ComfyUI OpenRouter Node

A custom node for ComfyUI that allows you to interact with OpenRouter's chat/completion API, providing access to a wide range of LLM models including GPT-4, Claude, Llama, Mistral, and more.

![OpenRouter Node Example](https://github.com/gabe-init/ComfyUI-Openrouter_node/blob/main/openrouter_node_example.png?raw=true)

## Features

- Access to all models available on OpenRouter
- Support for multiple image inputs (up to 10 images)
- Dynamic image input visibility - additional inputs appear as you connect images
- PDF support with multiple OCR engine options
- Web search capability with `:online` modifier
- Cheapest provider routing with `:floor` modifier
- Fastest provider routing with `:nitro` modifier
- Detailed statistics on token usage and generation speed
- Real-time OpenRouter account balance display

## Installation

1. Clone this repository into your ComfyUI custom_nodes folder:
```bash
cd ComfyUI/custom_nodes
git clone https://github.com/gabe-init/ComfyUI-Openrouter_node
```

2. Install the required dependencies:
```bash
pip install -r requirements.txt
```

3. Restart ComfyUI

## Usage

The OpenRouter node provides a simple interface to interact with various LLMs through the OpenRouter API.

### Inputs

#### Required Inputs:

- **api_key**: Your OpenRouter API key. You can get one from [OpenRouter](https://openrouter.ai/).
- **system_prompt**: The system prompt that sets the behavior of the LLM.
- **user_message_box**: The user message to send to the LLM.
- **model**: The model to use for generation. The node automatically fetches the list of available models from OpenRouter.
- **web_search**: Enable web search capability by appending `:online` to the model ID. This costs $4 per 1000 queries and automatically uses your openrouter balance.
- **cheapest**: Route to the cheapest provider by appending `:floor` to the model ID (enabled by default).
- **fastest**: Route to the fastest provider by appending `:nitro` to the model ID (disabled by default).
- **temperature**: Controls the randomness of the model's output (0.0 to 2.0).

#### Optional Inputs:

- **image_1** through **image_10**: Multiple image inputs for multimodal models. The first image input (image_1) is always visible. Additional image inputs automatically appear as you connect images (up to 10 total).
- **pdf_data**: PDF document input for models that support document understanding.
- **pdf_engine**: Choose between "auto", "mistral-ocr", or "pdf-text" for PDF processing.
- **user_message_input**: Alternative input for the user message, useful for connecting to other nodes.

### Outputs:

- **Output**: The text response from the LLM.
- **Stats**: A string detailing tokens per second, input tokens, output tokens, temperature, and the model used.
- **Credits**: A string showing your remaining OpenRouter account balance (e.g., "Remaining: $9.792").

Note: To display the output text in ComfyUI, you can use the ShowText nodes from [ComfyUI-Custom-Scripts](https://github.com/pythongosssss/ComfyUI-Custom-Scripts), but any text display node will work.

## Examples

### Basic Text Generation

1. Add the OpenRouter node to your workflow
2. Enter your API key
3. Set a system prompt (e.g., "You are a helpful assistant.")
4. Enter a user message (e.g., "Explain quantum computing in simple terms.")
5. Select a model (e.g., "openai/gpt-4")
6. Run the workflow

### Image Understanding

1. Add the OpenRouter node to your workflow
2. Connect an image output from another node to the "image_1" input
3. Enter your API key
4. Set a system prompt (e.g., "You are a helpful assistant.")
5. Enter a user message (e.g., "Describe this image in detail.")
6. Select a multimodal model (e.g., "openai/gpt-4-vision" or "anthropic/claude-3-opus-20240229")
7. Run the workflow

### Multiple Image Analysis

1. Connect your first image to "image_1"
2. As soon as you connect it, "image_2" will automatically appear
3. Connect additional images as needed (up to 6 total)
4. Unused image inputs will automatically hide when disconnected
5. Enter a prompt that references multiple images (e.g., "Compare these images and describe the differences.")
6. Select a multimodal model that supports multiple images
7. Run the workflow

**Note**: The user is responsible for checking if their selected model supports multiple images. Most modern multimodal models (4o, Gemini Flash, etc.) support multiple images in a single request.

### Routing Options

- For cost-effective responses, enable the "cheapest" option (on by default)
- For faster responses, disable "cheapest" and enable "fastest"
- For web search capability, enable "web_search"

## Troubleshooting

- **Model list not loading**: Check your internet connection and OpenRouter API key.
- **Error in response**: Check the error message in the output. It might be due to an invalid API key, model unavailability, or other API issues.
- **Slow responses**: Try using the `:nitro` modifier by enabling the "fastest" option.
- **Token counting issues**: The node uses tiktoken for accurate token counting, but falls back to an estimation method if there's an issue.

## License

MIT License

Copyright (c) 2024 

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Credits

- [OpenRouter](https://openrouter.ai/) 
- [ComfyUI](https://github.com/comfyanonymous/ComfyUI) 
