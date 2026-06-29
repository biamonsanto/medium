# Do Terminal ao Deus da Máquina: O Guia Definitivo para Dominar o Claude Code em 2026

> **"73% dos times de engenharia já usam ferramentas de IA diariamente. Os 27% restantes estão prestes a ser varridos."**
> — Pragmatic Engineer Survey, 15.000 devs, Fevereiro de 2026

---

Você provavelmente já ouviu falar do Claude Code. Talvez já o tenha instalado. Talvez o use para corrigir um bug aqui, gerar um componente ali.

Mas, se você está usando o Claude Code apenas para isso, está usando 10% da ferramenta.

Este artigo existe para mostrar os outros 90%. Do básico absoluto até o nível em que o Claude trabalha enquanto você dorme — sem o seu computador ligado.

São 10 níveis. Cada um multiplica o anterior.

---

![Os 10 Níveis de Domínio do Claude Code](https://raw.githubusercontent.com/biamonsanto/medium/main/images/01-10-levels.png)

*Onde você está nessa escala agora? Ao final deste artigo, você vai saber onde quer chegar.*

---

## Primeiro: Os Números que Justificam Seu Tempo

Antes de entrar nos detalhes técnicos, um contexto rápido sobre por que isso importa:

- **46% dos devs** nomeiam Claude Code como sua ferramenta "mais amada" — mais que o dobro do Cursor (19%) e 5x o GitHub Copilot (9%)
- Desenvolvedores no quartil superior economizam **5 a 8 horas por semana**
- Redução de **92% no tempo médio** de conclusão de tarefas complexas
- **29 milhões de instalações diárias** da extensão VS Code em Junho de 2026 (eram 17,7M em Janeiro)

Mas esses números só se materializam para quem entende a ferramenta de verdade. Não basta instalar.

Fontes: [Claude Code Statistics 2026](https://serpsculpt.com/claude-code-usage-statistics/) · [Developer Survey](https://claude5.ai/news/developer-survey-2026-ai-coding-73-percent-daily) · [Faros AI ROI Analysis](https://www.faros.ai/blog/how-to-measure-claude-code-roi-developer-productivity-insights-with-faros-ai)

---

# NÍVEL 1 — Terminal: Onde Tudo Começa

## Instalando e abrindo pela primeira vez

```bash
npm install -g @anthropic-ai/claude-code
cd seu-projeto
claude
```

Pronto. Você está dentro. Mas o que acontece agora?

## O que Claude Code realmente faz por baixo dos panos

Quando você manda uma mensagem, o Claude não apenas "responde". Ele entra em um loop agêntico:

![O Loop Agêntico do Claude Code](https://raw.githubusercontent.com/biamonsanto/medium/main/images/02-agentic-loop.png)

Observe o diagrama. O Claude **pensa → age → observa → decide se terminou → repete**. Ele pode ler 20 arquivos, rodar 5 comandos e editar 3 funções antes de dar a você uma resposta final. Tudo isso automaticamente.

É diferente de um chatbot. O Claude é um agente.

## Como aproveitar o Nível 1 de verdade

**Ruim** (como a maioria usa):
```
"melhore meu código de autenticação"
```

**Bom** (como você deve usar):
```
"O endpoint POST /api/auth/login em src/api/auth.ts está retornando 
401 intermitente. O problema parece estar na validação do token JWT. 
Leia o arquivo, identifique o bug e corrija."
```

A diferença? Especificidade. O Claude é um desenvolvedor sênior — ele precisa de contexto, não de ordens vagas.

**O que Claude enxerga automaticamente:**
- Toda a estrutura de pastas do projeto
- Conteúdo dos arquivos (com permissão)
- Output de comandos shell
- `git diff`, `git log`, `git status`
- Erros de compilação e testes

## Exercício do Nível 1

Abra seu projeto atual e mande essa mensagem:

```
Leia os últimos 5 commits do git log e me dê um resumo do que 
mudou no projeto recentemente. Depois, identifique qual arquivo 
tem o maior número de TODOs pendentes.
```

Observe o Claude ler o git log, varrer os arquivos e dar a você uma análise real. Isso já é diferente de qualquer copiloto que você usou antes.

---

# NÍVEL 2 — Memory: O Cérebro que Não Esquece

## O problema que a memória resolve

Sem memória, toda sessão começa do zero. O Claude não sabe que você usa TypeScript strict, que não quer comentários em inglês, nem que a pasta `/lib/auth` é crítica e não deve ser mexida.

Você repete essas instruções toda vez. Isso é desperdício.

A solução é o **CLAUDE.md**.

## Os 4 níveis de memória

![Hierarquia de Memória do CLAUDE.md](https://raw.githubusercontent.com/biamonsanto/medium/main/images/03-claude-md-hierarchy.png)

São 4 locais, cada um com escopo diferente. Do mais amplo ao mais específico:

**1. Global** (`~/.claude/CLAUDE.md`) — vale em todos os projetos:
```markdown
# Minhas Preferências Pessoais

- Prefiro código conciso sobre verbose
- Sempre use português nos comentários
- Explique decisões de arquitetura não óbvias
- Prefiro `const` sobre `let` quando possível
```

**2. Projeto** (`./CLAUDE.md` na raiz) — regras deste projeto:
```markdown
# Projeto: SaaS Financeiro para PMEs

## Stack
Next.js 15, TypeScript strict, PostgreSQL, Prisma, tRPC

## Regras Absolutas (nunca quebre)
- NUNCA use `any` em TypeScript — use `unknown` e narrowing
- SEMPRE escreva testes para funções de negócio
- Transações financeiras precisam de retry logic
- Logs de erro incluem `correlation_id` obrigatoriamente

## Arquitetura
- Lógica de negócio SEMPRE em /lib/services/ — nunca nos componentes
- Componentes de UI em /components/ui/ (shadcn)
- API Routes em /app/api/

## O Que NÃO Mexer Sem Perguntar
- /lib/auth/ — sistema crítico de autenticação
- /prisma/migrations/ — somente via `prisma migrate`
- Qualquer arquivo .env
```

**3. Pasta** (`./frontend/CLAUDE.md`) — perfeito para monorepos:
```markdown
# Regras do Frontend

- Componentes: arrow functions, sem class components
- Styling: Tailwind only, sem CSS modules
- Estado global: Zustand (decidido em 2026-03-15, não mude para Redux)
```

**4. Sessão** (via `/memory`) — para decisões do dia:
```
/memory
```
Abre seu editor. Você adiciona:
```markdown
## Decisão — 2026-06-28

Migrando o módulo de pagamentos de Stripe v3 para v4. 
A mudança é breaking em webhooks — checar /lib/webhooks/ com cuidado.
```
Na próxima sessão, o Claude lembra.

## A regra mais importante da memória

> **Se algo é importante para o projeto, coloca no CLAUDE.md. Não confie na memória da conversa.**

Quando o contexto fica grande, o Claude compacta automaticamente a conversa. O que está no CLAUDE.md **sobrevive** à compactação. O que está só no chat, não.

## Exercício do Nível 2

```bash
claude
/init
```

O `/init` analisa seu projeto e gera um CLAUDE.md inicial. Revise, adicione suas regras reais e salve. A partir daí, toda sessão começa com o Claude já sabendo as regras do seu jogo.

---

# NÍVEL 3 — Commands: Slash Commands que Mudam Tudo

## O que são

Slash commands são atalhos que você digita diretamente na sessão. Começam com `/`, executam imediatamente.

## Os comandos nativos que você precisa saber hoje

| Comando | O que faz | Quando usar |
|---------|-----------|-------------|
| `/compact` | Compacta o contexto sem perder memórias | Sessão longa, qualidade caindo |
| `/plan` | Claude propõe plano antes de agir | Tarefas complexas, mudanças grandes |
| `/review` | Code review com contexto limpo | Antes de abrir um PR |
| `/cost` | Mostra tokens e custo da sessão | Monitorar uso |
| `/clear` | Zera o contexto completamente | Recomeçar sem viés |
| `/memory` | Abre seus arquivos de memória | Adicionar decisões importantes |
| `/init` | Gera CLAUDE.md analisando o projeto | Setup inicial |

**Dica real:** Use `/plan` antes de qualquer refactoring grande. O Claude vai listar o que pretende fazer — você aprova ou ajusta antes que ele mexa em qualquer arquivo.

```
/plan
Preciso migrar o sistema de auth de JWT stateless para 
JWT + refresh tokens com Redis. Qual seria o plano?
```

O Claude vai responder com um plano detalhado, pedir sua aprovação e só então executar. Isso evita surpresas em código crítico.

## Criando seus próprios slash commands

Crie uma pasta e um arquivo:

```bash
mkdir -p .claude/commands
```

**`.claude/commands/deploy-check.md`:**
```markdown
Execute esta checklist ANTES de qualquer deploy:

1. Rode `npm run test` — todos os testes devem passar
2. Rode `npm run lint` — zero erros
3. Verifique se há variáveis de ambiente hardcoded no diff atual
4. Confirme que não há `console.log` de debug no código
5. Verifique se CHANGELOG.md foi atualizado

Se algum item falhar, liste o que precisa ser corrigido. 
Não aprove o deploy se houver falhas.
```

Agora você tem:
```
/deploy-check
```

Um comando que faz toda a checklist automaticamente. Tempo que você perdia manualmente: 15-20 minutos. Agora: 45 segundos.

## Commands com variáveis

```markdown
<!-- .claude/commands/bug-analysis.md -->
Analise o seguinte bug report:

Bug: $ARGUMENTS

Faça:
1. Identifique a causa raiz provável
2. Liste os arquivos que provavelmente precisam mudança
3. Estime a complexidade: baixa / média / alta
4. Proponha o plano de correção em passos numerados
```

Uso:
```
/bug-analysis Usuários recebem 401 intermitente após login bem-sucedido no mobile
```

## O novo formato: Skills (recomendado em 2026)

A Anthropic atualizou o padrão. Em vez de `.claude/commands/`, use `.claude/skills/<nome>/SKILL.md`:

```
.claude/skills/
  deploy-check/
    SKILL.md
  bug-analysis/
    SKILL.md
    severity-matrix.json   ← pode ter arquivos de suporte
```

A grande vantagem: o Claude pode invocar skills **autonomamente** quando a tarefa corresponde à descrição — sem que você precise chamá-las manualmente.

---

# NÍVEL 4 — Custom: Configuração que Controla Tudo

## O arquivo que governa o comportamento

`.claude/settings.json` controla permissões, modelo, hooks e MCPs. É o arquivo mais poderoso do seu setup.

```json
{
  "model": "claude-opus-4-8",
  "permissions": {
    "allow": [
      "Bash(npm run *)",
      "Bash(git diff*)",
      "Bash(git log*)",
      "Bash(git status)",
      "Bash(git add *)",
      "Bash(git commit *)",
      "Read(**/*)",
      "Edit(src/**/*)"
    ],
    "deny": [
      "Bash(rm -rf*)",
      "Bash(git push --force*)",
      "Write(.env*)",
      "Write(prisma/migrations/*)"
    ]
  }
}
```

## Por que permissões explícitas importam

Sem o `deny` de `rm -rf`, o Claude tecnicamente poderia executar esse comando se entendesse que é necessário para a tarefa. Com o deny, é impossível — nem que você peça.

Pense nas permissões como um contrato: "O Claude pode fazer A, B, C. O Claude **nunca** faz X, Y, Z."

## Escolhendo o modelo certo

| Modelo | Melhor para | Custo relativo |
|--------|-------------|----------------|
| `claude-opus-4-8` | Arquitetura complexa, refactoring grande, análise de sistemas | $$$ |
| `claude-sonnet-4-6` | Uso diário, bugs, features novas | $$ |
| `claude-haiku-4-5` | Tarefas simples, geração de testes, documentação | $ |

**Dica:** Configure Opus para projetos críticos, Sonnet para projetos do dia a dia. A diferença de qualidade em tarefas complexas é significativa.

## Variáveis de ambiente seguras

```json
{
  "env": {
    "DATABASE_URL": "postgresql://localhost:5432/dev",
    "NODE_ENV": "development"
  }
}
```

O Claude usa essas variáveis. Mas veja o que está no `deny`:
```json
"deny": ["Read(.env.production)", "Write(.env*)"]
```

Claude nunca lê seu `.env.production` e nunca escreve em arquivos `.env`. Credenciais de produção ficam fora do alcance.

---

# NÍVEL 5 — Skills: Workflows com Memória e Lógica Real

## Skills vs. Comandos simples

Um comando simples é um prompt. Uma Skill é um workflow com contexto, arquivos de suporte e detecção automática.

```
.claude/skills/pr-review/
  SKILL.md              ← o workflow
  review-criteria.json  ← critérios específicos do projeto
  templates/
    comment-template.md ← template para comentários no PR
```

## Uma Skill de PR Review real

**`.claude/skills/pr-review/SKILL.md`:**
```markdown
---
name: pr-review
description: Code review completo de PR — verifica bugs, segurança, 
             performance e padrões do projeto
---

# PR Review

## Processo

1. Leia o diff completo do PR atual
2. Para cada problema encontrado, classifique:
   - **BLOCKER**: deve ser corrigido antes do merge
   - **SUGGESTION**: melhoria recomendada
   - **NITPICK**: detalhe menor, não bloqueia

3. Verifique especialmente:
   - Código de negócio sem testes → sempre BLOCKER
   - XSS, SQL injection, credenciais expostas → sempre BLOCKER
   - N+1 queries em hot paths → BLOCKER
   - Violações do ESLint → SUGGESTION

4. Use os critérios em `review-criteria.json`

5. Conclua com: **APPROVE** | **REQUEST CHANGES** | **NEEDS DISCUSSION**

## Formato da Resposta

Para cada problema:
**[BLOCKER]** `src/api/auth.ts:47` — Token não está sendo invalidado no logout.
*Correção:* Adicione `await redis.del(token)` antes do retorno.
```

**`.claude/skills/pr-review/review-criteria.json`:**
```json
{
  "critical": [
    "Transações financeiras sem retry",
    "Queries sem parameterização",
    "Secrets em código-fonte",
    "Endpoints sem autenticação"
  ],
  "important": [
    "Funções com mais de 50 linhas sem teste",
    "any em TypeScript",
    "console.log em produção"
  ]
}
```

Quando você digita `/pr-review`, o Claude carrega o workflow **e** os arquivos de suporte — o review usa seus critérios reais, não critérios genéricos.

## Skills de onboarding

Uma das melhores aplicações: padronizar como o time implementa features.

```markdown
---
name: new-feature
description: Implementa uma nova feature seguindo os padrões do projeto
---

# Nova Feature — Passo a Passo

**Entrada:** nome e descrição da feature

## Passo 1 — Tipos primeiro
Crie os tipos em `/types/`. Toda feature começa com TypeScript bem definido.

## Passo 2 — Service depois
Implemente a lógica em `/lib/services/`. Nunca nos componentes.

## Passo 3 — API Route
Siga o padrão RESTful de `/app/api/`. Veja exemplos existentes.

## Passo 4 — Componentes
Use os componentes base de `/components/ui/`. Não reinvente.

## Passo 5 — Testes (obrigatório)
- Unit test para o service
- Integration test para a API route
- Se for fluxo crítico: E2E test

## Passo 6 — Docs
Adicione a feature em `docs/features/`. Uma linha descrevendo o que faz.
```

Todo dev novo do time faz `/new-feature` e segue o mesmo fluxo. Sem surpresas, sem "mas eu fiz diferente".

---

# NÍVEL 6 — MCP: Claude Conectado ao Mundo Real

## O que é MCP

MCP (Model Context Protocol) é o protocolo aberto que permite que o Claude se conecte a sistemas externos: GitHub, bancos de dados, Slack, Linear, browsers, deploys — qualquer coisa.

Sem MCP: o Claude vive dentro do terminal, isolado do mundo.
Com MCP: o Claude é um orquestrador que controla seus sistemas.

![Arquitetura MCP — Claude Conectado ao Mundo](https://raw.githubusercontent.com/biamonsanto/medium/main/images/04-mcp-architecture.png)

## Configurando seus primeiros MCPs

No `.claude/settings.json`:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
      }
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "POSTGRES_CONNECTION_STRING": "${DEV_DATABASE_URL}"
      }
    }
  }
}
```

Reinicie o Claude Code. Agora você pode:

```
Leia a issue #412 no GitHub, entenda o problema, 
consulte os dados afetados no banco, implemente a 
correção e abra um PR com uma descrição completa.
```

O Claude faz tudo isso, sem você precisar copiar e colar entre janelas.

## Os MCPs mais úteis em 2026

**GitHub MCP** — o mais importante:
```
Revise todos os PRs abertos há mais de 7 dias 
e poste um comentário pedindo atualização
```
```
Crie issues no GitHub para cada TODO com mais de 30 dias no código
```

**Database MCP** — análise direta no banco de dev:
```
Identifique as 5 queries mais lentas do último dia 
e sugira índices para otimizá-las
```
```
Gere 500 usuários realistas para o banco de dev com dados brasileiros
```

**Browser/Playwright MCP** — testes visuais:
```
Abra a aplicação em localhost:3000, faça login com 
test@example.com / senha123 e verifique se o 
dashboard carrega sem erros no console
```

**Slack MCP** — comunicação automática:
```
Poste no canal #deployments: "Deploy v2.4.1 iniciado. 
Principais mudanças: [leia o CHANGELOG e resuma em 3 bullets]"
```

## O workflow que economiza 2 horas por tarefa

Sem MCP:
1. Você lê a issue manualmente (5 min)
2. Você busca os arquivos relevantes (10 min)
3. Você implementa (60 min)
4. Você escreve o PR (15 min)
5. Você avisa o time no Slack (5 min)
**Total: ~95 minutos**

Com MCP:
1. Você manda: *"Resolva a issue #412 e avise o time"*
2. O Claude faz tudo em paralelo
**Total: ~12 minutos**

Fontes: [Claude Code Advanced Patterns — PDF Anthropic](https://resources.anthropic.com/hubfs/Claude%20Code%20Advanced%20Patterns_%20Subagents,%20MCP,%20and%20Scaling%20to%20Real%20Codebases.pdf)

---

# NÍVEL 7 — Subagents: Times de IA em Paralelo

## O problema que subagents resolvem

A janela de contexto tem limite. Em uma sessão longa, o Claude começa a "esquecer" detalhes do início. E, quando o mesmo agente que escreveu o código faz o review, ele tem viés — sabe por que fez cada escolha.

Subagents resolvem os dois problemas: **distribuem o trabalho** e **isolam o contexto**.

![Padrão de Subagents em Paralelo](https://raw.githubusercontent.com/biamonsanto/medium/main/images/06-subagents-pattern.png)

## Como funciona na prática

Você pede ao agente principal algo grande. Ele divide o trabalho:

```
Preciso refatorar o módulo de autenticação para suportar 
OAuth2 além do login por email. Use subagents.
```

Claude automaticamente vai:
1. Criar um subagent para **analisar dependências** do módulo atual
2. Criar um subagent para **implementar OAuth2**
3. Criar um subagent para **escrever os testes**
4. Criar um subagent de **review** com contexto limpo (sem viés)
5. Integrar os resultados e resolver conflitos

Cada subagent tem seu próprio contexto isolado. O agente principal só recebe o resumo do trabalho — não o contexto verboso inteiro.

## O insight contra-intuitivo sobre reviews

**Reviews são melhores com contexto fresco.**

Quando o mesmo agente que escreveu o código faz o review, ele "vê" o que deveria estar lá, não o que está. Um subagent de review que nunca viu o código — só o diff — é 40-60% mais rigoroso.

```
/review
```

O `/review` nativo do Claude Code já usa esse princípio: abre um contexto novo para fazer a review sem viés do que foi desenvolvido na sessão.

## Quando usar (e quando não usar)

**Use subagents quando:**
- A tarefa tem partes independentes que podem ser feitas em paralelo
- Você quer review sem viés
- O contexto principal está ficando muito grande
- Precisa de "especialistas" diferentes (segurança, performance, testes)

**Não use quando:**
- A tarefa é linear e simples
- Os passos dependem uns dos outros sequencialmente
- O overhead de coordenação > ganho de velocidade

A regra prática: comece com um agente. Adicione subagents só quando sentir a necessidade concreta.

---

# NÍVEL 8 — Hooks: Automação com Segurança Embutida

## O que são hooks

Hooks são scripts shell que executam automaticamente em resposta a eventos do Claude Code. São o middleware do seu workflow.

![Fluxo de Execução dos Hooks](https://raw.githubusercontent.com/biamonsanto/medium/main/images/05-hooks-flow.png)

Observe o fluxo: o Claude quer agir → seu hook verifica → se retornar `exit 1`, a ação é **bloqueada**; se retornar `exit 0`, ela prossegue → o hook pós-ação executa.

## Configurando hooks no settings.json

```json
{
  "hooks": {
    "PreToolUse": [{
      "matcher": "Bash",
      "hooks": [{
        "type": "command",
        "command": ".claude/hooks/safety-check.sh"
      }]
    }],
    "PostToolUse": [{
      "matcher": "Edit",
      "hooks": [{
        "type": "command",
        "command": "npx eslint $CLAUDE_TOOL_FILE --fix --quiet 2>&1 | head -10"
      }]
    }],
    "Stop": [{
      "hooks": [{
        "type": "command",
        "command": ".claude/hooks/test-check.sh"
      }]
    }]
  }
}
```

## Os 5 hooks que todo projeto deveria ter

### 1. Bloqueio de comandos perigosos (PreToolUse)

```bash
#!/bin/bash
# .claude/hooks/safety-check.sh
HOOK_INPUT=$(cat)
COMMAND=$(echo "$HOOK_INPUT" | jq -r '.tool_input.command // ""')

