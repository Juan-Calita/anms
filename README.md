# Anamnes.IA — Transcrever Aula

Ferramenta de transcrição e estruturação de aulas com IA (Claude da Anthropic).

## Estrutura

```
anamnes-ia/
├── public/
│   └── index.html     ← frontend React (standalone, sem build)
├── server.js          ← Express: serve o frontend + proxy da API Anthropic
├── package.json
├── render.yaml        ← configuração de deploy no Render
└── .gitignore
```

---

## 🚀 Deploy no Render (recomendado)

### 1. Suba o projeto no GitHub
```bash
git init
git add .
git commit -m "feat: Anamnes.IA — Transcrever Aula"
git remote add origin https://github.com/seu-usuario/anamnes-ia.git
git push -u origin main
```

### 2. Crie o serviço no Render
1. Acesse [render.com](https://render.com) → **New → Web Service**
2. Conecte seu repositório GitHub
3. O Render detecta o `render.yaml` automaticamente — confirme as configurações:
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
   - **Runtime:** Node

### 3. Configure a variável de ambiente
No painel do Render, vá em **Environment → Add Environment Variable**:
```
ANTHROPIC_API_KEY = sk-ant-xxxxxxxxxxxxxxxxxxxxxxxx
```

### 4. Deploy
Clique em **Deploy** — em ~2 minutos o site estará no ar em:
```
https://anamnes-ia.onrender.com
```

---

## Rodar localmente

```bash
# 1. Instale as dependências
npm install

# 2. Crie o .env
echo "ANTHROPIC_API_KEY=sk-ant-xxxx" > .env

# 3. Inicie o servidor
npm run dev

# Acesse: http://localhost:3001
```

---

## Como funciona

```
Navegador → POST /api/transcribe → server.js → API Anthropic (com a chave)
                                  ↑
                         A chave fica segura
                         no servidor, nunca
                         exposta no frontend
```

## Funcionalidades

- Upload de áudio (MP3, M4A, WAV) via `input_audio`
- Cola transcrição de texto direto
- Resumo estruturado: TLDR, pontos principais, capítulos, termos-chave, próximos passos
- Transcrição segmentada com timestamps
- Exportação para Markdown
- Histórico de sessão
- Design Anamnes.IA
