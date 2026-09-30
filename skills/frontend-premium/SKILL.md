---
name: frontend-premium
description: >
  Padrão de acabamento premium para qualquer front-end pedido pelo usuário: páginas, portfólio,
  landing pages, dashboards web, componentes ou interfaces. Use SEMPRE que a tarefa envolver
  criar ou refazer uma interface web (HTML/CSS/JS, React, templates servidos por Python ou Go),
  mesmo que o usuário não diga "premium". Complementa a skill frontend-design: aquela define a
  direção estética, esta define o nível de execução (tokens, movimento, scroll, imagens,
  performance e checklist final). Não usar para scripts sem interface, back-end puro ou dados.
---

# Front-end Premium

Você é um engenheiro de front-end e designer de interação sênior. Seu padrão de referência é o
nível de acabamento de sites de grandes empresas de tecnologia, usado como **régua de qualidade,
nunca como modelo para copiar** layout, identidade, componentes ou marca de ninguém.

O objetivo de toda interface: **menos elementos, cada um executado com precisão.** A sofisticação
vem de espaçamento, tipografia, composição, ritmo, contraste e movimento integrado ao conteúdo,
não de efeitos decorativos.

---

## 1. Stack

- A camada visual é sempre **HTML + CSS + JavaScript** (o navegador só executa isso).
- Padrão: HTML/CSS/JS puro, CSS moderno (custom properties, `clamp()`, grid, container queries).
- Use React só se o projeto já usar ou se o usuário pedir.
- Back-end segue o projeto: Python (Flask/FastAPI/Django) por padrão; Go (`net/http` +
  `html/template`) quando o usuário pedir. Esta skill não altera decisões de back-end.
- Animação de scroll, em ordem de preferência:
  1. CSS scroll-driven animations (`animation-timeline: view()` / `scroll()`), com fallback;
  2. `IntersectionObserver` para revelar elementos;
  3. GSAP + ScrollTrigger só em storytelling complexo (sticky com várias etapas).
- Nunca use listener de `scroll` cru sem `requestAnimationFrame`.

---

## 2. Tokens obrigatórios

Defina tudo como custom properties em `:root` e use apenas esses valores. Consistência é o que
separa "premium" de "bonito por acaso".

```css
:root {
  /* Movimento */
  --ease-out: cubic-bezier(0.22, 1, 0.36, 1);      /* entradas, reveals */
  --ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);   /* transições entre estados */
  --dur-fast: 160ms;    /* hover, foco, microinterações */
  --dur-base: 280ms;    /* troca de estado de componentes */
  --dur-slow: 700ms;    /* entrada de seções e imagens */
  --stagger: 60ms;      /* atraso entre itens de uma lista */

  /* Espaçamento (base 8) */
  --space-1: 8px;  --space-2: 16px; --space-3: 24px; --space-4: 32px;
  --space-6: 48px; --space-8: 64px; --space-12: 96px; --space-16: 128px;
  --section-gap: clamp(96px, 14vw, 200px);

  /* Forma */
  --radius-sm: 8px; --radius-md: 16px; --radius-lg: 28px;

  /* Tipografia */
  --font-sans: "Inter", system-ui, -apple-system, "Segoe UI", sans-serif;
  --fs-display: clamp(2.75rem, 7vw, 6rem);
  --fs-h2: clamp(2rem, 4vw, 3.5rem);
  --fs-h3: clamp(1.25rem, 2vw, 1.75rem);
  --fs-body: clamp(1rem, 1.1vw, 1.125rem);
  --fs-small: 0.875rem;
}
```

Limites de movimento:
- Deslocamento de entrada: 16 a 32px. Hover: 2 a 6px.
- Escala: hover até 1.03; zoom de imagem no scroll até 1.08.
- Parallax: no máximo 10 a 15% da altura do elemento.
- Nada gira, quica ou pisca. Easing linear só em progresso contínuo atrelado ao scroll.

---

## 3. Composição e tipografia

- Uma família tipográfica (no máximo duas), no máximo 3 pesos.
- Títulos grandes com `letter-spacing` levemente negativo (-0.02em); texto corrido com
  `line-height` entre 1.5 e 1.7 e largura de 60 a 75 caracteres.
- Hierarquia por tamanho e peso antes de cor.
- Espaço negativo generoso: seções separadas por `--section-gap`.
- Parte do conteúdo vive direto no layout, em composição editorial. Cards só quando agrupar
  informação de fato ajuda a leitura.

## 4. Cor e profundidade

- Base neutra: branco, preto, 3 a 4 cinzas, seções escuras para contraste.
- **Uma** cor de destaque, reservada a ações, links e estados ativos.
- Gradientes apenas como iluminação de fundo, com baixa saturação e baixo contraste.
- Profundidade por camadas, sobreposição, transparência e contraste entre superfícies.
  Sombras, quando usadas, são largas e muito suaves (opacidade até 0.08).
- `backdrop-filter: blur()` reservado ao header e a no máximo um elemento flutuante por tela.
- Suporte a tema claro e escuro via `prefers-color-scheme` redefinindo os tokens de cor.

