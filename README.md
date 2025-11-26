# Agent Quickstart - Python

Demonstrates connecting to an Azure AI Foundry agent for voice conversations. The agent handles model selection, instructions, and tools, with support for proactive greetings.

**Key Features:**
- Azure AI Foundry agent integration
- Proactive greeting support
- Azure authentication (required)
- Agent-managed tools and instructions

## Prerequisites

All samples require:

- [Python 3.8+](https://www.python.org/downloads/)
- Audio input/output devices (microphone and speakers)
- [Azure subscription](https://azure.microsoft.com/free/) - Create one for free

### Azure Resources

- [Azure AI Foundry project](https://learn.microsoft.com/azure/ai-studio/how-to/create-projects) with a deployed agent
- [Azure CLI](https://learn.microsoft.com/cli/azure/install-azure-cli) for authentication

## Getting Started

### Quick Start

1. **Navigate to the quickstarts folder**:

2. **Create a virtual environment** (recommended):
   ```bash
   python -m venv .venv
   
   # On Windows
   .venv\Scripts\activate
   
   # On Linux/macOS
   source .venv/bin/activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**:
   - Copy `.env_sample` to `.env`
   - Update `.env` with your Azure credentials

5. **Run a sample**:
   ```bash
   python agents-quickstart.py
   # or
   python agentsv2-quickstart.py
   ```

### Authentication

**Agent Quickstart** requires Azure authentication:
```bash
az login
python agents-quickstart.py
```

## Configuration

All samples use a `.env` file for configuration. Copy `.env_sample` to `.env` and update with your values:

### Agent Quickstart Configuration
```plaintext
AZURE_VOICELIVE_ENDPOINT=https://your-endpoint.services.ai.azure.com/
AZURE_VOICELIVE_API_VERSION=2025-10-01
AZURE_VOICELIVE_PROJECT_NAME=your-project-name

# Foundry Agent V1
AZURE_VOICELIVE_AGENT_ID=asst_your-agent-id

# Foundry Agent V2
AZURE_VOICELIVE_AGENT2_NAME=your-agent-name
```

## Common Features

All samples demonstrate:

- **Real-time Voice**: Bidirectional audio streaming for natural conversations
- **Audio Processing**: Microphone capture and speaker playback using PyAudio
- **Interruption Handling**: Support for natural turn-taking in conversations
- **Resource Management**: Proper cleanup of connections and audio resources
- **Async/Await**: Modern Python async programming patterns

## Available Voices

Popular neural voice options include:

- `en-US-AvaNeural` - Female, conversational
- `en-US-AndrewNeural` - Male, conversational
- `en-US-JennyNeural` - Female, friendly
- `en-US-GuyNeural` - Male, professional
- `en-US-AriaNeural` - Female, cheerful
- `en-US-DavisNeural` - Male, calm

See the [Azure Neural Voice Gallery](https://speech.microsoft.com/portal/voicegallery) for all available voices.

## Architecture

### Agent Quickstart Flow
```
User Voice → Microphone → PyAudio → VoiceLive SDK → Azure AI Foundry Agent
                                                              ↓
User Hears ← Speakers ← PyAudio ← VoiceLive SDK ← Agent Response
```

## Troubleshooting

### Audio Issues

- **No audio input/output**: Verify your microphone and speakers are working and set as default devices
- **PyAudio installation errors**: 
  - On Windows: Install via `pip install pyaudio`
  - On Linux: `sudo apt-get install python3-pyaudio` or `pip install pyaudio`
  - On macOS: `brew install portaudio && pip install pyaudio`
- **Audio device busy**: Close other applications using your audio devices (e.g., Teams, Zoom)
- **Poor audio quality**: Update your audio drivers to the latest version

### Authentication Issues

- **401 Unauthorized**: 
  - For Azure auth: Run `az login` to authenticate with Azure CLI
- **Agent not found** (Agent sample): Check your agent ID format (should be `asst_xxxxx`) and project name
- **Token credential fails**: Ensure Azure CLI is installed and you're logged in
- **Insufficient permissions** (Agent sample): Verify your Azure account has access to the AI Foundry project

### Connection Issues

- **Endpoint errors**: Verify your endpoint URL format in `.env`: `https://your-endpoint.services.ai.azure.com/`
- **WebSocket timeout**: Check your network connection and firewall settings
- **Certificate errors**: Ensure your system certificates are up to date
- **Model not available** (Model/Function samples): Verify your Speech resource has VoiceLive enabled

### Python Environment Issues

- **Module not found**: Run `pip install -r requirements.txt` to install dependencies
- **Python version**: Verify Python 3.8 or later is installed: `python --version`
- **Virtual environment**: Use a virtual environment to avoid package conflicts
- **Import errors**: Ensure you're in the correct directory and virtual environment is activated

### Common Command Line Options

All samples support these options (use `--help` for full details):

**agents-quickstart.py**

- `--endpoint`: Azure VoiceLive endpoint URL
- `--voice`: Voice for the assistant (default varies by sample)
- `--verbose` or `-v`: Enable detailed logging
- `--agent-id`: Azure AI Foundry agent ID
- `--project-name`: Azure AI Foundry project name

**agentsv2-quickstart.py**

- `--endpoint`: Azure VoiceLive endpoint URL
- `--voice`: Voice for the assistant (default varies by sample)
- `--verbose` or `-v`: Enable detailed logging
- `--agent-name`: Azure AI Foundry agent name
- `--project-name`: Azure AI Foundry project name


## Requirements

The samples use the following Python packages (defined in `requirements.txt`):

```
azure-ai-voicelive[aiohttp]
pyaudio
python-dotenv
azure-identity
```

Install all dependencies with:
```bash
pip install -r requirements.txt
```

## Additional Resources

- [Azure AI Speech - Voice Live Documentation](https://learn.microsoft.com/azure/ai-services/speech-service/voice-live)
- [Python SDK Documentation](https://learn.microsoft.com/python/api/overview/azure/ai-voicelive-readme)
- [Support Guide](../SUPPORT.md)


## License

This project is licensed under the MIT License - see the [LICENSE](../LICENSE) file for details.