BLOCKED=("rm -rf /" "rm -rf ~" "git push --force" "DROP TABLE" "DELETE FROM")
for pattern in "${BLOCKED[@]}"; do
  if echo "$COMMAND" | grep -qi "$pattern"; then
    echo "BLOQUEADO: '$pattern' não é permitido." >&2
    exit 1
  fi
done
exit 0
```

### 2. Lint automático após toda edição (PostToolUse)

```bash
#!/bin/bash
HOOK_INPUT=$(cat)
FILE=$(echo "$HOOK_INPUT" | jq -r '.tool_input.file_path // ""')

if [[ "$FILE" =~ \.(ts|tsx|js|jsx)$ ]]; then
  npx eslint "$FILE" --fix --quiet 2>&1
fi
```

Todo arquivo editado pelo Claude passa pelo lint automaticamente. Zero violações acumuladas.

### 3. Testes obrigatórios antes de encerrar (Stop)

```bash
#!/bin/bash
# .claude/hooks/test-check.sh
echo "Verificando testes antes de encerrar..."
npm run test -- --passWithNoTests 2>&1 | tail -5
if [ ${PIPESTATUS[0]} -ne 0 ]; then
  echo "ATENÇÃO: Testes falhando. Sessão bloqueada." >&2
  exit 1