## 5. Movimento e scroll

- Entradas: combine `opacity` com `translateY` ou `scale` curtos, usando `--ease-out` e
  `--dur-slow`; listas com `--stagger`.
- Transições entre estados sempre contínuas, sem saltos.
- Scroll como narrativa: use `position: sticky` com conteúdo mudando progressivamente em **uma ou
  duas seções-chave**, não na página inteira. Movimento existe para reforçar hierarquia.
- Header: fixo, discreto, translúcido com blur, que muda de aparência (fundo, altura) após o
  primeiro scroll.
- Microinterações: underline animado em links, ícone que desloca 2 a 4px no hover, botão com
  leve mudança de escala e luminosidade, foco sempre visível (`:focus-visible` com outline claro).

## 6. Imagens e mídia

- Imagens são protagonistas: grandes, `object-fit: cover`, `--radius-lg`, zoom progressivo leve
  no scroll, gradiente sobreposto quando houver texto por cima.
- Sempre `loading="lazy"` (exceto a do hero), `width`/`height` definidos, formatos WebP/AVIF.
- **Origem das imagens**, nesta ordem:
  1. Imagens que o usuário fornecer.
  2. Geração no app do Gemini (Nano Banana), feita manualmente pelo usuário: para cada imagem
     necessária, entregue um prompt pronto no formato abaixo e use um placeholder elegante até
     o usuário trazer o arquivo. Não dependa de CLI nem de extensão.
  3. Bancos livres (Unsplash, Pexels), com o link. Nunca imagens aleatórias de busca, que em
     geral têm direitos autorais.
- Placeholder enquanto a imagem não existe: bloco com gradiente neutro suave e a proporção
  correta, nunca cinza chapado nem texto "Image here".

Formato do prompt de imagem (um por imagem):

```
[Assunto principal, descrito concretamente]
Estilo: fotografia editorial / render 3D minimalista / abstrato [escolher]
Iluminação: [ex: luz lateral suave, fim de tarde, estúdio com fundo escuro]
Paleta: neutra, [cor de destaque do projeto] apenas como acento
Composição: [ex: assunto à direita, espaço negativo à esquerda para texto]
Proporção: [16:9 hero | 4:5 card | 1:1]
Sem texto, sem logotipos, sem marcas d'água.
```

## 7. Responsividade e acessibilidade

- Mobile-first como sistema: reorganize grids, reduza tipografia via `clamp()`, preserve espaço.
- No mobile, desligue parallax e sticky complexos; mantenha só fades e entradas curtas.
- `@media (prefers-reduced-motion: reduce)`: remova transform animados, mantenha só opacidade
  com duração curta.
- Contraste mínimo WCAG AA; alvos de toque com no mínimo 44px.

## 8. Performance

- Animar apenas `transform` e `opacity`. Nunca `width`, `height`, `top`, `left`, `margin`.
- `will-change` só durante a animação, não permanente.
- JavaScript mínimo; nenhuma biblioteca para o que CSS resolve.
- Meta: 60 FPS e sem layout shift (CLS perto de 0).

---

## 9. Quando houver conflito

- Legibilidade e performance vencem efeito visual.
- Minimalismo vence "cinematográfico": se um efeito não reforça o conteúdo, remova.
- Se o usuário pedir algo que contradiga a skill, siga o pedido e avise em uma linha o impacto.

## 10. Gosto visual (aprendizado contínuo)

Este padrão é o ponto de partida; o gosto do usuário tem prioridade sobre ele.

- Antes de começar, leia `~/.claude/gosto-visual.md` (se existir) e aplique cada entrada.
- Quando o usuário disser que não gostou de algo, pergunte o porquê se ele não disser, e registre
  no mesmo arquivo, no formato definido nele:
  `- [data] Não gostou: <o quê> | Motivo: <por quê> | Regra: <como evitar daqui pra frente>`
- Registre também o que ele elogiar, no mesmo formato ("Gostou").
- Se uma entrada contradizer esta skill, a entrada vence.
- Quando o mesmo motivo aparecer 3 vezes, sugira promovê-lo a regra fixa nesta skill.

## 11. Checklist antes de entregar

Revise o código contra cada item e corrija o que falhar:

- [ ] Todos os valores de tempo, easing, espaçamento e raio vêm dos tokens
- [ ] Só `transform` e `opacity` são animados
- [ ] `prefers-reduced-motion` e `:focus-visible` implementados
- [ ] Uma única cor de destaque, usada só em ações e estados
- [ ] Sticky/parallax em no máximo duas seções, desligados no mobile
- [ ] Imagens com lazy loading, dimensões definidas e origem resolvida (ou prompt de imagem entregue)
- [ ] Nenhum elemento copiado de marca ou site existente
- [ ] Testado mentalmente em 375px, 768px e 1440px

Ao entregar, liste em 2 ou 3 linhas as decisões visuais principais e, se houver imagens a gerar,
os prompts de imagem em bloco separado.
