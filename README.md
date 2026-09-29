# my-co-skills

Skills genéricas do Claude Code para uso pessoal.

## Instalação

```bash
npx skills add https://github.com/m1ttes1/my-co-skills --skill melhorar-prompt
```

Plano B (repo privado ou CLI com problema):

```bash
git clone https://github.com/m1ttes1/my-co-skills.git
# copiar skills/<nome> para %USERPROFILE%\.claude\skills\
```

## Skills

| Skill | Uso |
|---|---|
| melhorar-prompt | `/melhorar-prompt <texto>` analisa e reescreve prompts com as práticas da Anthropic |

## Agentes de revisão

`agents/` tem subagentes do Claude Code (qa-requisitos, revisor-critico, revisor-texto).
Copiar para `%USERPROFILE%\.claude\agents\`.

`global/CLAUDE.md` ativa a revisão automática em toda sessão.
Copiar (ou mesclar, se já existir) para `%USERPROFILE%\.claude\CLAUDE.md`.

## Regras do repo

- Só skills genéricas. Nada de dados, processos ou nomes de empresa/cliente.
- Edição e push feitos no PC pessoal.
