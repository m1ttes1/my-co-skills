# Técnicas Detalhadas de Prompt Engineering

Referência expandida baseada nas [best practices oficiais da Anthropic](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices).

---

## 1. Clareza e especificidade

**Princípio:** Claude responde bem a instruções claras e explícitas. Comportamento "above and beyond" deve ser solicitado explicitamente.

**Antes:**
```
Analise os dados de vendas
```

**Depois:**
```
Analise os dados de vendas abaixo e produza:
1. Um parágrafo resumindo a tendência geral do período
2. Os 3 produtos com melhor desempenho (nome + receita total)
3. Os 2 maiores riscos identificados nos dados
Limite sua resposta a no máximo 400 palavras.
```

**Regra de ouro:** Mostre o prompt para um colega sem contexto. Se ele ficaria confuso, o Claude também ficará.

---

## 2. Contexto e motivação

**Princípio:** Explicar o "por quê" ajuda o Claude a generalizar melhor e entregar respostas mais alinhadas com o objetivo real.

**Antes:**
```
Use bullets curtos na resposta
```

**Depois:**
```
Use bullets curtos na resposta — o output será exibido em um app mobile com largura limitada, então cada item deve ter no máximo uma linha.
```

Claude é inteligente o suficiente para generalizar a partir da explicação e aplicar o princípio em situações adjacentes.

---

## 3. Exemplos (Few-shot / Multishot)

**Princípio:** Exemplos são uma das formas mais confiáveis de guiar formato, tom e estrutura.

**Boas práticas:**
- 3–5 exemplos é o ideal
- Use `<example>` para um exemplo, `<examples>` para múltiplos
- Exemplos devem ser diversos e cobrir edge cases
- Exemplos devem espelhar de perto seu caso de uso real

**Estrutura:**
```xml
<examples>
  <example>
    <input>{{input_exemplo_1}}</input>
    <output>{{output_esperado_1}}</output>
  </example>
  <example>
    <input>{{input_exemplo_2}}</input>
    <output>{{output_esperado_2}}</output>
  </example>
</examples>
```

---

## 4. Estrutura com XML tags

**Princípio:** Tags XML ajudam o Claude a separar instruções, contexto, exemplos e input variável sem ambiguidade.

**Quando usar:**
- Prompts que misturam tipos de conteúdo
- Templates com variáveis
- Prompts longos com múltiplas seções

**Tags comuns:**
```xml
<instructions>  → o que fazer
<context>       → por que fazer / background
<examples>      → exemplos few-shot
<input>         → dado variável que será processado
<text>          → documento ou texto a processar
<constraints>   → restrições e limites
<output_format> → como formatar a resposta
```

**Hierarquia:**
```xml
<documents>
  <document index="1">
    <source>relatório-q3.pdf</source>
    <document_content>{{conteúdo}}</document_content>
  </document>
</documents>
```

---

## 5. Role (Persona)

**Princípio:** Definir um papel no system prompt foca o comportamento e o tom do Claude para o caso de uso.

**Exemplos:**
```
Você é um especialista em análise financeira com 15 anos de experiência em FP&A.
```
```
Você é um revisor técnico de código Python focado em performance e segurança.
```
```
Você é um analista de CX responsável por comunicação com clientes de infraestrutura.
```

Uma única frase já faz diferença. Roles mais detalhados funcionam bem para casos de uso especializados.

---

## 6. Formato de output

**Princípio:** Especifique o formato esperado explicitamente. Prefira dizer o que FAZER ao invés do que NÃO fazer.

| Em vez de | Use |
|---|---|
| "Não use markdown" | "Escreva em parágrafos fluidos de prosa" |
| "Não use bullet points" | "Incorpore os itens naturalmente nas frases" |
| "Seja conciso" | "Limite a resposta a 3 parágrafos" |

**Para controle fino de markdown:**
```xml
<avoid_excessive_markdown>
Escreva em prosa clara, com parágrafos completos. Reserve markdown apenas para
`código inline`, blocos de código e títulos simples (## e ###). Evite **negrito**,
*itálico* e listas com bullets a menos que o usuário peça explicitamente.
</avoid_excessive_markdown>
```

---

## 7. Chain-of-Thought (CoT)

**Princípio:** Para tarefas complexas, instrua o Claude a pensar antes de responder. Isso melhora precisão especialmente em raciocínio lógico, matemática e código.

**Abordagem básica:**
```
Pense passo a passo antes de responder.
```

**Com tags estruturadas:**
```
Resolva o problema abaixo. Use a tag <thinking> para seu raciocínio e <answer> para a resposta final.
```

**Auto-verificação:**
```
Antes de finalizar, verifique se sua resposta está correta verificando {{critério específico}}.
```

**Nota:** Quando extended thinking estiver desativado, evite a palavra "think" — prefira "considere", "avalie", "raciocine" ou "analise".

---

## 8. Contexto longo (20k+ tokens)

**Princípio:** Com documentos longos, a posição das instruções e a estrutura XML impactam muito a qualidade.

**Regras:**
1. **Documentos longos vêm primeiro** — coloque o conteúdo longo ANTES das instruções e queries. Isso melhora performance em até 30%.
2. **Estruture com XML** — cada documento em `<document>` com subtags `<source>` e `<document_content>`
3. **Solicite citações** — peça ao Claude para citar trechos relevantes antes de responder

**Estrutura ideal:**
```xml
<documents>
  <document index="1">
    <source>arquivo.pdf</source>
    <document_content>{{conteúdo longo}}</document_content>
  </document>
</documents>

<instructions>
Com base nos documentos acima, responda: {{pergunta}}
Antes de responder, cite os trechos mais relevantes que fundamentam sua resposta.
</instructions>
```

---

## 9. Prompts para sistemas agênticos

**Use quando:** O prompt será usado em loops agênticos, com múltiplas chamadas, uso de ferramentas ou subagentes.

**Ação proativa (Claude age em vez de sugerir):**
```xml
<default_to_action>
Por padrão, implemente as mudanças em vez de apenas sugerí-las. Se a intenção do
usuário estiver ambígua, infira a ação mais útil e prossiga.
</default_to_action>
```

**Ação conservadora (Claude confirma antes de agir):**
```xml
<do_not_act_before_instructions>
Não inicie implementações ou modifique arquivos a menos que seja explicitamente
instruído. Quando a intenção for ambígua, forneça informações e recomendações
antes de tomar ação.
</do_not_act_before_instructions>
```

**Paralelismo em chamadas de ferramentas:**
```xml
<use_parallel_tool_calls>
Se você pretende chamar múltiplas ferramentas sem dependências entre elas, faça
todas as chamadas em paralelo. Maximize o uso de chamadas paralelas para aumentar
velocidade e eficiência.
</use_parallel_tool_calls>
```