fi
echo "✓ Testes passando."
```

O Claude não pode encerrar uma sessão com testes quebrados. Ponto.

### 4. Detecção de secrets (PreToolUse em Write)

```bash
#!/bin/bash
HOOK_INPUT=$(cat)
CONTENT=$(echo "$HOOK_INPUT" | jq -r '.tool_input.content // ""')

if echo "$CONTENT" | grep -qE "(sk-|pk_live_|aws_secret|private_key|password\s*=\s*['\"][^'\"]{8,})"; then
  echo "BLOQUEADO: Possível secret detectado no conteúdo." >&2
  exit 1
fi
```

### 5. Notificação de conclusão (Stop)

```bash
#!/bin/bash
# Notifica quando Claude termina uma tarefa longa
if [[ "$OSTYPE" == "darwin"* ]]; then
  osascript -e 'display notification "Tarefa concluída!" with title "Claude Code"'
elif [[ "$OSTYPE" == "linux-gnu"* ]]; then
  notify-send "Claude Code" "Tarefa concluída!"
fi
```

Perfeito para quando você delega uma tarefa grande e vai fazer outra coisa.

## Proteção de branches (PreToolUse)

```bash
#!/bin/bash
HOOK_INPUT=$(cat)
CMD=$(echo "$HOOK_INPUT" | jq -r '.tool_input.command // ""')

