# Open-WebUI GitHub Actions Hoster

Host Open-WebUI and Ollama in a GitHub Actions workflow with ngrok tunnel access. Auto-restarts hourly for stability.

## Quick Start

1. Fork this repository
2. Add your ngrok auth token as `NGROK_AUTH_TOKEN` in repository secrets
   - Get token from [ngrok.com](https://ngrok.com) (free account)
   - Repository Settings > Secrets and Variables > Actions
3. Enable GitHub Actions in your repository

## Configuration

The `config.yml` in the root of the project contains all customizable settings:

```yaml
# Open-WebUI Container Settings
openwebui:
  image: ghcr.io/open-webui/open-webui:latest
  port: 3000
  # API integrations
  api_keys:
    openrouter: ""  # Your OpenRouter API key

# Ollama Container Settings
ollama:
  image: ollama/ollama
  download_models: []  # Add model names to download on startup

# Ngrok Tunnel Settings
ngrok:
  region: us  # Options: us, eu, ap, au, sa, jp, in
  update_interval: 300  # How often to refresh URL in logs (seconds)
```

### Configuring Models

To automatically load Ollama models at startup, add model names to the `download_models` array:

```yaml
ollama:
  image: ollama/ollama
  download_models: ["llama3", "mistral"]
```

### Configuring API Integrations

Open-WebUI supports various API integrations. To configure OpenRouter API:

1. Get your API key from [OpenRouter](https://openrouter.ai)
2. Add it to the `config.yml` file:
```yaml
openwebui:
  # ...existing configuration...
  api_keys:
    openrouter: "your_openrouter_api_key_here"
```

## Usage

### View Access URL
- Check the "Start ngrok tunnel and get URL" step in workflow logs
- Look for `🌐 Access URL: ...` between `=============` lines
- URL refreshes every 5 minutes (or as configured) in logs

### Run Options
- **Automatic**: Runs every hour
- **Manual**: 
  1. Go to Actions tab
  2. Select "Host Open-WebUI" workflow
  3. Click "Run workflow"

## Technical Details

### Storage
Docker volumes used:
- `ollama:/root/.ollama` - Stores models and configuration
- `open-webui:/app/backend/data` - Stores user data and chats

### Limitations
- New ngrok URL generated each run
- 55-minute runtime before auto-restart
- Free ngrok plan limitations apply

## Troubleshooting

1. Verify `NGROK_AUTH_TOKEN` is correctly set in repository secrets
2. Check workflow completion status
3. Review error messages in logs
4. Test with manual workflow run

## Advanced Customization

For more advanced configurations, you can modify the `.github/workflows/host-open-webui.yml` file. This contains the complete workflow definition and can be customized for special requirements.
