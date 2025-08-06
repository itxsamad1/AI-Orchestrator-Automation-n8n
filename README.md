# AI Orchestrator: Dynamic Model Selection Automation

![AI Orchestrator Workflow](image.png)

## Overview

This n8n workflow intelligently **routes user queries to the most suitable large language model (LLM)** based on the type of request received in a chat environment. It uses structured classification and model selection to optimize both performance and cost-efficiency in AI-driven conversations.

The automation dynamically routes requests to specialized AI models based on content type, optimizing response quality and efficiency while using free models through the OpenRouter API.

**Developed by:** [Abdul Samad](https://github.com/itxsamad1) (itxsamad@github.com)

## Features

- 🤖 **Intelligent Request Classification**: Automatically categorizes user requests into different types
- 🎯 **Dynamic Model Selection**: Routes to the most appropriate AI model based on request type
- 💰 **Cost-Efficient**: Uses free models through OpenRouter API
- 🧠 **Memory Management**: Maintains conversation context across interactions
- ⚡ **Real-time Processing**: Handles chat messages in real-time
- 🔄 **Scalable Architecture**: Easy to extend with additional models and request types

## Request Types & Model Mapping

| Request Type | Model Used | Best For |
|-------------|------------|----------|
| **coding** | `qwen/qwen3-coder` | Code generation, debugging, programming questions |
| **reasoning** | `deepseek/deepseek-chat-v3-0324:free` | Complex reasoning, problem-solving, analysis |
| **general** | `meta-llama/llama-3.3-70b-instruct:free` | General conversations, Q&A, casual chat |
| **search** | `moonshotai/kimi-dev-72b:free` | Information retrieval, research, fact-finding |

## Prerequisites

- [n8n](https://n8n.io/) installed locally or cloud instance
- [OpenRouter](https://openrouter.ai/) API key (free tier available)
- Basic understanding of n8n workflows

## Installation & Setup

### Step 1: Install n8n

If you haven't installed n8n yet, you can install it using npm:

```bash
npm install n8n -g
```

Or use Docker:

```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

### Step 2: Set up OpenRouter API Key

1. Go to [OpenRouter](https://openrouter.ai/) and create an account
2. Generate an API key from your dashboard
3. In n8n, go to **Settings** → **Credentials**
4. Add a new credential of type **OpenRouter API**
5. Enter your API key and save it

### Step 3: Import the Workflow

1. Open your n8n instance (usually at `http://localhost:5678`)
2. Click **"Import from file"** or **"Import from URL"**
3. Upload the `AI Orchestrator Automation.json` file from this repository
4. The workflow will be imported with all nodes and connections

### Step 4: Configure Credentials

1. In the imported workflow, you'll see several OpenRouter Chat Model nodes
2. Click on each model node and configure the credentials:
   - Select your OpenRouter API credential
   - The models are pre-configured to use free tiers

### Step 5: Activate the Workflow

1. Click the **"Active"** toggle in the top bar to activate the workflow
2. Click **"Save"** to save your changes

## Usage

### Starting a Chat Session

1. Once the workflow is active, you can start chatting through the n8n interface
2. The workflow will automatically:
   - Receive your chat message
   - Classify the request type
   - Route to the appropriate AI model
   - Return a contextual response

### Request Classification

The system automatically classifies your requests into these categories:

- **coding**: Programming questions, code generation, debugging
- **reasoning**: Complex problem-solving, logical analysis
- **general**: Casual conversation, general Q&A
- **search**: Information retrieval, research queries

### Example Usage

```
User: "Write a Python function to calculate fibonacci numbers"
→ Classified as: coding
→ Routes to: qwen/qwen3-coder
→ Response: Generated Python code with explanation

User: "Explain the concept of machine learning"
→ Classified as: general
→ Routes to: meta-llama/llama-3.3-70b-instruct
→ Response: Comprehensive explanation

User: "What are the implications of climate change on agriculture?"
→ Classified as: reasoning
→ Routes to: deepseek/deepseek-chat-v3-0324:free
→ Response: Detailed analysis with reasoning
```

## Workflow Architecture

The automation consists of several key components:

1. **Chat Trigger**: Receives incoming chat messages
2. **Request Type Classifier**: Analyzes and categorizes the request
3. **Model Selector**: Routes to the appropriate AI model based on classification
4. **AI Agent**: Manages the conversation and model interactions
5. **Memory Buffer**: Maintains conversation context
6. **Multiple AI Models**: Specialized models for different request types

## Customization

### Adding New Request Types

1. Modify the **Request Type** node's prompt to include new categories
2. Update the **Structured Output Parser** schema
3. Add new rules to the **Model Selector** node
4. Configure additional **OpenRouter Chat Model** nodes

### Changing Models

1. Edit any **OpenRouter Chat Model** node
2. Select a different model from the OpenRouter catalog
3. Ensure the model is compatible with your use case

### Adjusting Classification Logic

1. Modify the prompt in the **Request Type** node
2. Update the classification criteria in the **Model Selector** rules
3. Test with various input types to ensure proper routing

## Troubleshooting

### Common Issues

1. **Workflow not activating**: Check that all credentials are properly configured
2. **API errors**: Verify your OpenRouter API key is valid and has sufficient credits
3. **Classification issues**: Review and adjust the classification prompt in the Request Type node
4. **Memory not working**: Ensure the Simple Memory node is properly connected

### Debug Mode

1. Enable debug mode in n8n settings
2. Check the execution logs for detailed error information
3. Use the built-in testing tools to validate each node

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is open source and available under the [MIT License](LICENSE).

## Support

If you encounter any issues or have questions:

- Create an issue on this GitHub repository
- Check the [n8n documentation](https://docs.n8n.io/)
- Visit the [OpenRouter documentation](https://openrouter.ai/docs)

## Acknowledgments

- Built with [n8n](https://n8n.io/) - The workflow automation platform
- Powered by [OpenRouter](https://openrouter.ai/) - AI model aggregation service
- Uses various open-source AI models for specialized tasks

---

**Note**: This automation is designed to be cost-efficient by using free tier models. For production use, consider upgrading to paid models for better performance and reliability. 