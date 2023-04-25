# Replicate Discord bot

This is a companion codebase for a [tutorial for building a text-to-image chat bot](https://replicate.com/blog/build-a-robot-artist-for-your-discord-server-with-stable-diffusion) using the Stable Diffusion model and the Replicate API.

<img src="https://replicate.com/static/blog/discord-bot/dreaming-of-rabbits.png">

## Set up

```
poetry init -n
poetry add discord.py python-dotenv replicate
touch .env
```

Add Discord and Replicate tokens to `.env` (Do not share or commit this file)

```
REPLICATE_API_TOKEN=<your-token>
DISCORD_TOKEN=<your-token>
```

To run the bot:

```
poetry run python bot.py
```

## Using the bot

Add the bot to a Discord channel. Then type `!help` to get available commands.

To generate an image

```
!stable_diffusion an astronaut riding a horse
```
