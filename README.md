# IntentKit

IntentKit is an autonomous agent framework that enables creation and management of AI agents with various capabilities including blockchain interactions, social media management, and custom skill integration.

## 🚨 Alpha Warning

**This project is currently in alpha stage and is not recommended for production use. We are continuously working towards improvements and updates. Please use with caution.**

## 📋 Table of Contents
- [Features](#features)
- [Architecture](#architecture)
- [Quick Start](#quick-start)
- [The Model](#the-model)
- [Integrations](#integrations)
- [Configuration](#configuration)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

## 🚀 Features

- 🤖 Multiple Agent Support
- 🔄 Autonomous Agent Management
- 🔗 Blockchain Integration (EVM for now, will more)
- 🐦 Social Media Integration (Twitter, Telegram for now, will add more)
- 🛠️ Extensible Skill System
- 🔌 Extensible Plugin System (WIP)

## 🏗️ Architecture



```
                                                                                                       
                                 Entrypoints                                                           
                       │                             │                                                 
                       │   Twitter/Telegram & more   │                                                 
                       └──────────────┬──────────────┘                                                 
                                      │                                                                
  Storage:  ────┐                     │                      ┌──── Skills:                             
                │                     │                      │                                         
  Agent Config  │     ┌───────────────▼────────────────┐     │  Chain Integration (EVM,solana,etc...)  
                │     │                                │     │                                         
  Credentials   │     │                                │     │  Wallet Management                      
                │     │           The  Agent           │     │                                         
  Personality   │     │                                │     │  On-Chain Actions                       
                │     │                                │     │                                         
  Memory        │     │      Powered by LangGraph      │     │  Internet Search                        
                │     │                                │     │                                         
  Skill State   │     └────────────────────────────────┘     │  Image Processing                       
            ────┘                                            └────                                     
                                                                                                       
                                                                More and More...                       
                         ┌──────────────────────────┐                                                  
                         │                          │                                                  
                         │  Agent Config & Memory   │                                                  
                         │                          │                                                  
                         └──────────────────────────┘                                                  
                                                                                                       
```

For more detailed architecture structure, see the [Architecture](docs/architecture.md) section.

## 📥 Quick Start

### Docker (Recommended)

1. Create a new directory and navigate into it:

    ```bash
    mkdirkit && cd intentkit
    ```

2. Download the required files:

    ```bash
    # Download docker-compose.yml
    curl -O https://raw.githubusercontent.com/crestalnetwork/intentkit/main/docker-compose.yml

    # Download example environment file
    curl -O https://raw.githubusercontent.com/crestalnetwork/intentkit/main/example.env
    ```

3. Set up environment:

    ```bash
    # Rename example.env to .env
    mv example.env .env

    # Edit .env file and add your configuration
    # Make sure to set OPENAI_API_KEY
    ```

4. Start the services:

    ```bash
    docker compose up
    ```

5. Create your first Agent:

    ```bash
    curl -X POST http://127.0.0.1:8000/agents \
    -H "Content-Type: application/json" \
    -d '{
        "id": "admin",
        "name": "Admin",
        "prompt": "You are an autonomous AI agent. Respond to user queries."
    }'
    ```

6. Try it out    ```bash
    curl "http://127.0.0.1:8000/admin/chat?q=Hello"
    ```

## 🔬 The Model

Currently, we only support models from OpenAI and DeepSeek. We will be adding support for more models in future updates. If you have specific models in mind, feel free to reach out!

## 🌐 Integrations

### Twitter
[Twitter Integration](docs/twitter.md)

### Coinbase
[Coinbase Integration](docs/skills/cdp.md)

## ⚙️ Configuration

The application can be configured using environment variables or AWS Secrets Manager. Key configuration options include:

- `ENV`: Environment (local or production)
- `DB_*`: PostgreSQL Database configuration (Required)
- `OPENAI_API_KEY`: OpenAI API key for agent interactions (Required)
- `CDP_*`: Coinbase Developer Platform configuration (Optional)

Refer to `example.env` for all available options.

## 🗂️ Project Structure

- `s/`: Abstract classes and interfaces
- `app/`: Core application
  - `core/`: Core modules
  - `services/`: Services  - `entry/`: Entrypoints means the way to interact with the agent
  - `admin/`: Admin logic
  - `config/`: Configurations
  - `api.py`: REST API server
  - `autonomous.py`: Autonomous agent scheduler
  - `twitter.py`: Twitter listener
  - `telegram.py`: Telegram listener
- `models/`: Database models
- `skills/`: Skill implementations
- `skill_sets/`: Predefined skill set collections
- `plugins/`: Reserved for Plugin implementations
- `utils/`: Utility functions

## 🤝 Contributing

Contributions are welcome! Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting a pull request.

### Contribution Steps for Skills

If you want to add a skill collection, follow these steps:

1. Create a new skill collection in the `skills/` directory
2. Implement the skill interface
3. Register the skill in `skills/YOUR_SKILL_COLLECTION/__init__.py`

If you want to add a simple skill, follow these steps:

1. Create a new skill in the `skills/common/` directory
2. Register the skill in `skills/common/__init__.py`

Refer to the [Skill Development Guide](docs/contributing/skills.md) for more information.

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