if echo "$CMD" | grep -q "git commit"; then
  BRANCH=$(git branch --show-current)
  for protected in main master production staging; do
    if [[ "$BRANCH" == "$protected" ]]; then
      echo "BLOQUEADO: Commits diretos em '$BRANCH' não são permitidos." >&2
      exit 1
    fi
  done
fi
```

Claude nunca vai commitar direto na main. Mesmo que você peça.

---

# NÍVEL 9 — Headless: Claude sem Interface

## O que é modo headless

Headless é Claude Code rodando sem interface interativa — sem terminal visual, sem perguntas, sem confirmações. Você passa um prompt via `-p` e ele executa até completar.

```bash
claude -p "Analise o diretório /src e gere um relatório de complexidade"
```

## Para que serve na prática

| Contexto | Exemplo |
|----------|---------|
| CI/CD | Review automático em todo PR |
| Scripts | Gerar changelog de cada release |
| Cron jobs | Auditoria de segurança noturna |
| Pré-commit | Validação de qualidade antes do commit |

## Integrando no GitHub Actions

```yaml
# .github/workflows/claude-review.yml
name: Claude Security Review

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  security-review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - run: npm install -g @anthropic-ai/claude-code

      - name: Claude Security Scan
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: |
          DIFF=$(git diff origin/main...HEAD)
          
          RESULT=$(claude -p "
          Você é um especialista em segurança. Analise este diff.
          Retorne APENAS um JSON: 
          {\"vulnerabilities\": [{\"file\": \"...\", \"line\": 0, \"severity\": \"critical|high\", \"description\": \"...\"}]}
          Se não houver vulnerabilidades: {\"vulnerabilities\": []}
          
          Diff: $DIFF
          ")
          
          CRITICAL=$(echo "$RESULT" | jq '[.vulnerabilities[] | select(.severity == "critical")] | length')
          
          if [ "$CRITICAL" -gt 0 ]; then
            echo "❌ $CRITICAL vulnerabilidade(s) crítica(s)!"
            echo "$RESULT" | jq '.vulnerabilities[] | select(.severity == "critical")'
            exit 1
          fi
          echo "✅ Sem vulnerabilidades críticas"
```

## Script de changelog automático

```bash
#!/bin/bash
# generate-changelog.sh
VERSION=$1
PREV_TAG=$2

COMMITS=$(git log --oneline $PREV_TAG..HEAD)

claude -p "
Baseado nos commits abaixo, gere um CHANGELOG.md para a versão $VERSION.
Categorize em: ✨ Features, 🐛 Bug Fixes, ⚡ Performance, 💥 Breaking Changes.
Use linguagem clara para usuários finais — não linguagem de dev.
Retorne apenas o Markdown, sem explicações.

Commits:
$COMMITS
" > "CHANGELOG-$VERSION.md"

echo "Changelog gerado: CHANGELOG-$VERSION.md"
```

## Pré-commit hook com Claude

```bash
#!/bin/bash
# .git/hooks/pre-commit

DIFF=$(git diff --cached)

RESULT=$(claude -p "
Analise este diff de commit. Verifique:
1. Há console.log ou debugger esquecidos?
2. Há credenciais ou secrets expostos?
3. Há TODO/FIXME recém-adicionados (não pré-existentes)?

Retorne JSON: {\"pass\": true/false, \"issues\": [\"...\"]}}
Se pass=false, o commit será bloqueado.

Diff: $DIFF
")

PASS=$(echo "$RESULT" | jq -r '.pass')

if [ "$PASS" != "true" ]; then
  echo "❌ Claude bloqueou o commit:"
  echo "$RESULT" | jq -r '.issues[]' | sed 's/^/  - /'
  exit 1
fi

echo "✅ Commit aprovado pelo Claude"
```

---

# NÍVEL 10 — Routines: O Claude que Trabalha Enquanto Você Dorme

## O que são Routines

Routines são a forma mais avançada. Automações cloud-hosted, com schedule, que executam **sem você estar presente** — sem terminal aberto, sem computador ligado.

![Routines — Automação 24/7](https://raw.githubusercontent.com/biamonsanto/medium/main/images/07-routines-scheduler.png)

Uma Routine é configurada uma vez e depois trabalha sozinha. No schedule. Na nuvem. Com os resultados esperando quando você acordar.

## 4 Routines que todo time de engenharia deveria ter

### Routine 1: Auditoria de Segurança Diária

```yaml
# .claude/routines/daily-security.yaml
name: daily-security-audit
schedule: "0 6 * * *"    # Todo dia às 06:00
model: claude-opus-4-8
connectors: [github, slack]
permissions:
  allow: [github:read:*, github:issues:write, slack:post:#security-alerts]
  deny: [github:push:*, github:pr:merge]
```

**Prompt:**
```
Faça uma varredura de segurança no repositório:
1. `npm audit` — liste vulnerabilidades high/critical
2. Procure por secrets hardcoded (regex: sk-, pk_live_, aws_secret, password=)
3. Verifique endpoints sem middleware de autenticação
4. Identifique queries SQL com concatenação de strings

Se encontrar algo crítico: crie uma issue no GitHub com label "security".
Envie resumo no Slack #security-alerts.
Se nada crítico: apenas log no Slack "✅ Auditoria limpa."
```

### Routine 2: Atualização de Dependências Semanais

```yaml
name: weekly-dep-update
schedule: "0 9 * * 1"   # Toda segunda às 09:00
connectors: [github]
permissions:
  allow: [github:read:*, github:pr:create, github:push:deps/*]
  deny: [github:pr:merge, github:push:main]
```

**Prompt:**
```
Verifique as dependências do projeto:
1. Rode `npm outdated` e liste o que está desatualizado
2. Para cada atualização: verifique se é patch/minor (seguro) ou major (breaking)
3. Atualize as dependências patch e minor automaticamente
4. Crie um PR com branch "deps/auto-update-YYYY-MM-DD"
5. No PR, liste o que foi atualizado e destaque se alguma tem breaking changes
6. Deixe as major versions para revisão manual com um comentário explicando
```

### Routine 3: Monitor de PRs (Webhook)

```yaml
name: pr-review-bot
trigger: github:pr:opened    # Dispara a cada novo PR
connectors: [github]
permissions:
  allow: [github:read:*, github:pr:comment]
  deny: [github:pr:merge, github:pr:approve]
```

**Prompt:**
```
Faça code review do PR recém-aberto:
1. Analise o diff completo
2. Verifique contra os critérios em .claude/skills/pr-review/review-criteria.json
3. Classifique cada problema: BLOCKER | SUGGESTION | NITPICK
4. Poste os comentários inline no PR (nos arquivos e linhas corretos)
5. Poste um comment resumo com: total de issues, recomendação (APPROVE/REQUEST CHANGES)
6. NUNCA aprove automaticamente — deixe sempre para o humano aprovar
```

### Routine 4: Health Report Quinzenal

```yaml
name: code-health-report
schedule: "0 10 1,15 * *"  # Dias 1 e 15 do mês às 10:00
connectors: [github, slack]
```

**Prompt:**
```
Gere um relatório de saúde do código:
1. Funções com complexidade ciclomática > 10 (candidatos a refactoring)
2. Arquivos com > 400 linhas (candidatos a splitting)
3. TODOs com mais de 30 dias (dívida técnica acumulada)
4. Módulos com cobertura de testes < 60%
5. Dead code: funções exportadas sem consumidores

Formato: relatório Markdown com prioridades.
Poste no Slack #engenharia e crie uma issue de rastreamento no GitHub.
```

## A regra de ouro das Routines

> **Permissões mínimas. Nunca dê acesso de escrita em produção. Nunca merge automático. Routine sugere → humano decide.**

Uma Routine que roda 24/7 sem supervisão tem escopo de dano maior que uma sessão interativa. Configure com cuidado:

```json
"permissions": {
  "deny": [
    "github:pr:merge",
    "github:push:main",
    "github:push:production",
    "github:delete:*",
    "aws:*",
    "Write(.env*)"
  ]
}
```

---

# Juntando Tudo: O Setup do Dev Nível 10

Aqui está a estrutura completa de um projeto com todos os 10 níveis configurados:

```
meu-projeto/
├── CLAUDE.md                      ← Regras do projeto (Nível 2)
├── .claude/
│   ├── settings.json             ← Permissões, modelo, hooks, MCPs (Nível 4)
│   ├── skills/
│   │   ├── pr-review/            ← Review com critérios do projeto (Nível 5)
│   │   ├── new-feature/          ← Guia de implementação (Nível 5)
│   │   ├── deploy-check/         ← Checklist de deploy (Nível 3/5)
│   │   └── security-scan/        ← Varredura customizada (Nível 5)
│   ├── hooks/
│   │   ├── safety-check.sh      ← Bloqueia comandos perigosos (Nível 8)
│   │   ├── post-edit-lint.sh    ← Lint automático (Nível 8)
│   │   ├── test-check.sh        ← Testes antes de encerrar (Nível 8)
│   │   └── notify.sh            ← Notificação de conclusão (Nível 8)
│   └── routines/
│       ├── daily-security.yaml  ← Auditoria noturna (Nível 10)
│       ├── weekly-deps.yaml     ← Atualização de deps (Nível 10)
│       └── pr-monitor.yaml      ← Review automático de PRs (Nível 10)
└── ~/.claude/
    └── CLAUDE.md                ← Suas preferências pessoais (Nível 2)
```

---

# Os 6 Erros Mais Comuns (e Como Não Cometê-los)

## Erro 1: Contexto grande sem compactação

A qualidade das respostas cai com sessões longas. Use `/compact` a cada 30-40 trocas. Coloque o que é importante no CLAUDE.md antes de compactar.

## Erro 2: Pedidos vagos

"Melhore o código" não funciona. "Adicione rate limiting ao endpoint X usando Redis, máximo 5 tentativas por IP em 15 minutos, seguindo o padrão do middleware em src/middleware/" funciona.

## Erro 3: Não ler o que Claude escreve

O Claude pode gerar código que você não entende. Isso é perigoso. Sempre peça:
```
"Gere o código E explique cada decisão não óbvia"
```

## Erro 4: MCPs com permissões amplas demais

Conectar o MCP de produção numa sessão de desenvolvimento é pedir problema. Ambientes separados, permissões separadas.

## Erro 5: Hooks silenciosos

Hooks que falham sem mensagem são piores que não ter hooks. Sempre inclua uma mensagem clara:
```bash
echo "BLOQUEADO: [motivo específico]. Para prosseguir: [ação necessária]" >&2
exit 1
```

## Erro 6: Routines sem monitoramento

Uma Routine que executa sem que ninguém saiba se funcionou é inútil. Configure sempre: log de execução + alerta de falha + resumo do que foi feito.

---

# Roteiro: 10 Semanas para o Nível 10

| Semanas | Foco | Entregável |
|---------|------|------------|
| 1–2 | Terminal + Memory | CLAUDE.md com 20+ regras reais |
| 3–4 | Commands + Custom | 5 skills customizadas funcionando |
| 5–6 | MCP | GitHub + DB MCP, workflow issue→PR automático |
| 7–8 | Subagents + Hooks | 3 hooks ativos, 1 refactoring com subagents |
| 9–10 | Headless + Routines | CI/CD integrado, 2 routines em produção |

---

# Conclusão

A diferença entre um dev no Nível 1 e no Nível 10 não é que um é "melhor programador". É que um opera em uma realidade diferente.

No Nível 1, o Claude é um assistente. No Nível 10, o Claude é um sistema que trabalha em paralelo com você — e, às vezes, enquanto você dorme.

Os dados confirmam: os que chegam ao topo economizam de 5 a 8 horas por semana, mantêm codebases que seriam impossíveis de administrar manualmente e produzem com uma consistência que revisões manuais não conseguem garantir.

Mas isso exige investimento real. Não de horas de uso passivo. De aprendizado deliberado, nível por nível.

Você tem o mapa. O caminho é seu.

---

## Referências

- [Claude Code Docs — Best Practices](https://code.claude.com/docs/en/best-practices)
- [How Anthropic Teams Use Claude Code — PDF Oficial](https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf)
- [Claude Code Advanced Patterns: Subagents, MCP, Scaling](https://resources.anthropic.com/hubfs/Claude%20Code%20Advanced%20Patterns_%20Subagents,%20MCP,%20and%20Scaling%20to%20Real%20Codebases.pdf)
- [Claude Code Guide 2026: 25 Features — MarkTechPost](https://www.marktechpost.com/2026/06/14/claude-code-guide-2026-25-features-with-examples-demo/)
- [Claude Code Usage Statistics 2026](https://serpsculpt.com/claude-code-usage-statistics/)
- [Developer Survey 2026: AI Coding 73% Daily](https://claude5.ai/news/developer-survey-2026-ai-coding-73-percent-daily)
- [MIT Technology Review: Code with Claude](https://www.technologyreview.com/2026/05/21/1137735/anthropics-code-with-claude-showed-off-codings-future-whether-you-like-it-or-not/)
- [Measuring Claude Code ROI — Faros.ai](https://www.faros.ai/blog/how-to-measure-claude-code-roi-developer-productivity-insights-with-faros-ai)
- [Claude Code Routines: 24/7 Agents — MindStudio](https://www.mindstudio.ai/blog/claude-code-routines-24-7-agents)
- [Claude Code Hooks, Subagents & Skills — ofox.ai](https://ofox.ai/blog/claude-code-hooks-subagents-skills-complete-guide-2026/)
- [Claude Code Setup: MCP, Hooks, Skills — Okhlopkov](https://okhlopkov.com/claude-code-setup-mcp-hooks-skills-2026/)
- [Claude Code vs Copilot 2026](https://orbilontech.com/claude-code-vs-copilot-2026-productivity-gap/)
- [MCP Directory — Best Practices](https://mcp.directory/blog/claude-code-best-practices)
- [GitHub Best Practices Repo](https://github.com/shanraisshan/claude-code-best-practice)

---

*Publicado em Junho de 2026. Dados e recursos refletem o estado da ferramenta nesta data.*
