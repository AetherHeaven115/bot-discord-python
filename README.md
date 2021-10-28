# bot-discord-python

import discord from discord.ext import commands import datetime

from urllib import parse, request import re

bot = commands.Bot(command_prefix='!', description="This is a Helper Bot")

@bot.command() async def sum(ctx, numOne: int, numTwo: int): await ctx.send(numOne + numTwo)

@bot.command() async def ping(ctx): await ctx.send('pong')

#Events @bot.event async def on_ready(): await bot.change_presence(activity=discord.Streaming(name="Tutorials", url="http://www.twitch.tv/aetherheaven935")) print('My Ready is Body')

@bot.command() async def info(ctx): embed = discord.Embed(title=f"{ctx.guild.name}", description="es el mejor server", timestamp=datetime.datetime.utcnow(), color=discord.Color.blue()) embed.add_field(name="Server created at", value=f"{ctx.guild.created_at}") embed.add_field(name="Server Owner", value=f"{ctx.guild.owner}") embed.add_field(name="Server Region", value=f"{ctx.guild.region}") embed.add_field(name="Server ID", value=f"{ctx.guild.id}") # embed.set_thumbnail(url=f"{ctx.guild.icon}") embed.set_thumbnail(url="https://xbox-store-checker.com/assets/upload/game/2019/02/optimize/c0twnspk361c-background.jpg")

await ctx.send(embed=embed)
#Busquedas de youtube :3

@bot.command() async def youtube(ctx, *, search): query_string = parse.urlencode({'search_query': search}) html_content = request.urlopen('http://www.youtube.com/results?' + query_string) #print(html_content.read().decode()) search_results = re.findall('href="\/watch\?v=(.{11})', html_content.read().decode()) # print(search_results) #I will put just the first result, you can loop the response to show more results await ctx.send('https://www.youtube.com/watch?v=' + search_results[0])

@bot.command() async def hola(ctx): await ctx.send('bienvenido al server')

@bot.command() async def aetherheaven(ctx): await ctx.send('https://www.twitch.tv/aetherheaven935')

@bot.command() async def twitter(ctx): await ctx.send('https://twitter.com/AetherHeaven115')

bot.run('Token')
