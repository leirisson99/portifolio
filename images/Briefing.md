# Briefing de Design — xkintaro.com

Referência visual extraída do site **Kintaro Portfolio** (xkintaro.com), para uso por agentes de design/desenvolvimento ao reproduzir ou se inspirar no estilo. Site construído em Next.js + Tailwind CSS (v4, tokens shadcn/ui) + Framer Motion.

## Conceito geral

Portfólio pessoal de desenvolvedor full stack, com estética **monocromática radical**: preto, branco e cinzas puros, sem nenhuma cor de marca. O próprio site expõe seu manifesto em textos de rolagem contínua entre seções: "RADICAL TRANSPARENCY", "INTENTIONAL MINIMALISM", "ARCHITECTURAL INTEGRITY", "FIRST PRINCIPLES THINKING", "PERFORMANCE WITHOUT COMPROMISE", "SCALABLE VISION". O tom é técnico, direto, editorial — mistura tipografia de revista (display condensada + itálicos de ênfase) com estrutura de dashboard/terminal (numeração de seções, labels em caixa alta, monospace sutil em detalhes).

## Paleta de cores

Confirmada via variáveis CSS computadas (tokens padrão do Tailwind v4 "neutral", sem matiz — todos os valores em Lab/OKLab têm a e b em 0, ou seja, cinza puro, sem tonalidade quente ou fria):

- Fundo (background): `#0a0a0a` — quase preto
- Texto principal (foreground): `#fafafa` — quase branco
- Cards/painéis (card, popover): `#171717`
- Superfícies secundárias / muted / accent: `#262626`
- Texto secundário (muted-foreground): `#a1a1a1` — cinza médio, usado em parágrafos de apoio
- Primary (botões de destaque, ex. "CONTACT ME"): `#e5e5e5` (fundo claro) com texto `#171717` (quase preto) por cima
- Borda padrão: branco a 10% de opacidade (`rgba(255,255,255,0.1)`)
- Input/borda de campos: branco a 15% de opacidade
- Ring de foco: `#737373`
- Única cor com saturação real no sistema: `destructive` em `#ff6467` (vermelho), reservada só para estados de erro — nunca aparece na UI decorativa

Não há gradientes, nem cor de destaque secundária. Todo o contraste vem de variações de luminosidade (preto → cinza escuro → cinza médio → branco), reforçando o conceito de "intentional minimalism".

## Tipografia

- **Display / títulos (headings, logo, botões, labels)**: fonte **Syne**, peso variável 400–800, usada quase sempre em peso 800/900 (black/extrabold), *tudo em caixa alta*, com tracking bem negativo (ex. `letter-spacing: -4.8px` no H1 de 96px). É uma fonte geométrica, angulosa, de alto impacto — usada no "KINTARO", "PORTFOLIO", "ABOUT", nos números de ano do roadmap (2022–2026) e nos rótulos de seção.
- **Corpo de texto (parágrafos, descrições)**: **Inter**, peso variável 100–900, normalmente em peso regular/400 para o texto corrido e cinza médio (`#a1a1a1`) sobre fundo escuro. Palavras-chave dentro dos parágrafos recebem ênfase alternando **negrito** e *itálico* (ex.: "*Full* Stack Developer focused on building **clean** and **sustainable** systems"), criando um efeito editorial dentro da mesma frase.
- Ambas as fontes são carregadas via `next/font` (self-hosted, `font-display: swap`), sem fontes de sistema aparentes visualmente — apenas como fallback técnico.
- Labels e rótulos pequenos (nav, badges "[001]", tags de stack como "HTML"/"REACT") usam caixa alta com tracking levemente aberto, tamanho pequeno (14–16px), peso 500–700.

## Layout e estrutura

