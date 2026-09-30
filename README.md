# my-co-skills

Skills, subagentes e instruções globais do Claude Code para uso pessoal. Só conteúdo genérico: nada de dado, processo ou nome de empresa ou cliente.

## Estrutura

```
global/CLAUDE.md      regras de comportamento (vira um bloco no ~/.claude/CLAUDE.md)
agents/               triagem-ticket, pesquisador-politicas, planejador-configuracao,
                      revisor, qa, redator-doc, revisor-texto
skills/               melhorar-prompt, consultor, humanizer-pt-br,
                      i-have-adhd, frontend-premium, revisor-email
commands/pq.md        atalho /pq para melhorar-prompt
gosto-visual.md       registro do gosto visual em front-end (começa vazio)
INSTALAR.md           prompt de instalação
```

## Skills e comandos

| Nome | Uso |
|---|---|
| melhorar-prompt | `/melhorar-prompt <texto>` ou `/pq <texto>` analisa e reescreve prompts com as práticas da Anthropic |
| consultor | `/consultor` respostas enxutas e formais para comunicação corporativa |
| humanizer-pt-br | remove marcas de texto gerado por IA em português brasileiro |
| i-have-adhd | `/i-have-adhd` modo completo de formatação amigável a TDAH (opt-in) |
| frontend-premium | padrão de acabamento para qualquer interface web |
| revisor-email | revisa e-mail corporativo, interno ou externo, com alerta leve de framing |

Agentes: o time de ticket (`triagem-ticket`, `pesquisador-politicas`, `planejador-configuracao`), os de conferência (`revisor`, `qa`) e os de texto (`redator-doc`, `revisor-texto`). O `global/CLAUDE.md` define o fluxo, a regra de padronizar conteúdo para o time e a regra de não colocar dado pessoal.

## Instalar (sem admin)

Abra o [INSTALAR.md](INSTALAR.md), copie o prompt e cole no Claude Code da máquina de destino. Ele clona o repo, mostra o que vai mudar, faz backup em `~/.claude/backups/`, copia agents, skills e commands, e insere o `CLAUDE.md` como bloco delimitado sem apagar o que já existe.

Instalação manual de uma skill isolada:

```bash
npx skills add https://github.com/m1ttes1/my-co-skills --skill melhorar-prompt
```

## Atualizar

Edição e push só do PC pessoal. No PC de destino, rode o prompt do INSTALAR.md de novo. O `gosto-visual.md` com conteúdo nunca é sobrescrito. Como ele é preenchido lá, não faça push a partir do PC de destino.

## Créditos

- `i-have-adhd` é adaptada de [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd), licença MIT (ver `skills/i-have-adhd/LICENSE`).

## Regras do repo

- Só conteúdo genérico. Nada de dados, processos ou nomes de empresa ou cliente.
- Sem segredos, tokens, e-mails nem dados pessoais.
