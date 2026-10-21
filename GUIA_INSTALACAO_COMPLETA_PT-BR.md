# Editonny — guia completo de instalação

Repositório oficial: https://github.com/soumatheusgomes/editonny

O Editonny edita vídeo localmente por conversa: remove pausas, erros e respirações, adiciona legendas, normaliza voz, reenquadra quando aprovado e pode inserir cenas de motion. Os vídeos não precisam ser enviados a um serviço externo para transcrição ou renderização.

## Antes de começar

- Use um computador local com internet estável e bastante espaço livre. Reserve ao menos **12 GB livres** para o ambiente, navegador de renderização, modelo local de transcrição, cache e projetos. Para vídeos longos, prefira 25 GB ou mais.
- Os vídeos originais devem ficar fora da pasta da instalação.
- Requisitos do Editonny nesta versão: Python 3.10 a 3.13, `uv`, FFmpeg/ffprobe, Node.js 22.13+ ou 24+ com `npx` e OCR local. No Windows/Linux, o OCR é o Tesseract.
- O setup baixa componentes de software e o modelo local de transcrição. Ele não envia seus vídeos para fora sem uma solicitação explícita.

## Caminho A — Codex (mais direto)

### 1. Instale o Codex

**macOS/Linux**

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

**Windows PowerShell**

```powershell
irm https://chatgpt.com/codex/install.ps1 | iex
```

Abra um novo terminal, entre em qualquer pasta de trabalho e rode:

```bash
codex
```

Faça login quando ele pedir.

### 2. Cole este pedido no Codex

```text
Instale ou atualize a skill editonny para Codex a partir de https://github.com/soumatheusgomes/editonny. Clone a versão mais recente em uma pasta temporária; eu não vou baixar nada manualmente. Leia skills/editonny/SKILL.md e siga o procedimento completo em skills/editonny/references/setup.md. Prepare ferramentas locais compatíveis, engine com dependências fixadas, renderizador e navegador na versão fixada, modelo padrão local de transcrição, OCR local para conferir legendas e mídia incluída antes da primeira edição. Verifique com diagnósticos, integridade de mídia, OCR e uma amostra sintética. Informe qualquer pendência, remova o clone temporário e me diga quando reiniciar o Codex. Peça autorização antes de serviços pagos ou envio das minhas mídias.
```

### 3. Reinicie e edite

Abra novamente o Codex e use:

```text
$editonny
Edite um vídeo vertical de 45 segundos da pasta <PASTA_DO_VIDEO>.
Remova pausas, respirações, erros e repetições sem cortar palavras completas.
Adicione legendas claras em português e revise uma amostra antes da exportação final.
```

O Editonny deve mostrar um cartão de configurações antes de editar. Responda `ok` ou ajuste o que quiser.

## Caminho B — Claude Code

### 1. Instale o Claude Code

**macOS/Linux**

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**Windows PowerShell**

```powershell
irm https://claude.ai/install.ps1 | iex
```

Abra um novo terminal e confirme:

```bash
claude --version
```

### 2. Inicie em uma pasta e cole este pedido

```bash
claude
```

```text
Instale ou atualize a skill editonny para Claude Code a partir de https://github.com/soumatheusgomes/editonny. Clone a versão mais recente em uma pasta temporária; eu não vou baixar nada manualmente. Leia skills/editonny/SKILL.md e siga o procedimento completo em skills/editonny/references/setup.md. Prepare ferramentas locais compatíveis, engine com dependências fixadas, renderizador e navegador na versão fixada, modelo padrão local de transcrição, OCR local para conferir legendas e mídia incluída antes da primeira edição. Verifique com diagnósticos, integridade de mídia, OCR e uma amostra sintética. Informe qualquer pendência, remova o clone temporário e me diga quando reiniciar o Claude Code. Peça autorização antes de serviços pagos ou envio das minhas mídias.
```

### 3. Reinicie e use

Depois do setup, abra um novo chat no Claude Code e digite:

```text
/editonny
Edite os vídeos da pasta <PASTA_DO_VIDEO> como um Reel 9:16 de até 45 segundos, com cortes naturais e legendas em português. Preserve as cores originais. Faça uma amostra de 10 segundos antes da exportação final.
```

## Caminho C — Google Antigravity

O Antigravity reconhece skills em `.agents/skills/`, padrão que o Editonny já usa.

### Opção rápida: CLI

**macOS/Linux**

```bash
curl -fsSL https://antigravity.google/cli/install.sh | bash
```

**Windows PowerShell**

```powershell
irm https://antigravity.google/cli/install.ps1 | iex
```

Abra um novo terminal e valide:

```bash
agy --version
```

Depois, clone e prepare a skill. No Windows, use os comandos equivalentes da seção PowerShell deste guia.

```bash
git clone https://github.com/soumatheusgomes/editonny.git
cd editonny
python3 install.py --target codex
```

> O instalador oficial registra Codex e Claude. Para Antigravity, exponha a skill do checkout criando o caminho `<SEU_WORKSPACE>/.agents/skills/editonny` apontando para `editonny/skills/editonny`, ou copie essa pasta inteira para esse local. Prefira link simbólico para acompanhar atualizações sem duplicar arquivos.

No terminal, entre no workspace e abra o agente:

```bash
agy
```

Peça: `Use a skill editonny para editar os vídeos da pasta <PASTA_DO_VIDEO>. Mostre as configurações antes de iniciar.`

### Opção visual: Antigravity App

