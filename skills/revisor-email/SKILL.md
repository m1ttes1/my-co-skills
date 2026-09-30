---
name: revisor-email
description: Revisa e-mails corporativos em português (PT-BR), internos (equipe, gestão) e externos (clientes, parceiros, fornecedores), focando em gramática, ortografia, pontuação, clareza e tom, e sinalizando riscos leves de framing (afirmações prematuras de causa ou responsabilidade, prazos e compromissos não confirmados). Use esta skill sempre que o usuário colar o texto de um e-mail e pedir para revisar, corrigir, conferir, dar uma olhada, ou perguntar se o e-mail "está bom para mandar". Também dispara para "revisa esse email", "confere a gramática", "dá uma olhada antes de eu enviar", "isso tá pronto pra mandar?" ou qualquer variação que envolva validar um e-mail antes do envio. NÃO é auditoria técnica completa do conteúdo: o alerta de framing é leve e não valida causa raiz.
---

# Revisor de E-mail Corporativo

## Por que essa skill existe

E-mail corporativo costuma ser a prova documentada de uma interação. Erros de português passam impressão de descuido, e armadilhas de framing (afirmar uma causa antes de confirmar, prometer prazo que não está garantido, encerrar um assunto prematuramente) podem gerar problema sério depois. Esta skill faz duas passadas separadas: uma de revisão linguística (o foco principal) e outra, mais leve, de sinalização de risco de framing. Mantenha as duas separadas, porque "isso está gramaticalmente errado" e "isso é arriscado de afirmar" são problemas de natureza diferente e pedem seções diferentes na resposta.

## Quando usar

- O usuário cola o texto de um e-mail e pede revisão, correção, ou confirmação de que "está bom para mandar".
- **E-mail externo** (cliente, parceiro, fornecedor): registro mais formal, as duas passadas com atenção total.
- **E-mail interno** (equipe, gestão): registro pode ser mais direto e menos cerimonioso. Não force formalidade que destoe da cultura do time. A Passada 1 continua; a Passada 2 é mais curta e só vale para compromissos, prazos e atribuição de culpa.
- Se não estiver claro se o destinatário é interno ou externo, pergunte em uma linha antes de revisar.
- Não substitui auditoria técnica. A skill não tem acesso ao contexto do caso (tickets, logs, histórico). Ela só sinaliza linguagem que *parece* arriscada pela forma como está escrita, não valida se o conteúdo técnico está certo.

## Passada 1: Revisão linguística (foco principal)

Revise o texto procurando por:

- **Ortografia e acentuação:** erros de grafia, acentos faltando ou trocados (ex.: "está" vs "esta", "é" vs "e").
- **Concordância verbal e nominal:** sujeito-verbo, especialmente em frases com "a gente", sujeitos compostos, ou orações intercaladas que fazem o escritor perder o fio da concordância.
- **Crase:** um dos erros mais comuns em e-mail corporativo brasileiro (ex.: "devido à", "às vezes"; e atenção a expressões como "a nível de", que tecnicamente nem deveriam ser usadas nesse sentido).
- **Pontuação:** vírgula antes de "que" explicativo, vírgula separando sujeito do verbo (erro comum), ponto final faltando, excesso de exclamação em contexto formal.
- **Clareza e objetividade:** frases longas demais, ambiguidade de pronomes ("ele" referindo a quê?), redundância, gerundismo desnecessário ("estaremos verificando" vira "vamos verificar").
- **Registro adequado ao destinatário:** externo pede "você" formal e consistente (sem misturar com "tu"), saudação e fechamento adequados; interno aceita tom mais direto.
- **Nomes próprios e termos técnicos:** preserve exatamente como o usuário escreveu nomes de pessoas, empresas, sistemas e siglas (SLA, ERP, ticket, etc.). Não "corrija" o que já está correto só porque parece estrangeiro.

Para cada problema encontrado, anote a mudança e o motivo de forma direta. Não precisa citar a regra gramatical formal, só o suficiente para o usuário entender por que mudou.

## Passada 2: Alerta leve de framing

Depois da revisão linguística, releia o texto procurando especificamente por linguagem que:

- Afirma uma causa raiz ou responsabilidade técnica de forma definitiva quando o texto não indica que isso foi de fato confirmado (ex.: "identificamos que o problema é X" sem nenhuma ressalva).
- Assume ou descarta responsabilidade de uma área ou de terceiros antes da hora (ex.: "o problema não é nosso" sem evidência conclusiva no próprio texto).
- Promete prazo, SLA ou solução sem ressalva, quando isso pode não estar garantido.
- Tem tom que pode ser lido como admissão de culpa ou compromisso contratual não intencional.
- Fecha ou encerra um chamado ou investigação antes de qualquer confirmação adicional.

Esse alerta é **leve, não uma auditoria**. Você não tem acesso ao histórico técnico completo do caso, então não tente julgar se a causa apontada está certa ou errada. Apenas aponte: "essa frase parece definitiva, isso já foi confirmado?" e sugira uma redação mais cautelosa como alternativa. Se a Passada 2 não encontrar nada suspeito, diga isso em uma linha curta e não invente um alerta para preencher espaço.

## Formato de saída

Estruture sempre a resposta em três partes:

1. **E-mail revisado:** o texto completo já corrigido, pronto para copiar e colar. Nunca use travessão (—); prefira vírgula, ponto, dois-pontos ou parênteses.
2. **O que foi alterado:** lista enxuta das mudanças da Passada 1, cada uma com o problema e a correção.
3. **Alerta de framing:** só aparece com conteúdo se a Passada 2 encontrar algo; senão, uma linha confirmando que nada chamou atenção.

Não reescreva o conteúdo técnico do e-mail (não altere fatos, números ou decisões já tomadas pelo usuário). Ajuste só a linguagem e aponte risco de framing quando existir.

## Exemplo

**Entrada:**
"Boa tarde, conforme analisamos os logs de monitoramento identificamos que o problema é do servidor de aplicação, o time de infra já pode finalizar o chamado. Qualquer duvida estou a disposição."

**E-mail revisado:**
"Boa tarde, conforme análise dos logs de monitoramento, identificamos indícios de que o problema está relacionado ao servidor de aplicação. Seguimos investigando para confirmar a causa antes de finalizar o chamado. Qualquer dúvida, estou à disposição."

**O que foi alterado:**
- "duvida" para "dúvida": faltou o acento.
- "a disposição" para "à disposição": crase obrigatória nessa expressão.
- "Qualquer duvida estou a disposição" dividido em duas orações com vírgula, para evitar a leitura corrida.

**Alerta de framing:**
- O trecho "identificamos que o problema é do servidor de aplicação, o time de infra já pode finalizar o chamado" afirma causa definitiva e encerra o chamado antes de qualquer confirmação adicional. Sugestão: "identificamos indícios de que o problema está relacionado a..." e manter o chamado aberto até a causa ser confirmada, o que evita reabertura caso a causa real seja outra.
