import discord
from discord.ext import commands
import asyncio


class MeuPrimeiroBot(commands.Bot):
    def __init__(self):
        intents = discord.Intents.all()

        super().__init__(
            command_prefix="$",
            intents=intents
        )

    async def setup_hook(self):
        await self.tree.sync()

    async def on_ready(self):
        print(f"O bot {self.user} ESTÁ A 100%.")


bot = MeuPrimeiroBot()

@bot.command()
async def ping(ctx):
    await ctx.send("Ao seus comandos!")


@bot.command()
async def status(ctx):
    await ctx.send(
        "🟢 **Sistemas Online**\n\n"
        "✔ IA Principal\n"
        "✔ Banco de Dados\n"
        "✔ Servidor Discord\n"
        "✔ Módulo de Segurança"
    )


@bot.command()
async def energia(ctx):
    await ctx.send(
        "⚡ **Reator**\n\n"
        "██████████ 100%\n\n"
        "Energia estável."
    )


@bot.command()
async def diagnostico(ctx):
    await ctx.send("🔍 Executando diagnóstico...")

    await asyncio.sleep(2)

    await ctx.send(
        "```"
        "CPU ............ OK\n"
        "Memória ........ OK\n"
        "Rede ........... OK\n"
        "Banco de Dados . OK\n\n"
        "Nenhuma falha detectada."
        "```"
    )


@bot.command()
async def boot(ctx):
    msg = await ctx.send("Inicializando sistemas...")

    await asyncio.sleep(1)
    await msg.edit(content="Inicializando sistemas...\n\n[██░░░░░░░░] 20%")

    await asyncio.sleep(1)
    await msg.edit(content="Inicializando sistemas...\n\n[█████░░░░░] 50%")

    await asyncio.sleep(1)
    await msg.edit(content="Inicializando sistemas...\n\n[████████░░] 80%")

    await asyncio.sleep(1)
    await msg.edit(
        content="Inicializando sistemas...\n\n"
                "[██████████] 100%\n\n"
                "✅ Bem-vindo à **clube do dc**."
    )
@bot.command()
async def avatar(ctx, member: discord.Member = None):
    member = member or ctx.author

    await ctx.send(member.display_avatar.url)

bot.run("TOKEN")
