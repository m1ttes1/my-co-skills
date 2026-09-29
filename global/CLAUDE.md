# Instruções globais

## Revisão multiagente

Revisores disponíveis (subagentes, contexto separado, só leitura):
- `qa-requisitos`: entrega vs. pedido (faltou, inventou, fugiu do escopo).
- `revisor-critico`: premissas, lógica, riscos, alternativas.
- `revisor-texto`: texto que outras pessoas vão ler (PT/EN).

### Quando ACIONAR (qualquer gatilho basta)

1. **Erro repetido:** eu apontei erro ou pedi correção 2 vezes ou mais na mesma tarefa. A partir daí, toda nova tentativa passa por `qa-requisitos` + `revisor-critico` antes de me entregar, e você explica o que causou os erros anteriores.
2. **Planejamento:** eu pedi para planejar, desenhar, estruturar ou propor abordagem. Passe o plano pelo `revisor-critico` ANTES de me apresentar ou executar.
3. **Tarefa complexa**, sinais objetivos:
   - envolve 3 ou mais arquivos, etapas ou sistemas;
   - altera ou apaga dados, arquivos ou configurações existentes;
   - análise de dados com números ou conclusões que vou usar para decidir ou apresentar;
   - requisitos longos, com várias restrições;
   - você mesmo está em dúvida entre abordagens ou fez suposições relevantes.
4. **Texto para terceiros:** e-mail, mensagem, documentação ou apresentação que será enviada → `revisor-texto`.
5. **Pedido explícito:** eu digo "revisa", "passa no QA", "caprichado", "modo revisão".

### Quando NÃO acionar

Pergunta simples, conversa, explicação curta, comando trivial, ou quando eu disser "sem revisão" / "rápido". Pedido explícito meu sempre vence os gatilhos.

### Como conduzir

- Envie ao revisor o pedido original, restrições e a entrega. Nada além do necessário.
- Corrija o que for procedente. Se discordar de um apontamento, diga por quê.
- Na entrega, informe em 1 a 3 linhas: qual gatilho acionou, o que os revisores apontaram e o que foi corrigido.
- Se não acionou em algo que eu achar que deveria, eu vou avisar; trate isso como gatilho de erro repetido.
