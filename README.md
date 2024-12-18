# Eng Discord Bot / Code Captain

This repository contains the PR Summary Bot, a Google Cloud Function that generates and sends pull request summaries to a Discord channel.

- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Running the Bot locally](#running-the-bot-locally)
- [Deployment](#deployment)
- [Testing the Bot in production](#testing-the-bot-in-production)
- [Checking the logs](#checking-the-logs)
  - [Project Structure](#project-structure)
  - [Deploying the Bot](#deploying-the-bot)

## Prerequisites

- Node.js (>=20.x)
- pnpm (>=9.x)

## Setup

1. Clone the repository:

   ```sh
   git clone https://github.com/mento-protocol/eng-discord-bot.git
   cd eng-discord-bot
   ```

2. Install dependencies:

   ```sh
   pnpm install
   ```

3. Configure environment variables:

   - Create a `.env` file in the root directory via `cp .env.example .env`
   - Add the necessary environment variables for GitHub, Discord, and OpenAI services.

4. Build the project:

   ```sh
   pnpm run build
   ```

## Running the Bot locally

To start the bot locally, run:

```sh
# Dev mode with hot-reloading via nodemon
pnpm dev
```

Now trigger the bot by sending a request to it:

```sh
pnpm test
```

## Deployment

To deploy the bot, run:

```sh
pnpm deploy:function
```

If you want to change the schedule on which the bot runs, update the `deploy:scheduler` npm task with the desired cronjob frequency and then run:

```sh
pnpm deploy:scheduler
```

## Testing the Bot in production

To manually trigger the deployed Bot in production, run:

```sh
# Will fire a PubSub event that the bot will catch and trigger
pnpm test:prod
```

## Checking the logs

To view the last logs in your local terminal, run:

```sh
pnpm run logs
```

To get a URL to the full logs in the Google Cloud Console, run:

```sh
pnpm run logs:url
```

### Project Structure

- `src/` - Contains the source code for the bot.
  - `index.ts` - Entry point of the cloud function.
  - `config.ts` - Configuration settings.
  - `discord-service.ts` - Service for interacting with Discord.
  - `github-service.ts` - Service for interacting with GitHub.
  - `openai-service.ts` - Service for generating messages using OpenAI.

### Deploying the Bot

- Run `npm run deploy:function` redeploy the Google Cloud Function with the latest changes
- If you also want to change the scheduler job, run `npm run deploy:scheduler`
