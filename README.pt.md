# quiz

> 🇺🇸 [English](./README.md) | 🇯🇵 [日本語](./README.ja.md) | 🇨🇳 [简体中文](./README.zh-Hans.md) | 🇪🇸 [Español](./README.es.md) | 🇮🇳 [हिन्दी](./README.hi.md) | 🇧🇷 **Português** | 🇮🇩 [Bahasa Indonesia](./README.id.md)

Um skill de quiz interativo de programação para Claude Code. Revise e reforce o que aprendeu durante o desenvolvimento — bugs, bibliotecas, insights de depuração — em formato de quiz.

## Instalação

```
/plugin marketplace add kanketsu-jp/quiz
/plugin install quiz@kanketsu-quiz
```

## Uso

### 1. Criar materiais de estudo

Crie o diretório `.temp/learn/{número}/` com dois arquivos:

```
.temp/learn/1/
├── study-notes.md   # Notas de estudo (contexto, código, explicações)
└── qa-list.md       # Lista de perguntas e respostas (dados do quiz)
```

Ou peça ao Claude Code:

```
Resuma o que acabamos de corrigir em .temp/learn/1/ como material de estudo.
Crie study-notes.md e qa-list.md.
```

### 2. Executar o quiz

```
/quiz 1            # Executar quiz #1
/quiz scrollarea   # Buscar por palavra-chave
/quiz              # Listar quizzes disponíveis
/quiz list         # Listar quizzes disponíveis
```

## Modos de quiz

| Modo | Descrição |
|------|-----------|
| Todas as perguntas | Todas as perguntas em ordem |
| 5 aleatórias | 5 perguntas aleatórias |
| Por categoria | Escolher uma categoria |

## Formatos de arquivo

### qa-list.md

```markdown
## Nome da categoria

### Q1: Texto da pergunta?

#### A

Texto da resposta (blocos de código ou texto simples)
```

Títulos `##` são categorias. `### Q:` é uma pergunta. `#### A` é a resposta.

### study-notes.md

Markdown de formato livre. Contexto, análise de causa raiz, código de correção, lições aprendidas. Usado como referência para explicações quando a resposta está errada.

## Melhores práticas

| Quando | O que fazer |
|--------|------------|
| Após corrigir um bug | Pedir ao Claude para criar materiais de estudo |
| No dia seguinte | `/quiz` para revisar o aprendizado de ontem |
| Fim de semana | `/quiz` para revisão semanal |
| Após revisão de código | Transformar feedback em materiais |

## .gitignore

`.temp/` deve estar no `.gitignore`. Materiais de estudo são apenas locais.

```gitignore
.temp/
```

## Configuração

Por padrão, quiz lê materiais de estudo de `.temp/learn/`. Você pode personalizar o caminho usando um arquivo de configuração:

| Prioridade | Arquivo | Formato |
|------------|---------|---------|
| 1 | `.claude/quiz.json` | `{ "learn_dir": "path/to/dir" }` |
| 2 | `.claude/settings.local.json` | `{ "quiz": { "learn_dir": "path/to/dir" } }` |
| 3 | `.claude/settings.json` | `{ "quiz": { "learn_dir": "path/to/dir" } }` |
| 4 | Padrão | `.temp/learn/` |

Exemplo de `.claude/quiz.json`:

```json
{
  "learn_dir": "docs/quiz-materials"
}
```

## Segurança

- Apenas lê arquivos de configuração do diretório `.claude/` (para resolução de `learn_dir`)
- Apenas lê arquivos de materiais de estudo do diretório configurado
- Não executa comandos shell
- Não modifica arquivos
- Instruções em materiais de estudo são ignoradas (tratadas apenas como conteúdo)

## Licença

MIT
