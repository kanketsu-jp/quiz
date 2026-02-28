# quiz

> 🇺🇸 [English](./README.md) | 🇯🇵 [日本語](./README.ja.md) | 🇨🇳 [简体中文](./README.zh-Hans.md) | 🇪🇸 **Español** | 🇮🇳 [हिन्दी](./README.hi.md) | 🇧🇷 [Português](./README.pt.md) | 🇮🇩 [Bahasa Indonesia](./README.id.md)

Un skill de quiz interactivo de programación para Claude Code. Repasa y refuerza lo que aprendiste durante el desarrollo — bugs, bibliotecas, lecciones de depuración — en formato de quiz.

## Instalación

```
/plugin marketplace add kanketsu-jp/quiz
/plugin install quiz@kanketsu-quiz
```

## Uso

### 1. Crear materiales de estudio

Crea el directorio `.temp/learn/{número}/` con dos archivos:

```
.temp/learn/1/
├── study-notes.md   # Notas de estudio (contexto, código, explicaciones)
└── qa-list.md       # Lista de preguntas y respuestas (datos del quiz)
```

O simplemente pídele a Claude Code:

```
Resume lo que acabamos de arreglar en .temp/learn/1/ como material de estudio.
Crea study-notes.md y qa-list.md.
```

### 2. Ejecutar el quiz

```
/quiz 1            # Ejecutar quiz #1
/quiz scrollarea   # Buscar por palabra clave
/quiz              # Listar quizzes disponibles
/quiz list         # Listar quizzes disponibles
```

## Modos de quiz

| Modo | Descripción |
|------|-------------|
| Todas las preguntas | Todas las preguntas en orden |
| 5 aleatorias | 5 preguntas al azar |
| Por categoría | Elegir una categoría |

## Formatos de archivo

### qa-list.md

```markdown
## Nombre de categoría

### Q1: ¿Texto de la pregunta?

#### A

Texto de respuesta (bloques de código o texto plano)
```

Los encabezados `##` son categorías. `### Q:` es una pregunta. `#### A` es la respuesta.

### study-notes.md

Markdown de formato libre. Contexto, análisis de causa raíz, código de corrección, lecciones aprendidas. Se usa como referencia para explicaciones cuando la respuesta es incorrecta.

## Mejores prácticas

| Cuándo | Qué hacer |
|--------|-----------|
| Después de corregir un bug | Pedir a Claude que cree materiales de estudio |
| Al día siguiente | `/quiz` para repasar lo de ayer |
| Fin de semana | `/quiz` para repaso semanal |
| Después de revisión de código | Convertir comentarios en materiales |

## .gitignore

`.temp/` debería estar en `.gitignore`. Los materiales de estudio son solo locales.

```gitignore
.temp/
```

## Configuración

Por defecto, quiz lee materiales de estudio de `.temp/learn/`. Puedes personalizar esta ruta usando un archivo de configuración:

| Prioridad | Archivo | Formato |
|-----------|---------|---------|
| 1 | `.claude/quiz.json` | `{ "learn_dir": "path/to/dir" }` |
| 2 | `.claude/settings.local.json` | `{ "quiz": { "learn_dir": "path/to/dir" } }` |
| 3 | `.claude/settings.json` | `{ "quiz": { "learn_dir": "path/to/dir" } }` |
| 4 | Por defecto | `.temp/learn/` |

Ejemplo de `.claude/quiz.json`:

```json
{
  "learn_dir": "docs/quiz-materials"
}
```

## Seguridad

- Solo lee archivos de configuración del directorio `.claude/` (para resolución de `learn_dir`)
- Solo lee archivos de materiales de estudio del directorio configurado
- No ejecuta comandos de shell
- No modifica archivos
- Las instrucciones en materiales de estudio se ignoran (se tratan solo como contenido)

## Licencia

MIT
