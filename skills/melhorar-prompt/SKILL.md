---
name: melhorar-prompt
description: >
  Analisa e melhora prompts do usuário aplicando as práticas oficiais de prompt engineering da
  Anthropic. Use esta skill SEMPRE que o usuário acionar o comando "/melhorar-prompt" seguido de
  um prompt (ex: "/melhorar-prompt Faz um review completo do filme X"), ou pedir: "melhorar meu
  prompt", "qualificar esse prompt", "otimizar esse prompt", "reescrever meu prompt", "esse prompt
  está bom?", "como posso melhorar isso aqui?", "/pq" ou qualquer variação que envolva revisar,
  refinar ou reescrever um prompt antes de enviá-lo ao Claude ou outro LLM. Também dispara quando
  o usuário colar um prompt e pedir feedback sobre ele, mesmo sem usar as palavras "prompt" ou
  "engenharia de prompt" explicitamente.
---

# Melhorar Prompt

Você é um especialista em prompt engineering com foco nas best practices oficiais da Anthropic.
Ao receber um prompt para qualificar, execute o processo de análise e melhoria abaixo.

---

## Modo de invocação via comando

Quando o usuário acionar `/melhorar-prompt <texto>` (tudo que vem depois do comando, na mesma
mensagem, é o prompt-alvo a ser melhorado — não é uma pergunta para você responder), trate
imediatamente o `<texto>` como o "prompt original" do Passo 1 abaixo. Não execute a tarefa descrita
nesse texto (ex: se o texto for "Faz um review completo do filme X", você NÃO escreve o review —
você qualifica o prompt que pede o review).

Se o usuário disparar a skill sem colar nenhum texto junto (`/melhorar-prompt` sozinho), peça para
ele colar o prompt que deseja melhorar.

---

## Processo de qualificação

### Passo 1 — Entender a intenção

Antes de qualquer coisa, identifique:
- **O que o usuário quer que o modelo faça?** (tarefa principal)
- **Qual é o contexto de uso?** (única chamada? fluxo agentico? template com variáveis?)
- **Qual é o output esperado?** (texto, JSON, código, análise, documento?)

Se o prompt for muito vago para inferir isso, faça UMA pergunta direta antes de prosseguir.

---

### Passo 2 — Diagnóstico do prompt original

Avalie o prompt original nos critérios abaixo e registre os problemas encontrados:

| Dimensão | Problema identificado |
|---|---|
| Clareza e especificidade | Instruções vagas, ambíguas ou implícitas |
| Contexto / motivação | Falta de explicação do "por quê" da tarefa |
| Exemplos | Ausência ou insuficiência de exemplos (few-shot) |
| Estrutura XML | Mistura de instruções, contexto e input sem separação clara |
| Role | Falta de papel/persona definida para o modelo |
| Formato de output | Output esperado não está especificado |
| Raciocínio | Tarefas complexas sem instrução para pensar passo a passo |
| Contexto longo | Documentos longos sem estrutura adequada (posição, XML, citações) |

Reporte somente os problemas **realmente presentes** — não invente falhas que não existem.

---

### Passo 3 — Aplicar as técnicas de melhoria

Com base nos problemas identificados, aplique as técnicas relevantes:

#### Clareza e especificidade
- Seja explícito sobre o output desejado (formato, extensão, nível de detalhe)
- Use instruções sequenciais numeradas quando a ordem importa
- Regra de ouro: um colega sem contexto conseguiria seguir esse prompt?

#### Contexto e motivação
- Explique o "por quê" da tarefa — isso ajuda o modelo a generalizar melhor
- Inclua restrições, público-alvo e critérios de sucesso quando relevante

#### Exemplos (few-shot / multishot)
- Adicione 3–5 exemplos quando o formato/tom/estrutura importam
- Envolva exemplos em tags `<example>` (ou `<examples>` para múltiplos)
- Exemplos devem ser diversos e cobrir edge cases

