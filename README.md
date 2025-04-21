# Code.py

Uma biblioteca avançada para criar bots Discord em 2025, com suporte a comandos slash, interações ricas, voz, IA, cache distribuído, sharding, logging e métricas. Projetada para ser simples, em português brasileiro, e não requer a instalação direta do Nextcord.

## Instalação

```bash
pip install code-py
```

## Exemplo

```python
from code import Code, Interacao
import nextcord

bot = Code.criar_bot(prefixo="!")

@bot.comando(nome="ola", desc="Diz olá")
async def ola(inter: Interacao):
    await inter.responder("Olá, mundo!", efemera=True)

Code.rodar(bot, "SEU_TOKEN_AQUI")
```

## Funcionalidades

- Comandos slash e contextuais com opções e subcomandos
- Interações ricas: modais, botões, menus, views
- Suporte a voz: streaming, TTS, reconhecimento de fala
- Cache distribuído com Redis
- Sharding automático
- Integração com IA (ex.: Grok)
- Logging estruturado e métricas
- API fluida em português brasileiro

## Licença

MIT License
