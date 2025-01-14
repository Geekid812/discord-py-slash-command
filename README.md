<p align="center">
    <br>
    <a href="https://pypi.org/project/discord-py-slash-command/"><img src="/.github/discordpyslashlogo.png" alt="discord-py-slash-command" height="128"></a>
    <h2 align = "center">A simple discord slash command extension for <a href="https://github.com/Rapptz/discord.py">discord.py</a></h2>
</p>
<p align="center">
        <a href="https://app.codacy.com/gh/eunwoo1104/discord-py-slash-command?utm_source=github.com&utm_medium=referral&utm_content=eunwoo1104/discord-py-slash-command&utm_campaign=Badge_Grade_Settings"><img src="https://api.codacy.com/project/badge/Grade/224bdbe58f8f43f28a093a33a7546456" alt="Codacy Badge'></a>
        <a href="https://discord.gg/KkgMBVuEkx"> <img alt="Discord" src="https://img.shields.io/discord/789032594456576001"> </a>
</p>
<p align="center">
   <a href="#about">About</a> ⦿
   <a href="#installation">Installation</a> ⦿
   <a href="#disclaimer">Disclaimer</a> ⦿
   <a href="#examples">Examples</a> ⦿
   <a href="https://discord-py-slash-command.readthedocs.io/en/latest/">Documentation</a> ⦿
   <a href="https://github.com/eunwoo1104/discord-py-slash-command/discussions">Discussions</a>
</p>
   

Note that `master` branch is in development. For release version, please see `hotfix-command-register` branch.

## About
Discord Slash Commands are a new implementation for the Bot API that utilize the forward-slash "/" symbol.
Released on 15 December 2020, many bot developers are still learning to learn how to implement this into
their very own bots. This extension aims to help serve as a guidance for those looking into wanting to add
these new slash commands into their bots for those that use discord.py, building off of the current library
code and substituting its own for where it's needed. *discord-py-slash-command* stands as the first public
slash command extension library to be made for Discord Bot API libraries.

## Installation
You are able to easily install the *discord-py-slash-command* library by using the given PIP line below:

`pip install -U discord-py-slash-command`

## Disclaimer
Since slash commands are currently not officially released (They're in public beta), there will be many breaking
changes to this extension which may cause it to become unstable. It is recommended to wait until discord officially
releases slash commands. Waiting until Release 1.1.0, which is planned to have most features implemented in the code, is also recommended.
At this time, the developer of *discord.py* has no plans to officially support slash commands for their library.

## Examples
### Quick Startup
This is a quick startup method towards using slash commands.
```py
import discord
from discord.ext import commands
from discord_slash import SlashCommand, SlashContext

bot = commands.Bot(command_prefix="!", intents=discord.Intents.all())
slash = SlashCommand(bot)

@slash.slash(name="test")
async def _test(ctx: SlashContext):
    embed = discord.Embed(title="embed test")
    await ctx.send(content="test", embeds=[embed])

bot.run("discord_token")
```

### Advanced
This offers implementation of the slash command library in the usage of a cog.
```py
import discord
from discord.ext import commands
from discord_slash import cog_ext, SlashCommand, SlashContext

class Slash(commands.Cog):
    def __init__(self, bot):
        if not hasattr(bot, "slash"):
            # Creates new SlashCommand instance to bot if bot doesn't have.
            bot.slash = SlashCommand(bot, override_type=True)
        self.bot = bot

    @cog_ext.cog_slash(name="test")
    async def _test(self, ctx: SlashContext):
        embed = discord.Embed(title="embed test")
        await ctx.send(content="test", embeds=[embed])

def setup(bot):
    bot.add_cog(Slash(bot))
```
