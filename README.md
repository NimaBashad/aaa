import discord
import asyncio
from discord.ext import commands
from discord import app_commands

token = "MTIxNjQyMjUxNzI0NjI2NzUyMw.Gi6vfE.YiOdWkd__KDABDCg8ZKMRB30mCb4Gkx5Dy9mfM"

intents = discord.Intents.all()
client = commands.Bot(command_prefix= "!",intents= intents)

@client.event
async def on_ready():
    await client.change_presence(status = discord.Status.idle, activity=discord.Game("Moon Store"))
    print('Amade!')


@client.event
async def on_member_join(member : discord.Member):
    channel  = client.get_channel(1215379593054392341)
    await channel.send(f"Hey {member.mention} Welcome to Wolf Store")

voice_object = None


@client.command()
@commands.has_permissions(administrator=True)
async def join(ctx):
    global voice_object
    my_channel = ctx.message.author.voice.channel
    voice_object = await my_channel.connect()
    await ctx.send('ربات با موفقیت جوین چنل شد.')
    

@client.command()
@commands.has_permissions(administrator=True)
async def left(ctx):
    global voice_object
    if voice_object != None:
        await voice_object.disconnect()
        voice_object = None
        await ctx.send('ربات از ویس خارج شد.')
        
    else:
        await ctx.send('ربات جوین ویس چنل نمیباشد.')



client.run(token)