1. Instale o aplicativo pelo site oficial do Google Antigravity.
2. Crie um projeto apontando para a pasta onde você clonou o Editonny.
3. Garanta que exista a pasta `.agents/skills/editonny/` dentro do workspace, contendo o `SKILL.md` e as subpastas do Editonny.
4. Abra o chat do projeto e peça a edição normalmente. A skill pode ser acionada automaticamente ou pelo comando `/editonny`, se aparecer na lista.

## Caminho D — instalação manual no PowerShell (Windows)

Abra o PowerShell **como administrador** apenas para instalar dependências do sistema. Para o resto, use o PowerShell normal.

### 1. Instale as ferramentas obrigatórias

```powershell
winget install Git.Git
winget install Python.Python.3.13
winget install OpenJS.NodeJS.LTS
winget install Gyan.FFmpeg
winget install UB-Mannheim.TesseractOCR
```

Feche e abra o PowerShell. Confirme:

```powershell
python --version
node --version
npm --version
npx --version
ffmpeg -version
tesseract --version
```

Instale o `uv`:

```powershell
irm https://astral.sh/uv/install.ps1 | iex
```

Feche e abra o PowerShell mais uma vez, então confirme:

```powershell
uv --version
```

### 2. Baixe o Editonny

```powershell
mkdir $HOME\StudioVideo -ErrorAction SilentlyContinue
cd $HOME\StudioVideo
git clone https://github.com/soumatheusgomes/editonny.git
cd editonny
```

### 3. Registre para o seu agente

Somente Codex:

```powershell
python install.py --target codex
```

Somente Claude Code:

```powershell
python install.py --target claude
```

Para os dois:

```powershell
python install.py --target both
```

> Se o Windows bloquear a criação de links, ative o **Modo de Desenvolvedor** em Configurações → Sistema → Para desenvolvedores, e rode de novo. Alternativamente, abra o PowerShell como administrador para esse passo.

### 4. Prepare motor, navegador e OCR

```powershell
uv sync --locked --directory "$HOME\.local\share\editonny\engine"
npx --yes hyperframes@0.8.179 --help
npx --yes hyperframes@0.8.179 browser ensure
npx --yes hyperframes@0.8.179 doctor --json
```

No Windows, a pasta de instalação pode diferir. Se `$HOME\.local\share\editonny` não existir, use a pasta clonada no comando de `uv`, por exemplo:

```powershell
uv sync --locked --directory "$HOME\StudioVideo\editonny\skills\editonny\engine"
```

### 5. Verifique tudo

```powershell
python "$HOME\.local\share\editonny\scripts\editonny.py" doctor --json
python "$HOME\.local\share\editonny\scripts\editonny.py" doctor --probe-media --json
python "$HOME\.local\share\editonny\scripts\editonny.py" media status --json
```

Se a instalação estiver na pasta clonada, troque o caminho acima por:

```powershell
python "$HOME\StudioVideo\editonny\skills\editonny\scripts\editonny.py" doctor --json
python "$HOME\StudioVideo\editonny\skills\editonny\scripts\editonny.py" doctor --probe-media --json
python "$HOME\StudioVideo\editonny\skills\editonny\scripts\editonny.py" media status --json
```

Depois use o agente escolhido e solicite uma edição.

## Checagem obrigatória para legendas no Windows/Linux

O Tesseract precisa ter ao menos o idioma inglês (`eng`) disponível. Confira:

```powershell
tesseract --list-langs
```

Se `eng` não aparecer, reinstale o Tesseract com o pacote de idiomas. Para legendas em português, é recomendado também instalar `por`, mas o verificador do Editonny aceita a rota `eng`.

## Primeiro pedido recomendado

Depois do setup completo, deixe os vídeos em uma pasta única e faça um pedido específico:

```text
Edite os arquivos da pasta <PASTA_DO_VIDEO> em um Reel vertical de até 45 segundos.
Remova erros, falsos começos, respirações audíveis e pausas desnecessárias, mas preserve palavras completas, sentido e ritmo natural.
Adicione legendas claras em português, sem música, sem filtros e sem mudar as cores.
Mostre as configurações e espere minha confirmação. Depois, gere uma amostra de 8 a 15 segundos antes da versão final.
```

## Onde ficam os resultados

Por padrão, cada trabalho fica em `Downloads/editonny/data-titulo/`:

- `exports/`: MP4 final e legendas, quando solicitadas.
- `project/`: arquivos do projeto para revisão.
- O vídeo original não é substituído.

## Solução rápida de problemas

| Problema | Ação |
|---|---|
| `uv not found` | Feche e abra o terminal; rode `uv --version`. Reinstale pelo site do Astral se necessário. |
| `npx not found` | Instale Node.js 22.13+ ou 24+; não use apenas Node 20. |
| `Python engine missing` | Rode `uv sync --locked --directory <PASTA>/skills/editonny/engine`. |
| Legendas não validam | Instale/ajuste Tesseract e confirme `tesseract --list-langs`. |
| Render falha | Rode `doctor --probe-media --json` e mantenha FFmpeg no PATH. |
| Falta de espaço | Libere espaço antes do setup; modelo, browser, cache e renderização podem ocupar vários GB. |
| Links no Windows falham | Ative Modo de Desenvolvedor ou execute o registro como administrador. |

## Atualização segura

Não atualize dependências isoladamente. Para atualizar, abra Codex ou Claude Code e peça para comparar a versão instalada com o repositório oficial, resumir as mudanças e só aplicar depois da sua aprovação. A origem correta é sempre:

```text
https://github.com/soumatheusgomes/editonny
```