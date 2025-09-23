# Renovate Setup Instructions

## Required GitHub Secrets

To enable Renovate with GitHub App authentication, you need to add the following secrets to your repository:

### 1. Go to Repository Settings
- Navigate to your repository on GitHub
- Click on **Settings** tab
- Click on **Secrets and variables** → **Actions**

### 2. Add Required Secrets

Add these two secrets:

#### `BOT_APP_ID`
- **Value**: Your GitHub App ID (numeric)
- **Description**: The ID of your GitHub App used for Renovate

#### `BOT_APP_PRIVATE_KEY`
- **Value**: Your GitHub App private key (PEM format)
- **Description**: The private key of your GitHub App

### 3. How to Get These Values

If you don't have a GitHub App yet:

1. Go to GitHub → Settings → Developer settings → GitHub Apps
2. Click "New GitHub App"
3. Fill in the required fields:
   - **GitHub App name**: `renovate-bot` (or any name you prefer)
   - **Homepage URL**: Your repository URL
   - **Webhook URL**: Leave empty
   - **Repository permissions**:
     - Contents: Read & write
     - Metadata: Read
     - Pull requests: Read & write
     - Issues: Read & write
   - **Subscribe to events**: Pull requests, Push
4. Click "Create GitHub App"
5. Copy the **App ID** (this is your `BOT_APP_ID`)
6. Click "Generate a private key" and download the PEM file
7. Copy the contents of the PEM file (this is your `BOT_APP_PRIVATE_KEY`)

### 4. Install the GitHub App

1. Go to your GitHub App settings
2. Click "Install App"
3. Select your repository
4. Click "Install"

### 5. Test the Setup

1. Go to Actions tab in your repository
2. Click on "Renovate" workflow
3. Click "Run workflow" → "Run workflow"
4. Check the logs to ensure it runs successfully

## Troubleshooting

### Common Issues

1. **Permission denied errors**: Make sure the GitHub App has the correct permissions
2. **Token generation fails**: Verify the App ID and private key are correct
3. **No PRs created**: Check if Renovate can access the repository

### Manual Run

You can manually trigger Renovate by:
1. Going to Actions → Renovate
2. Clicking "Run workflow"
3. Selecting options:
   - **Dry Run**: `false` (to actually create PRs)
   - **Log Level**: `debug` (for detailed logs)
   - **Renovate Version**: `latest`

## Configuration

The Renovate configuration is in `.renovaterc.json5`. Key features:

- **Schedule**: Runs every Monday at 6 AM Moscow time
- **Grouping**: Updates are grouped by service type
- **Auto-merge**: Security updates are automatically merged
- **Ignored**: Custom images and backup tools are excluded

## Next Steps

After setup:
1. Merge the onboarding PR to activate Renovate
2. Review the first batch of dependency updates
3. Customize the configuration in `.renovaterc.json5` if needed
4. Monitor the regular update schedule
