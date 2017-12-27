import discord
from discord.ext.commands import Bot
from discord.ext import commands
from bs4 import BeautifulSoup
import asyncio
from urllib.request import urlopen
#import logging

#logging.basicConfig(level=logging.INFO)

Client = discord.Client()
client = Bot(command_prefix = "!")
@client.event
async def on_ready():
    print("Bot is ready")

@client.event
async def on_message(message):
    if message.content.startswith('!elo'):
        parsed = message.content[len('!elo'):].strip()
        name = parsed.split()
        first_name = name[0]
        last_name = name[1]
        url = "http://www.mtgeloproject.net/index.php?lastname="+last_name+"&firstname="+first_name+"&search=Search"
        content = urlopen(url)
        soup = BeautifulSoup(content, "lxml")
        elo_listed = soup.find('font', attrs={'style':'font-weight:bold'})
        try:
            listed = elo_listed.text.strip()
        except:
            await client.send_message(message.channel, "Name could not be found (multiple listings, name not found, or incorrect spelling)")
        #print(listed)
        await client.send_message(message.channel, "ELO found for "+first_name+" "+last_name+": "+ listed)
                                  
client.run("TOKEN-REDACTED")
