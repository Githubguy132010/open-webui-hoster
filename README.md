# Open-WebUI GitHub Actions Tunnel

Run Open-WebUI in a GitHub Actions workflow with ngrok tunnel access. Auto-restarts hourly for stability.

## Quick Start

1. Fork the repository
2. Add your ngrok auth token as `NGROK_AUTH_TOKEN` in repository secrets
   - Get token from [ngrok.com](https://ngrok.com) (free account)
   - Repository Settings > Secrets and Variables > Actions
3. Enable GitHub Actions in your repository

## Usage

### View Access URL
- Check the "Start ngrok tunnel and get URL" step in workflow logs
- Look for `🌐 Access URL: ...` between `=============` lines
- URL refreshes every 5 minutes in logs

### Run Options
- **Automatic**: Runs every hour
- **Manual**: 
  1. Go to Actions tab
  2. Select "Host Open-WebUI" workflow
  3. Click "Run workflow"

## Technical Details

### Storage
Docker volumes used:
- `ollama:/root/.ollama`
- `open-webui:/app/backend/data`

### Limitations
- New ngrok URL generated each run
- 55-minute runtime before auto-restart
- Free ngrok plan limitations apply

## Troubleshooting

1. Verify `NGROK_AUTH_TOKEN` in secrets
2. Check workflow completion status
3. Review error messages in logs
4. Test with manual workflow run