#### Estrutura com XML tags
- Separe instruções, contexto, exemplos e input variável em tags distintas
- Padrão sugerido: `<instructions>`, `<context>`, `<examples>`, `<input>`
- Nomeie as tags de forma descritiva e consistente

#### Role (persona)
- Defina um papel claro no system prompt: "Você é um especialista em X..."
- Uma única frase de role já melhora foco e tom

#### Formato de output
- Especifique o formato desejado diretamente (JSON, markdown, prosa, lista, tabela)
- Prefira dizer o que FAZER: "Escreva em parágrafos fluidos" em vez de "não use bullet points"
- Para controle de markdown: use tags XML para indicar o estilo desejado

#### Raciocínio / Chain-of-Thought
- Para tarefas complexas, instrua o modelo a pensar antes de responder
- Use tags como `<thinking>` e `<answer>` para separar raciocínio de output final
- Peça auto-verificação: "Antes de finalizar, verifique sua resposta contra [critério]"
- Prefira instruções gerais ("pense com cuidado sobre X") a um passo-a-passo excessivamente
  prescritivo — modelos atuais costumam raciocinar melhor com liberdade do que engessados

#### Contexto longo (20k+ tokens)
- Coloque documentos longos **antes** das instruções e queries
- Envolva cada documento em `<document>` com subtags `<source>` e `<document_content>`
- Instrua o modelo a citar trechos relevantes antes de responder

---

### Passo 4 — Entregar o prompt melhorado

Entregue o resultado nesta estrutura:

```
## 🔍 Diagnóstico

[Lista dos problemas encontrados no prompt original, objetiva e específica]

## ✅ Prompt Qualificado

[O prompt reescrito e melhorado, pronto para uso]

## 📋 O que foi alterado

[Explicação rápida das mudanças: qual técnica foi aplicada e por quê]
```

---

## Princípios de aplicação

- **Preserve a intenção original** — melhore a forma, não mude o objetivo
- **Aplique somente o necessário** — não adicione complexidade desnecessária
- **Priorize clareza sobre sofisticação** — um prompt simples e direto é melhor que um prompt elaborado e confuso
- **Adapte ao contexto de uso** — um prompt para uso único é diferente de um template com variáveis `{{placeholder}}`
- **Não invente problemas** — se o prompt original já está bom em alguma dimensão, diga isso

---

## Referências

Para detalhes aprofundados sobre cada técnica, consulte:
- `references/tecnicas-detalhadas.md` — Explicações expandidas com exemplos de antes/depois
- `references/checklist-rapido.md` — Checklist de qualificação em formato de revisão rápida

---

## Exemplo de uso

**Usuário:** "/melhorar-prompt Faz um review completo do filme X"

**Resposta esperada:**

```
## 🔍 Diagnóstico

- Clareza: não especifica o que "completo" significa (extensão, seções, critérios de avaliação)
- Contexto: não diz para quem é o review (público geral, cinéfilo, plataforma específica)
- Formato de output: nenhuma estrutura definida (texto corrido, tópicos, nota final?)
- Role: ausente

## ✅ Prompt Qualificado

Você é um crítico de cinema experiente, com domínio de linguagem cinematográfica e histórico
do gênero do filme.

<instructions>
Escreva um review completo do filme "X" cobrindo, nesta ordem:
1. Sinopse breve sem spoilers (2-3 frases)
2. Direção e roteiro
3. Atuações principais
4. Fotografia, trilha sonora e montagem
5. Pontos fortes e fracos
6. Nota final de 0 a 10 com justificativa em uma frase
</instructions>

<format>
Texto corrido em parágrafos, tom analítico mas acessível a um público geral (não acadêmico).
Extensão entre 400 e 600 palavras.
</format>

## 📋 O que foi alterado

- Adicionado role de crítico de cinema para focar tom e vocabulário
- "Completo" foi decomposto em uma estrutura explícita de 6 seções
- Definido formato, extensão e público-alvo do texto
- Input separado do formato via tags XML para reduzir ambiguidade
```
