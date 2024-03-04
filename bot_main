import discord
import requests
from discord.ext import commands, tasks
import os
from datetime import datetime

# Access the bot token from the environment variable
TOKEN = "PASTE YOUR BOT TOKEN HERE"

# Replace 'WEBSITE_INFO' with a dictionary of custom names and URLs
WEBSITE_INFO = {
#   "[[CZ] JN90BU - Ostrava OpenWebRX](http://sdr1.mrak.cz:8073/)": "http://sdr1.mrak.cz:8073/", EXAMPLE WEBSDR
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",
    "[[XX] XX00XX - NAME](WEBSDR WEBSIDE)": "WEBSDR WEBSIDE",

}

# Define intents
intents = discord.Intents.default()
intents.all()

bot = commands.Bot(command_prefix='!', intents=intents)

# Store the last message ID to edit it later
last_message_id = PASTE MESSAGE ID HERE

@bot.event
async def on_ready():
    print(f'{bot.user} has connected to Discord!')
    await bot.change_presence(activity=discord.Game(name="Checking WEBSDR statuses"))
    # Start the background task to check the website status every 5 minutes
    check_status.start()

#CHECK INTERVAL (IN MINUTES)
@tasks.loop(minutes=5)
async def check_status():
    global last_message_id

    # Get the current local time
    local_time = datetime.now()

    status_message = f"**Checking WEBSDRs.** \n__Last check was at:__ **{local_time.strftime('%d.%m.%Y %H:%M')}** (your time zone)\n"

    for custom_name, website_url in WEBSITE_INFO.items():
        try:
            response = requests.get(website_url)
            if response.status_code == 200:
                status_message += f"🟢 - {custom_name} is online\n"
            else:
                status_message += f"🔴 - {custom_name} is offline with status code {response.status_code}\n"
        except requests.ConnectionError:
            status_message += f"🔴 - {custom_name} is offline. Connection error\n"

    # Find the channel where you want to send/edit the status message
    channel_id = PASTE YOUR CHANNEL ID HERE  # Replace with your actual channel ID
    channel = bot.get_channel(channel_id)

    if last_message_id:
        # Edit the last sent message
        last_message = await channel.fetch_message(last_message_id)
        await last_message.edit(content=status_message)
    else:
        # Send a new message
        last_message = await channel.send(status_message)
        last_message_id = last_message.id

@bot.command(name='status', help='Check the current status of the websites')
async def check_status_command(ctx):
    global last_message_id

    # Get the current local time
    local_time = datetime.now()

    status_message = f"**Checking WEBSDRs.** \n__Last check was at:__ **{local_time.strftime('%d.%m.%Y %H:%M')}** (your time zone)\n"

    for custom_name, website_url in WEBSITE_INFO.items():
        try:
            response = requests.get(website_url)
            if response.status_code == 200:
                status_message += f"🟢 - {custom_name} is online\n"
            else:
                status_message += f"🔴 - {custom_name} is offline with status code {response.status_code}\n"
        except requests.ConnectionError:
            status_message += f"🔴 - {custom_name} is offline. Connection error\n"

    await ctx.send(status_message)

# Run the bot
bot.run(TOKEN)
