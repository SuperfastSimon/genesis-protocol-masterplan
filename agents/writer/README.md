# Genesis Writer Agent

## Status: ✅ ACTIVE

## Platform IDs
- **Graph ID**: `ec6e684e-ec01-4901-a040-69870497d347`
- **Library ID**: `7e8cae83-077f-4096-bf7a-fec3f1b4e9d4`
- **Platform Link**: [Open in Builder](https://platform.agpt.co/build?flowID=ec6e684e-ec01-4901-a040-69870497d347)

## Architecture
```
Input: task, language, framework, requirements
  │
  □
[AI Text Generator] → Generate code with system prompt
  │
  □
[Code Extraction Block] → Parse into language-specific outputs
  │
  □
Output: { python, javascript, html, css, bash, remaining_text }
```

## Blocks Used
| Block | ID | Purpose |
|-------|----|---------|
| AI Text Generator | `1f292d4a-41a4-4977-9684-7c8d560b9f91` | LLM code generation |
| Code Extraction | `d3a7d896-3b78-4f44-8b4b-48fbf4f0bcd8` | Parse code blocks |

## LLM Config
- **Model**: Groq Llama 3.3 70B Versatile
- **Fallback**: Claude Sonnet 4 / GPT-4o

## System Prompt
```
You are the Writer Agent of the Genesis Protocol.
Your job:
1. Receive a specific writing task
2. Generate clean, production-ready code or content
3. Always include: proper file structure, comments, error handling, type hints
4. Follow best practices for the target language/framework
5. Output code in markdown code blocks
```

## Test Results

### Test 1: Flask TODO API ✅
- **Input**: "Build a REST API for a todo app with CRUD operations"
- **Language**: Python
- **Framework**: Flask
- **Output**: 6 files (config.py, models.py, schemas.py, utils.py, routes.py, app.py)
- **Code Extraction**: Successfully parsed Python, Bash, Markdown
- **Status**: PASSED
