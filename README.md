# J.A.R.V.I.S. - Advanced Personal AI Assistant

> "Sometimes you gotta run before you can walk." — Tony Stark

Um assistente pessoal inteligente para Windows com interface holográfica futurista, controle por voz, integração com aplicativos e automação completa do sistema.

![JARVIS Interface](docs/interface-preview.png)

## ✨ Funcionalidades

### 🎨 Interface Visual Futurista
- **Núcleo Holográfico Central** — Animações SVG/Canvas com 12 anéis concêntricos rotativos independentes
- **Estados Visuais Dinâmicos** — Standby, Escutando, Processando, Respondendo, Executando, Erro
- **Reatividade de Áudio** — Ondas e partículas respondem em tempo real à voz
- **Tema Black Futuristic** — Preto absoluto (#000000) com acentos brancos/cinza metálico
- **Responsivo** — Suporte a tela cheia, janela redimensionável, system tray

### 🗣️ Controle por Voz Completo
- **Wake Word** — "Jarvis" ativa o assistente
- **Speech-to-Text** — Reconhecimento em português brasileiro (Google Speech Recognition)
- **Text-to-Speech** — Edge TTS com vozes neurais naturais (Thalita, Antonio, etc.)
- **Interrupção Inteligente** — Para de falar quando você começa a falar
- **Indicadores Visuais** — Microfone, nível de áudio, estado do processamento

### 🤖 Inteligência Artificial
- **Múltiplos Provedores** — Anthropic (Claude), OpenAI (GPT), Ollama (local), Custom
- **Contexto de Conversa** — Memória de até 20 mensagens anteriores
- **Personalidade JARVIS** — Inteligente, educado, eficiente, levemente irônico
- **Português Brasileiro** — Respostas naturais no seu idioma

### 💻 Controle do Windows
- **Apps** — Abrir/fechar/focar qualquer aplicativo (Brave, Spotify, VS Code, etc.)
- **Arquivos** — Navegar pastas, buscar arquivos, criar diretórios
- **Sistema** — Volume, brilho, captura de tela, desligar/reiniciar/suspender/bloquear
- **Janela** — Minimizar, maximizar, fechar janela ativa
- **PowerShell** — Execução segura de comandos com sanitização
- **Confirmação** — Ações perigosas pedem confirmação explícita

### 🎵 Integração Spotify
- **Controle Total** — Play, pause, next, previous, volume
- **Busca** — Artistas, álbuns, playlists, faixas
- **Contexto** — "Coloque uma música do The Weeknd"
- **OAuth 2.0** — Autenticação segura com tokens de atualização

### 🌐 Automação Brave Browser
- **Playwright** — Automação robusta headless/headed
- **Busca** — Google, DuckDuckGo, Bing, YouTube
- **Navegação** — Abrir URLs, novas abas, trocar abas
- **JavaScript** — Execução de scripts personalizados

### 🧠 Memória Persistente
- **SQLite Local** — Dados ficam no seu computador
- **Categorias** — Preferências, fatos, projetos, contatos, notas
- **Tags** — Organização flexível com busca
- **CRUD Completo** — Interface visual para gerenciar memórias

### 📊 Monitoramento do Sistema
- **Tempo Real** — CPU, RAM, Disco, Rede, GPU, Temperatura
- **Processos** — Top 20 por uso de CPU
- **Serviços** — Listar, iniciar, parar serviços Windows
- **Drivers** — Informações de drivers assinados

## 🚀 Instalação Rápida

### Pré-requisitos
- **Windows 10/11** (64-bit)
- **Node.js 18+** — [nodejs.org](https://nodejs.org/)
- **Python 3.10+** — [python.org](https://python.org/)
- **Rust** (para app desktop) — [rustup.rs](https://rustup.rs/)
- **Microfone** funcional

### 1. Clone e instale
```powershell
# No PowerShell como Administrador (recomendado)
git clone https://github.com/seu-usuario/jarvis-assistant.git
cd jarvis-assistant
.\scripts\install.ps1
```

### 2. Configure as chaves de API
Edite `backend/.env` com suas credenciais:

```env
# Obrigatório: pelo menos um provedor de IA
ANTHROPIC_API_KEY=sk-ant-xxxxxxxxxxxx
# OU
OPENAI_API_KEY=sk-xxxxxxxxxxxx

# Opcional: Spotify
SPOTIFY_CLIENT_ID=xxxxxxxxxxxx
SPOTIFY_CLIENT_SECRET=xxxxxxxxxxxx
```

> **Obtenha chaves em:**
> - Anthropic: https://console.anthropic.com/
> - OpenAI: https://platform.openai.com/
> - Spotify: https://developer.spotify.com/dashboard/

### 3. Execute

**Desenvolvimento (hot reload):**
```powershell
.\scripts\dev.ps1
```
- Frontend: http://localhost:5173
- Backend: http://localhost:8000
- Docs API: http://localhost:8000/docs

**Produção (app desktop):**
```powershell
.\scripts\build.ps1
```
Instalador em `frontend/src-tauri/target/release/bundle/`

## 🎮 Como Usar

### Ativação por Voz
1. Diga **"Jarvis"** claramente
2. Aguarde o som de confirmação
3. Fale seu comando naturalmente

### Exemplos de Comandos

**Conversa:**
- "Jarvis, qual a capital da França?"
- "Explique quantum computing de forma simples"
- "Me ajude a escrever um email formal"

**Sistema:**
- "Abra o VS Code"
- "Feche o Spotify"
- "Aumente o volume"
- "Faça uma captura de tela"
- "Pesquise Rust tutorial no YouTube"

**Spotify:**
- "Toque minha playlist de favoritos"
- "Coloque The Weeknd"
- "Pause a música"
- "Próxima faixa"

**Memória:**
- "Lembre-se que meu aniversário é dia 15 de março"
- "Qual meu projeto atual?"
- "Esqueça minha senha do wifi"

### Atalhos de Teclado
| Atalho | Ação |
|--------|------|
| `Ctrl + Espaço` | Ativar/desativar microfone |
| `F11` | Alternar tela cheia |
| `ESC` | Fechar painéis laterais |

## 🏗️ Arquitetura

```
jarvis-assistant/
├── frontend/                 # React + TypeScript + Vite
│   ├── src/
│   │   ├── components/
│   │   │   ├── core/         # HolographicCore (núcleo principal)
│   │   │   ├── layout/       # TopBar, BottomBar
│   │   │   └── panels/       # SystemPanel, MemoryPanel, SettingsPanel
│   │   ├── stores/           # Zustand (estado global)
│   │   ├── hooks/            # Custom hooks
│   │   └── styles/           # Tailwind + CSS customizado
│   └── src-tauri/            # Tauri (Rust) - App desktop nativo
│
├── backend/                  # Python + FastAPI
│   ├── app/
│   │   └── main.py           # FastAPI + WebSocket
│   ├── config/
│   │   └── settings.py       # Pydantic Settings
│   ├── models/
│   │   └── database.py       # SQLite + operações
│   └── services/
│       ├── ai_service.py     # Múltiplos provedores LLM
│       ├── voice_service.py  # STT/TTS + Wake word
│       ├── windows_service.py# Automação Windows
│       ├── spotify_service.py# Spotify Web API
│       ├── brave_service.py  # Playwright automation
│       └── system_service.py # Monitoramento sistema
│
├── scripts/                  # PowerShell scripts
│   ├── install.ps1
│   ├── dev.ps1
│   └── build.ps1
│
└── docs/                     # Documentação
```

### Tecnologias

| Camada | Tecnologias |
|--------|-------------|
| **Frontend** | React 18, TypeScript, Vite, Tailwind CSS, Framer Motion, Zustand |
| **Desktop** | Tauri 2 (Rust), Webview2 |
| **Backend** | FastAPI, WebSockets, Uvicorn |
| **IA** | Anthropic SDK, OpenAI SDK, Ollama, HTTPX |
| **Voz** | Edge TTS, SpeechRecognition, PyAudio |
| **Automação** | PyAutoGUI, psutil, pycaw, WMI, Playwright |
| **Banco** | SQLite (arquivo único, sem servidor) |
| **APIs** | Spotify Web API, Brave/Playwright |

## ⚙️ Configuração Avançada

### Variáveis de Ambiente (backend/.env)

```env
# App
DEBUG=false
HOST=0.0.0.0
PORT=8000

# IA Provider: anthropic | openai | ollama | custom
ANTHROPIC_API_KEY=
OPENAI_API_KEY=
CUSTOM_API_KEY=
CUSTOM_API_BASE=

# Voice
WAKE_WORD=jarvis
WAKE_WORD_SENSITIVITY=0.5
VOICE_LANGUAGE=pt-BR
TTS_VOICE=pt-BR-ThalitaMultilingualNeural
TTS_RATE=1.0
TTS_PITCH=1.0

# Spotify
SPOTIFY_CLIENT_ID=
SPOTIFY_CLIENT_SECRET=
SPOTIFY_REDIRECT_URI=http://localhost:8000/auth/spotify/callback

# Brave (auto-detectado se padrão)
BRAVE_EXECUTABLE_PATH=

# Security
SECRET_KEY=gere-uma-chave-segura
ALLOWED_ORIGINS=http://localhost:5173,http://localhost:3000,tauri://localhost
```

### Modelos Suportados

**Anthropic:** `claude-3-5-sonnet-20241022`, `claude-3-5-haiku-20241022`, `claude-3-opus-20240229`

**OpenAI:** `gpt-4o`, `gpt-4o-mini`, `gpt-4-turbo`

**Ollama (Local):** `llama3.1`, `llama3.1:70b`, `mistral`, `codellama`, `phi3`

### Vozes TTS Disponíveis (Edge)
- `pt-BR-ThalitaMultilingualNeural` (padrão, feminina)
- `pt-BR-AntonioMultilingualNeural` (masculina)
- `en-US-AriaMultilingualNeural`
- `en-US-GuyMultilingualNeural`
- +400 vozes em https://aka.ms/edge-voices

## 🔒 Segurança

- **Chaves de API** — Armazenadas apenas no `.env` local, nunca no código
- **Comandos Perigosos** — Exigem confirmação explícita (desligar, excluir, admin)
- **Sanitização** — PowerShell commands filtrados (; & | removidos)
- **Memória Local** — SQLite no seu disco, nenhum dado na nuvem
- **CORS Restrito** — Origens permitidas configuráveis
- **Tauri** — Binário nativo com sandbox, sem Node.js no runtime

## 🐛 Troubleshooting

### Microfone não funciona
```powershell
# Verificar dispositivos de áudio
Get-PnpDevice -Class AudioEndpoint

# Permitir acesso ao microfone nas configurações do Windows
# Configurações > Privacidade > Microfone > Ativar
```

### Backend não inicia
```powershell
# Verificar porta 8000 livre
netstat -ano | findstr :8000

# Verificar venv
cd backend
.\venv\Scripts\Activate.ps1
python -m uvicorn app.main:app --reload
```

### Spotify não conecta
1. Verifique `SPOTIFY_CLIENT_ID` e `SPOTIFY_CLIENT_SECRET` no `.env`
2. Adicione `http://localhost:8000/auth/spotify/callback` no Dashboard do Spotify
3. Clique em "Conectar Spotify" nas configurações do JARVIS

### Build Tauri falha
```powershell
# Limpar cache
cd frontend/src-tauri
cargo clean

# Atualizar Rust
rustup update

# Reinstalar dependências
npm install
```

### Erro de módulo Python
```powershell
cd backend
.\venv\Scripts\pip install --upgrade pip
.\venv\Scripts\pip install -r requirements.txt --force-reinstall
```

## 📝 Roadmap

- [ ] **Plugins** — Sistema de extensões para novas integrações
- [ ] **WhatsApp/Telegram** — Integração via API oficial
- [ ] **Discord** — Bot com comandos de voz
- [ ] **Home Assistant** — Controle de casa inteligente
- [ ] **OCR** — Leitura de tela para automação visual
- [ ] **Multi-monitor** — Suporte a múltiplas telas
- [ ] **Backup/Sync** — Sincronização de configurações e memórias
- [ ] **Mobile Companion** — App React Native para controle remoto

## 🤝 Contribuindo

1. Fork o projeto
2. Crie uma branch: `git checkout -b feature/nova-funcionalidade`
3. Commit: `git commit -m 'Adiciona nova funcionalidade'`
4. Push: `git push origin feature/nova-funcionalidade`
5. Abra um Pull Request

## 📄 Licença

MIT License — veja [LICENSE](LICENSE) para detalhes.

## 🙏 Agradecimentos

- **Tony Stark** — Pela inspiração
- **Anthropic** — Pelo Claude
- **Tauri Team** — Pelo framework incrível
- **Edge TTS** — Pela síntese de voz natural
- **Comunidade Open Source** — Pelas bibliotecas usadas

---

<div align="center">
  <strong>J.A.R.V.I.S.</strong> — <em>Just A Rather Very Intelligent System</em>
</div>