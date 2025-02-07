# Open-WebUI GitHub Actions Tunnel

This repository contains a GitHub Actions workflow that automatically runs Open-WebUI in a Docker container and makes it accessible via an ngrok tunnel. The service restarts every hour to maintain stability.

## Setup Instructions

1. **Fork this repository** to your GitHub account.

2. **Configure ngrok Authentication**
   - Sign up for a free account at [ngrok.com](https://ngrok.com)
   - Get your ngrok authentication token from your dashboard
   - Add the token as a repository secret:
     1. Go to your repository's Settings
     2. Navigate to Secrets and Variables > Actions
     3. Create a new secret named `NGROK_AUTH_TOKEN`
     4. Paste your ngrok auth token as the value

3. **Enable GitHub Actions**
   - Go to the "Actions" tab in your repository
   - Enable workflows if they're not already enabled

## Usage

### Automatic Execution
- The workflow runs automatically every hour
- Each run will provide a new ngrok URL in the workflow logs

### Manual Execution
1. Go to the "Actions" tab in your repository
2. Select the "Host Open-WebUI" workflow
3. Click "Run workflow"
4. Wait for the workflow to start
5. Open the running workflow
6. Look for the URL in the "Start ngrok tunnel and get URL" step logs
   - The URL will be clearly displayed with "🌐 Access URL: ..."
   - The URL is refreshed every 5 minutes in the logs

### Finding the Access URL
1. Click on the latest workflow run
2. Expand the "Start ngrok tunnel and get URL" step
3. Look for the URL displayed between the "=============" lines
4. The URL is also repeated every 5 minutes in the "Keep alive" step

### Important Notes
- Each workflow run creates a new ngrok URL
- The service runs for approximately 55 minutes before restarting
- If you need a permanent URL, consider upgrading to ngrok's paid plan
- The Docker container uses persistent volumes for data storage:
  - `ollama:/root/.ollama`
  - `open-webui:/app/backend/data`

## Troubleshooting

If you don't see the URL in the logs:
1. Make sure your `NGROK_AUTH_TOKEN` is correctly set in repository secrets
2. Check if the workflow completed the "Start ngrok tunnel and get URL" step
3. Look for any error messages in the workflow logs
4. Try running the workflow manually to verify the setup