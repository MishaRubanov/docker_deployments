# Docker Auto-Deploy Repository

This repository contains Docker configurations for applications that automatically deploy to Coolify when changes are pushed.

## Structure

```
.
├── apps/                    # Directory containing all application Dockerfiles
│   ├── app1/               # First application
│   │   ├── Dockerfile      # Application-specific Dockerfile
│   │   └── .env.example    # Example environment variables
│   └── app2/               # Second application
│       ├── Dockerfile      # Application-specific Dockerfile
│       └── .env.example    # Example environment variables
├── .github/
│   └── workflows/          # GitHub Actions workflows
└── README.md              # This file
```

## How It Works

1. Each application has its own directory under `apps/`
2. When changes are pushed to a Dockerfile with the commit message containing `[deploy]`, the GitHub Action will trigger
3. The action will:
   - Detect which app's Dockerfile was changed
   - Trigger Coolify to build and deploy only the changed app

## Setup

1. In Coolify:
   - Set up your deployment type as "Dockerfile" for each app
   - Get the webhook URL from each resource's Webhook menu
   - Create an API token

2. In GitHub:
   Add the following secrets:
   - `COOLIFY_TOKEN`: Your Coolify API token
   - `COOLIFY_WEBHOOK_app1`: Webhook URL for app1
   - `COOLIFY_WEBHOOK_app2`: Webhook URL for app2
   (Add more webhook secrets for each app, using the format `COOLIFY_WEBHOOK_appname`)

## Adding a New Application

1. Create a new directory under `apps/` for your application
2. Add your Dockerfile and any necessary configuration files
3. Add the app's webhook URL as a secret in GitHub (`COOLIFY_WEBHOOK_appname`)
4. Push your changes with the commit message containing `[deploy]`

## Commit Message Format

To trigger a deployment, include `[deploy]` in your commit message. For example:
```
git commit -m "Update Dockerfile [deploy]"
```

## Requirements

- GitHub repository
- Coolify instance 