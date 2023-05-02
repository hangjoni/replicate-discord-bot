# Replicate Discord bot

This is a companion codebase for a [tutorial for building a text-to-image chat bot](https://replicate.com/blog/build-a-robot-artist-for-your-discord-server-with-stable-diffusion) using the Stable Diffusion model and the Replicate API.

<img src="https://replicate.com/static/blog/discord-bot/dreaming-of-rabbits.png">

## Set up

```
pip install -r requirements.txt
```

Add Discord and Replicate tokens to `.env` (Do not share or commit this file)

```
REPLICATE_API_TOKEN=<your-token>
DISCORD_TOKEN=<your-token>
```

To run the bot:

```
python bot.py
```

## Using the bot

Add the bot to a Discord channel. Then type `!help` to get available commands.

To generate an image

```
!stable_diffusion an astronaut riding a horse
```

## Host the bot on the cloud
Hosting the bot deployment on the cloud makes it highly available. This way we can use the Discord bot to generate arts even without keeping our computer running.

We will be using fly.io 
To get started, see [Fly's "speedrun" guide](https://fly.io/docs/speedrun/) to install the flyctl command-line tool and create a Fly account.

Create Dockerfile and paste this below. This tells fly.io to create a tiny Docker image with python 3.10 loaded, load our code to working directory, install required packages as specified in requirements.txt , and run the bot.py app

```
FROM python:3.10
WORKDIR /code
COPY requirements.txt /code/
RUN pip install -r requirements.txt
COPY . /code
CMD python bot.py
```
Now we're ready to launch the app on fly.io
```
flyctl launch
```
That command will generate a new file called fly.toml, but it's designed for running web apps so you'll need to make a few changes. Remove the [[services]] block and everything below it. Your modified file should look something like this:
```
# fly.toml app configuration file generated for aged-sunset-8082 on 2023-04-26T10:22:03+08:00
#
# See https://fly.io/docs/reference/configuration/ for information about how to use this file.
#

app = "aged-sunset-8082"
primary_region = "sin"

kill_signal = "SIGINT"
kill_timeout = 5
processes = []

[env]

[experimental]
  allowed_public_ports = []
  auto_rollback = true
```
Then configure your Fly app using the secrets from your local .env file
```
flyctl secrets set REPLICATE_API_TOKEN=... DISCORD_TOKEN=...
```
Now our app should be running on the cloud
