# Checklist Rápido de Qualificação de Prompt

Use este checklist para revisar rapidamente um prompt antes de entregá-lo qualificado.

---

## ✅ Clareza e especificidade
- [ ] A tarefa principal está explícita e sem ambiguidade?
- [ ] O output esperado está descrito (formato, extensão, estrutura)?
- [ ] Instruções sequenciais usam numeração quando a ordem importa?
- [ ] Um colega sem contexto conseguiria seguir o prompt?

## ✅ Contexto e motivação
- [ ] Há explicação do "por quê" quando isso pode influenciar o resultado?
- [ ] O público-alvo do output está definido (quando relevante)?
- [ ] Restrições importantes estão mencionadas (tom, nível técnico, limitações)?

## ✅ Exemplos
- [ ] Há exemplos quando formato/tom/estrutura são críticos?
- [ ] Os exemplos estão em tags `<example>` ou `<examples>`?
- [ ] Os exemplos cobrem casos variados (não são todos iguais)?

## ✅ Estrutura XML
- [ ] Instruções, contexto, exemplos e input estão separados em tags?
- [ ] Tags têm nomes descritivos e consistentes?
- [ ] Documentos longos têm hierarquia adequada (`<documents>` > `<document>`)?

## ✅ Role
- [ ] Há um papel definido para o modelo (no system prompt ou início do prompt)?
- [ ] O role é relevante para a tarefa pedida?

## ✅ Formato de output
- [ ] O formato de resposta está especificado?
- [ ] As instruções de formato dizem o que FAZER (não só o que evitar)?
- [ ] JSON, markdown, prosa ou outro formato está explícito quando necessário?

## ✅ Raciocínio
- [ ] Tarefas complexas incluem instrução para pensar antes de responder?
- [ ] Há separação entre raciocínio (`<thinking>`) e output final (`<answer>`) quando útil?
- [ ] Há instrução de auto-verificação para tarefas críticas?

## ✅ Contexto longo (somente se aplicável)
- [ ] Documentos longos estão ANTES das instruções e queries?
- [ ] Cada documento tem sua própria tag `<document>` com `<source>` e `<document_content>`?
- [ ] O modelo é instruído a citar trechos antes de responder?

---

## Pontuação de maturidade do prompt

| Critérios atendidos | Maturidade |
|---|---|
| 0–3 | 🔴 Fraco — reescrever completamente |
| 4–6 | 🟡 Mediano — melhorias significativas necessárias |
| 7–9 | 🟢 Bom — ajustes pontuais |
| 10+ | ✅ Excelente — pronto para uso |

---

## Sinais de alerta imediatos

🚩 Prompt de uma linha sem nenhuma especificação  
🚩 Mistura de instruções e dados sem separação  
🚩 Output esperado completamente ausente  
🚩 Instrução negativa sem alternativa positiva ("não faça X" sem "faça Y")  
🚩 Documentos longos colocados APÓS as instruções  
🚩 Pedido de raciocínio complexo sem CoT ou role adequado  