- Site em página única (single page) com seções numeradas sequencialmente: `[001] ABOUT`, `[002] STACK`, `[003] PROJECTS`, `[004] ROADMAP`, `[005] CONTACT` — cada uma com esse "eyebrow" numérico monoespaçado no canto.
- Navbar fixa no topo, fundo preto translúcido, logo "KINTARO" à esquerda em Syne bold, links de menu centralizados/à direita em caixa alta espaçada, e dois ícones circulares à direita (seletor de idioma/globo e alternância de tema claro/escuro).
- Hero: título gigante em duas linhas ("KINTARO" / "PORTFOLIO"), parágrafo de apresentação abaixo, dois CTAs (botão sólido claro "CONTACT ME" com seta, e link ghost "EXPLORE PROJECTS"), e um grid decorativo de fotos em preto e branco/dessaturadas no canto direito, com pequenos pontos/estrelas espalhados como textura de fundo. Um indicador vertical "SCROLL" com linha fina no canto direito.
- Seção Stack: abas numeradas (01 Frontend, 02 Backend, 03 Databases & ORMs, 04 Tools) listando tecnologias como pills/tags.
- Seção Roadmap: timeline vertical com linha central, pontos (dots) marcando cada ano, números de ano em tipografia gigante semi-transparente ao fundo (efeito de "número gigante atrás do texto"), alternando blocos de texto à esquerda/direita.
- Seção Projects: galeria de rolagem horizontal, cards de projeto com screenshot da interface e o nome do projeto em tipografia enorme e semi-transparente sobreposta atrás da imagem (efeito de "watermark" tipográfico).
- Footer/Contact: simples, título grande "CONTACT", e-mail de contato, ícones de redes sociais (GitHub, Discord, Instagram, LinkedIn) e copyright.
- Cantos levemente arredondados nos componentes (`border-radius` base de `0.625rem` / ~10px via token `--radius`), cards com fundo `#171717` e borda branca a 10%.

## Animações (Framer Motion) — detalhamento técnico

Analisei os bundles JS do site (não só o visual) e confirmei uso intenso da API de animação do **Framer Motion**: 21 componentes `motion.*`, 6 usos de `useScroll`, 12 de `useTransform`, 8 de `useSpring`, 6 de `whileInView`, além de `AnimatePresence` (3x) para transições de montagem/desmontagem. Valores reais extraídos do código:

- **Fade + slide-up na entrada (scroll reveal)**: padrão dominante é `opacity: 0→1` combinado com `y: 20→0` (elemento sobe 20px enquanto aparece). Também há uma variante com `x: -30→0` (entra deslizando da esquerda), usada em blocos alternados como o roadmap.
- **Scale-in**: alguns elementos (provavelmente cards e badges) entram com `scale: 0.8→1` ou `0.9→1` combinado ao fade.
- **Blur-in**: elementos passam de `blur(10px)`/`blur(15px)` para `blur(0)` conforme entram em foco — efeito de "nitidez progressiva".
- **Durações**: variam de `0.2s` a `0.6s` para microinterações (hover, botões, ícones), `0.8s`–`1.2s` para revelações de seção, e valores maiores (`1.5s`, `2s`, até `12s`) para animações contínuas como o marquee.
- **Easings**: mistura de curvas nomeadas (`easeOut` é a mais usada, depois `easeInOut`, e `linear` para movimentos contínuos/loop) com **6 curvas cubic-bezier customizadas**, ex.: `[.25,.1,.35,1]`, `[.65,0,.35,1]`, `[.22,1,.36,1]`, `[.76,0,.24,1]` — assinatura típica de site autoral com easing "afinado à mão" em vez de usar só os padrões do Tailwind.
- **Física de mola (springs)**: 8 configurações diferentes de `stiffness`/`damping` (ex. `300/25`, `100/10`, `500/2` — bem "elástico e rápido" —, `550/25`, `400/30`), usadas provavelmente no cursor, em botões magnéticos/hover e na suavização do scroll.
- **Faixas de texto em loop infinito (marquee)**: `translateX(0) → translateX(-100%)`, `linear`, `infinite` — o ticker do manifesto ("RADICAL TRANSPARENCY"...) entre seções.
- **Rotação contínua**: há um elemento com `rotate: 0→360` em loop, típico de indicador circular giratório (ex. o badge "SCROLL" ou algum ícone de status).
- **Pulse**: opacidade `1 → 0.5 → 1` em loop, efeito de "respiração" em indicadores.
- **AnimatePresence (enter/exit)**: usada em elementos que entram/saem do DOM (toggle de tema claro/escuro, menus, tooltips), com fade + leve escala/translação/blur — timing padrão `cubic-bezier(0.4, 0, 0.2, 1)`.
- **Hover states**: links ganham sublinhado (ex. "Read Full Version"), botões variam levemente opacidade/escala.
- Nada de parallax 3D pesado nem partículas animadas — as animações são discretas e funcionais, reforçando a filosofia "performance without compromise" do próprio site.

