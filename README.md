# Code.py 🇧🇷

![GitHub release (latest by date)](https://img.shields.io/github/v/release/LucasDesignerF/code-py?color=00FF00&style=flat-square)
![PyPI](https://img.shields.io/pypi/v/code-py?color=00FF00&style=flat-square)
![Python](https://img.shields.io/badge/python-3.12.7+-00FF00?style=flat-square)
![License](https://img.shields.io/github/license/LucasDesignerF/code-py?color=00FF00&style=flat-square)
![GitHub issues](https://img.shields.io/github/issues/LucasDesignerF/code-py?color=00FF00&style=flat-square)
![GitHub stars](https://img.shields.io/github/stars/LucasDesignerF/code-py?color=00FF00&style=flat-square)


**Code.py** é uma biblioteca **pioneira** para criação de bots Discord em **2025**, **100% brasileira**, projetada para ser **simples**, **poderosa** e **moderna**. Com abreviações fluídas (como `cmd`, `resp`, `btn`), suporte nativo às tecnologias mais recentes do Discord, integração com **IA**, **voz avançada**, **OAuth2**, e **sincronização incremental**, a Code.py é a escolha ideal para desenvolvedores que querem criar bots inovadores sem complicações.

---

## 🚀 Por que escolher Code.py?

- **🇧🇷 100% Brasileira**: API com termos em português (`comando`, `usuário`, `interação`) e abreviações intuitivas (`cmd`, `resp`, `falar`).
- **Pioneira para 2025**: Suporte a **IA generativa**, **voz multimídia**, **OAuth2 nativo**, e **sincronização incremental** de comandos.
- **Sem dependências externas**: Suporte nativo a reprodutores de mídia (FFmpeg, VLC, Opus) sem precisar instalar binários.
- **Escalável**: Sharding automático, cache distribuído com Redis, e métricas detalhadas.
- **Open Source**: Licença MIT, com testes robustos e comunidade ativa.

---

## 🛠️ Instalação

Instale a Code.py via pip:

```bash
pip install code-py
```

### Pré-requisitos

- **Python**: 3.12.7 ou superior
- **Dependências**:
  - `aiohttp>=3.11.17`
  - `redis>=5.2.1`
  - `pydub>=0.25.1`
  - `pyopus>=0.3.0`
  - `python-vlc>=3.0.0` (opcional)
  - `sounddevice>=0.4.0` (opcional)

> **Nota**: Não é necessário instalar binários como FFmpeg ou VLC, pois a Code.py usa backends puros em Python (ex.: `pydub`) por padrão.

---

## 🎯 Funcionalidades

### 🗣️ Voz Avançada
- **TTS (Text-to-Speech)**: Integração com ElevenLabs para gerar fala em português.
- **STT (Speech-to-Text)**: Reconhecimento de fala com OpenAI Whisper.
- **Reprodução Multimídia**: Suporte nativo a FFmpeg, VLC, Opus, e outros sem binários externos.
- **Fila de Reprodução**: Toque múltiplos áudios em sequência.
- **Captura de Áudio**: Gravação real de canais de voz com `nextcord.sinks`.

### 🤖 Integração com IA
- Geração de texto com **Grok** (xAI).
- Análise de sentimentos e respostas inteligentes (futuro).
- Suporte a APIs externas para extensibilidade.

### 🔒 OAuth2 Nativo
- Autenticação fluida para apps Discord.
- Geração de URLs de autorização e troca de tokens.

### ⚡ Comandos Modernos
- **Sincronização Incremental**: Registra apenas comandos novos, otimizando performance.
- Suporte a **slash commands**, **contextuais**, e **autocomplete dinâmico**.
- Decoradores simples: `@bot.cmd`, `@bot.btn`, `@bot.menu`.

### 📊 Escalabilidade e Monitoramento
- **Cache Distribuído**: Suporte a Redis com TTL.
- **Sharding Automático**: Ideal para servidores grandes.
- **Métricas Detalhadas**: Latência, interações, erros, e mais.

### 🎨 Interações Multimodais
- **Modais Aninhados**: Formulários interativos.
- **Botões e Menus Dinâmicos**: Crie interfaces ricas.
- **Webhooks Avançados**: Procesamento de eventos em tempo real.

---

## 📝 Exemplo Rápido

Crie um bot com comandos de voz, interações, e IA em poucas linhas:

```python
from codepy import Code, Inter, Embed, Cmd, Voz, Canal

# Cria o bot
bot = Code.criar_bot(prefix="!")

# Comando de saudação com botão
@bot.cmd("ola", desc="Diz olá", opts=[{"nome": "user", "desc": "Usuário a saudar", "tipo": "user"}])
async def ola(inter: Inter, user: User):
    embed = Embed(tit="Olá", desc=f"Saudações, {user.nome}!", cor=0x00FF00)
    await inter.resp("Olá!", embed=embed, btns=[{"txt": "Clicar", "id": "btn_ola"}])

@bot.btn("btn_ola")
async def btn_ola(inter: Inter):
    await inter.resp("Você clicou!", efemera=True)

# Comando para falar
@bot.cmd("falar", desc="Faz o bot falar", opts=[{"nome": "texto", "desc": "Texto a falar", "tipo": "texto"}])
async def falar(inter: Inter, texto: str):
    canal = Canal(inter.channel)
    voz = Voz(bot, canal, elevenlabs_key="SUA_CHAVE_ELEVENLABS", backend="pydub")
    await voz.conectar()
    await voz.falar(texto)
    await voz.desconectar()
    await inter.resp("Fala enviada!")

# Comando para ouvir
@bot.cmd("ouvir", desc="Ouve e transcreve", opts=[{"nome": "duracao", "desc": "Duração em segundos", "tipo": "inteiro"}])
async def ouvir(inter: Inter, duracao: int):
    canal = Canal(inter.channel)
    voz = Voz(bot, canal, whisper_key="SUA_CHAVE_WHISPER", backend="opus")
    await voz.conectar()
    texto = await voz.ouvir(duracao)
    await voz.desconectar()
    await inter.resp(f"Transcrição: {texto}")

# Roda o bot
Code.rodar(bot, "SEU_TOKEN_AQUI")
```

---

## 🧑‍💻 Como Usar

### 1. Configurar o Projeto
- Crie um ambiente virtual:
  ```bash
  python -m venv venv
  source venv/bin/activate  # Linux/Mac
  venv\Scripts\activate     # Windows
  ```
- Instale a Code.py:
  ```bash
  pip install code-py
  ```

### 2. Obter Chaves de API
- **ElevenLabs**: [elevenlabs.io](https://elevenlabs.io) para TTS.
- **OpenAI Whisper**: [openai.com](https://openai.com) para STT.
- **xAI Grok**: [x.ai](https://x.ai) para geração de texto (opcional).

### 3. Criar um Bot
- Crie um bot no [Discord Developer Portal](https://discord.com/developers/applications).
- Ative as intents necessárias (`guilds`, `messages`, `voice_states`).
- Copie o token do bot.

### 4. Rodar o Exemplo
- Salve o código acima em `bot.py`.
- Substitua `"SEU_TOKEN_AQUI"`, `"SUA_CHAVE_ELEVENLABS"`, e `"SUA_CHAVE_WHISPER"` pelas suas chaves.
- Execute:
  ```bash
  python bot.py
  ```

---

## 📚 Documentação Completa

### Classes Principais
- **`Code`**: Classe estática para criar e rodar bots.
  - `Code.criar_bot(prefix="!")`: Cria um bot.
  - `Code.rodar(bot, token)`: Inicia o bot.
- **`Bot`**: Classe principal do bot.
  - `@bot.cmd`: Registra comandos.
  - `@bot.btn`, `@bot.menu`, `@bot.modal_cb`: Registra interações.
- **`Voz`**: Gerencia voz e multimídia.
  - `falar(txt)`: Gera e toca fala.
  - `ouvir(duracao)`: Captura e transcreve áudio.
  - `play_audio(source)`: Toca áudio com suporte a FFmpeg, VLC, Opus.
- **`Inter`**: Manipula interações (slash commands, botões, modais).
- **`Embed`**: Cria embeds estilizados.

### Backends de Mídia
- **Pydub** (padrão): Manipulação de áudio em Python puro, sem binários.
- **Opus**: Codificação de baixa latência com `pyopus`.
- **VLC**: Reprodução avançada com `python-vlc` (opcional).
- **Sounddevice**: Áudio bruto via hardware (opcional).

### Configuração Avançada
- **Cache com Redis**:
  ```python
  bot = Code.criar_bot(cache_conf={"redis_url": "redis://localhost:6379"})
  ```
- **Sharding**:
  ```python
  bot = Code.criar_bot(shards=4)
  ```

---

## 🌟 Contribuindo

Quer ajudar a tornar a Code.py ainda melhor? Siga estes passos:

1. Fork o repositório: [github.com/LucasDesignerF/code-py](https://github.com/LucasDesignerF/code-py)
2. Clone seu fork:
   ```bash
   git clone https://github.com/SEU_USUARIO/code-py.git
   ```
3. Crie uma branch:
   ```bash
   git checkout -b sua-funcionalidade
   ```
4. Faça suas alterações e commit:
   ```bash
   git commit -m "Adiciona funcionalidade X"
   ```
5. Envie para o repositório:
   ```bash
   git push origin sua-funcionalidade
   ```
6. Abra um Pull Request!

### Diretrizes
- Siga o estilo de código PEP 8.
- Adicione testes em `tests/`.
- Use abreviações em português (ex.: `cmd`, `resp`).

---

## 🛡️ Licença

Licença MIT - veja [LICENSE](LICENSE) para detalhes.

---

## 📬 Contato

- **Autor**: Lucas Dev - RedeBots
- **Email**: [ofc.rede@gmail.com](mailto:ofc.rede@gmail.com)
- **GitHub**: [LucasDesignerF](https://github.com/LucasDesignerF)
- **Discord**: Junte-se ao nosso [servidor de suporte](https://discord.gg/AhcHfUpNeM)

---

## 🎉 Agradecimentos

- **Comunidade brasileira de desenvolvedores** por inspirar uma biblioteca 100% nacional.
- **xAI**, **ElevenLabs**, e **OpenAI** pelas APIs de IA.
- **Nextcord** pela base sólida para bots Discord.

---

> **Code.py - Feito no Brasil, para o mundo!** 🇧🇷