## Efeitos de rolagem (scroll-driven)

Além do scroll-reveal padrão (fade/slide ao entrar no viewport), o site usa `useScroll` + `useTransform` do Framer Motion para animações **atreladas ao progresso do scroll** (não apenas disparadas uma vez):

- **Scroll progress por seção**: `useScroll({ target: ref, offset: [...] })` é usado com dois padrões de offset — `["start start", "end end"]` e `["start center", "end center"]` — ou seja, o progresso da animação é calculado enquanto a seção atravessa a viewport, não a página inteira.
- **Parallax vertical**: valores de `y` interpolados de `"0%"` a `"-50%"` (e o inverso, `"-50%"` a `"0%"`) — camadas diferentes se movem em velocidades/direções opostas conforme o usuário rola, um parallax sutil entre texto e elementos de fundo (ex. no hero e no roadmap).
- **Galeria de projetos com "scroll horizontal" (scrollytelling)**: a seção Projects usa `scrollX`/translateX derivado do scroll vertical (9 ocorrências no código) combinado com `position: sticky` (14 ocorrências) — a seção fica "grudada" na tela enquanto o usuário rola verticalmente, e esse scroll é convertido em movimento horizontal dos cards. É exatamente o comportamento visto no site: o texto "SCROLL TO EXPLORE" antes da galeria, e os cards "Aether Media" / "Aether JS" deslizando horizontalmente por baixo do mouse mesmo com scroll vertical.
- **Foco progressivo nos cards de projeto**: os cards não focados ficam visivelmente apagados — o código confirma interpolação de `grayscale` (filtro dessaturado → colorido), `blur` (desfocado → nítido) e `opacity` (baixa → total) todas amarradas ao `scrollYProgress`. Ou seja, cada card do projeto "ganha vida" (cor, nitidez, opacidade plena) só quando chega ao centro da viewport, e volta a apagar ao sair — efeito de "spotlight" controlado pelo scroll.
- **Clip-path / wipe**: 5 usos de `clip-path` sugerem transições de revelação tipo "cortina" (a imagem ou bloco é revelado progressivamente, não só aparece com fade).
- Não há scroll-jacking agressivo de página inteira (tipo "cada scroll = 1 seção") — o efeito é mais sutil, seção a seção, mantendo a rolagem nativa do navegador na maior parte do site.

## Imagens e texturas

- Fotos pessoais e screenshots de projetos tratados em preto e branco/baixa saturação, condizente com a paleta monocromática.
- Pequenos pontos/partículas estáticas espalhadas pelo fundo do hero como textura sutil.
- Números e nomes de projeto em tamanho grande e opacidade muito baixa usados como elemento gráfico de fundo (typographic watermark), tanto no roadmap (anos) quanto nos cards de projeto (nomes).

## Stack técnico observado

Next.js, React, TypeScript, Tailwind CSS v4 (com tokens de tema shadcn/ui, paleta "neutral"), Framer Motion, tailwindcss-animate. Hospedado na Vercel.

## Resumo para o agente

Ao replicar esse estilo: usar fundo quase preto (`#0a0a0a`) com texto quase branco (`#fafafa`), zero cor de marca (apenas variações de cinza + vermelho reservado a erros), tipografia display condensada e pesada em caixa alta com tracking negativo para títulos (estilo Syne), tipografia neutra (estilo Inter) para corpo com uso pontual de negrito/itálico para ênfase editorial, seções numeradas com labels tipo "[00X]", marquees de texto em loop infinito como separadores de seção, animações de entrada suaves ao rolar a página (fade + translate), e tipografia gigante semi-transparente como elemento decorativo de fundo em títulos e cards.