# DESIGN.md

Portfólio de Pedro Cauã. Base: tokens, fontes e trilho do `index (1).html` atual. Valores marcados com **novo** não existem no código ainda; os demais já existem.

## História da página

Desenvolvedor que constrói software que as pessoas conseguem usar, e usa IA para trabalhar melhor.

Implicação: o produto usável (Nodify, acessibilidade) é o fim e a IA é o meio. O h1 atual ("Faço agentes de IA trabalharem como um time de engenharia") inverte essa ordem. [PENDENTE: decidir se o h1 muda para seguir a história]

## Tese visual

Um painel de engenharia em azul de planta e amarelo de sinalização: o portfólio de quem trabalha com agentes se mostra como um log de execução legível, em que cada seção é uma etapa e cada troca de fundo é a passagem para a próxima.

## Detalhe do assunto

- **Log de execução**: linhas em mono com `✓`, `…` e `→` (hoje no `.trace` do hero). Rótulos, contadores e eyebrows usam o mesmo registro.
- **Coordenadas de Brasília** no eyebrow do início (`15°47′S 47°53′W`), como carimbo de local.
- **O nó de agente**: círculo com anel e 3 satélites em `--accent`, a assinatura gráfica que muda de pose a cada seção. É o único elemento ilustrado da página.

## Ousadia em um lugar só

A cena do Nodify é a ilha escura da página (no tema claro também). O resto fica quieto: cortes de cor discretos, sem degradês, sem sombra forte.

## Mapa das seções

Implementado: início, faixa de tecnologias, projetos (pin horizontal), Nodify em ação (pin), agentes no trabalho (pin), habilidades (abas), trajetória (carrossel), sobre e contato. Tons por seção: accent (início, agentes), dark (faixa, projetos, trajetória, contato) e paper (Nodify, habilidades, sobre). Capacidades e o card AlavancaquIA saíram como seções; o conteúdo vive na aba IA e dados.

Tabela do brief inicial, mantida como referência:

| Seção prevista | Hoje no HTML | Observação |
|---|---|---|
| início | `#inicio` | igual |
| agentes | `#metodo` | passos e princípios |
| jarvis | card 1 de `#projetos` | vira seção própria |
| nodify | card 2 de `#projetos` | vira seção própria, escura |
| trajetória | `#experiencia` + `#certificados` | carrossel único |
| contato | `#contato` | igual |
| sem lugar definido | `#capacidades` e card AlavancaquIA | [PENDENTE: onde ficam]. Até decidir, usam os tokens de início. |

## Cores

### Tokens base

| Token | Claro | Escuro | Uso |
|---|---|---|---|
| `--bg` | `#EAEFF5` | `#0A1325` | fundo do início e da página |
| `--surface` | `#F7F9FC` | `#111D36` | cartões e painéis |
| `--fg` | `#0E1A2E` | `#E7EDF8` | texto principal |
| `--muted` | `#4A5A74` | `#9AA9C4` | texto de apoio |
| `--line` | `#C6D1DF` | `#24365C` | bordas e divisórias (decorativo) |
| `--accent` | `#1E3FE0` | `#8CA4FF` | ação, eyebrow, links, progresso |
| `--on-accent` | `#FFFFFF` | `#0A1325` | texto sobre `--accent` |
| `--signal` | `#F7C21B` | `#FFCB2E` | só como preenchimento (marca-texto, selo). Nunca como texto: 1,4:1 sobre o fundo claro. |
| `--ok` | `#0F6B44` **novo** (era `#16794F`) | `#5BD99C` | `✓` e estados concluídos |

`--ok` escureceu no claro porque `#16794F` dá 4,2:1 sobre o fundo de agentes.

### Fundo chapado por seção

Cada seção troca de cor no corte da borda, sem degradê. Tokens novos: `--sec-bg` e `--sec-surface`, aplicados por seção. Texto, `--muted`, `--accent` e `--ok` seguem a tabela de tokens base, exceto no Nodify do tema claro, que usa os valores do tema escuro.

| Seção | `--sec-bg` claro | `--sec-surface` claro | `--sec-bg` escuro | `--sec-surface` escuro |
|---|---|---|---|---|
| início | `#EAEFF5` | `#F7F9FC` | `#0A1325` | `#111D36` |
| agentes | `#D9E3F5` | `#F7F9FC` | `#0F1C3A` | `#16264A` |
| jarvis | `#F4EDCB` | `#FBF8E8` | `#1C1B0F` | `#282511` |
| nodify | `#0E1A2E` (tokens do tema escuro) | `#16264A` | `#050A16` | `#0C1731` |
| trajetória | `#DCE5F1` | `#F7F9FC` | `#0D1830` | `#14264D` |
| contato | `#FBE9A6` | `#FFF8DC` | `#2A2308` | `#3A3110` |

Jarvis e contato são tons do amarelo de sinalização, não creme: continuam com tinta azul e fontes sem serifa.

### Contraste (WCAG 2.2, calculado)

Texto normal 4,5:1, texto grande e componentes 3:1. Todas as combinações abaixo passam.

| Seção | Claro: fg / muted / accent / ok | Escuro: fg / muted / accent / ok |
|---|---|---|
| início | 15,1 / 6,0 / 6,4 / 5,7 | 15,8 / 7,8 / 7,8 / 10,5 |
| agentes | 13,5 / 5,4 / 5,7 / 5,1 | 14,3 / 7,1 / 7,1 / 9,5 |
| jarvis | 14,8 / 5,9 / 6,3 / 5,6 | 14,7 / 7,3 / 7,3 / 9,8 |
| nodify | 14,8 / 7,3 / 7,4 / 9,8 | 16,8 / 8,3 / 8,4 / 11,2 |
| trajetória | 13,7 / 5,5 / 5,8 / 5,2 | 15,0 / 7,4 / 7,5 / 10,0 |
| contato | 14,4 / 5,8 / 6,1 / 5,4 | 13,3 / 6,6 / 6,6 / 8,8 |

- Texto sobre o cartão (`--sec-surface`): pior caso `--muted` 6,3:1 no claro (nodify) e 5,4:1 no escuro (contato).
- Botão primário (`--fg` sobre `--bg`): 15,1:1 no claro.
- Marca-texto: no tema claro, `--fg` sobre `--signal` dá 10,5:1. No escuro, o texto dentro de `mark` deve ser `#0A1325` (12,2:1). Hoje o `mark` mantém `--fg` claro sobre amarelo, 1,3:1, e **falha**.

### Cortes

No claro, os cortes entre seções vizinhas têm pouca diferença de luminância (1,05 a 1,12) e se apoiam no matiz; o único corte forte é a entrada e a saída do Nodify (14:1). No escuro, os cortes ficam entre 1,03 e 1,14. Por isso, toda borda de seção leva uma divisória pontilhada (`1px dashed var(--line)`).

### Trilho e barra do topo

Trilho lateral e barra superior pegam os tokens da seção que cruza o meio da tela. No Nodify do tema claro, passam para texto claro. O contraste é o da tabela acima.

## Tipografia

Atualizado na implementação: as fontes do brief inicial foram trocadas por estas.

| Papel | Fonte | Uso | Escala |
|---|---|---|---|
| Títulos gigantes | Big Shoulders Display 800, caixa alta | nome do início, h2 das seções, números | nome `clamp(72px, 14vw, 200px)` (mobile `clamp(88px, 30vw, 180px)`). h2 `clamp(46px, 7vw, 96px)`. Contato `clamp(52px, 11vw, 150px)`. |
| Texto | Instrument Sans 400 e 600 | parágrafos, botões, rótulos de navegação | corpo 1,0625rem/1,6. Lede 1,125rem. |
| Rótulos | JetBrains Mono 400 e 500 | eyebrow, chips, datas, log | 0,75rem, caixa alta, tracking 0,08em |

Fallbacks: `Arial Narrow, Segoe UI, system-ui` para títulos, `Segoe UI, system-ui` para texto e `ui-monospace, SFMono-Regular, Menlo` para rótulos. `font-display: swap` pelo Google Fonts. Só os pesos usados são pedidos.

## Espaçamento e forma

- Seção: `padding-block: clamp(56px, 8vw, 112px)`.
- Gutter lateral: 16px mínimo, somado a `env(safe-area-inset-*)`.
- Largura máxima: 1280px. Trilho 200px a partir de 1040px, com 56px de respiro.
- Leitura: cabeçalho de seção até 46rem, lede até 40rem, texto corrido até 52rem.
- Escala: 4, 8, 12, 16, 24, 32, 56, 112.
- Raios: cartão grande 10px, cartão pequeno 6px, botão e chip 999px.
- Sombra: só em painéis grandes, `0 28px 56px -36px var(--shadow)`. Cartões menores só com borda.
- Grão: SVG `feTurbulence` inline, opacidade até 0,06, só nos fundos de seção.

## Movimento

### Tokens

| Token | Valor | Uso |
|---|---|---|
| `--dur-fast` | 200ms | hover, foco, botão |
| `--dur-base` | 350ms | estado de passo, borda de cartão |
| `--dur-slow` | 600ms | entrada de grupo, contador |
| `--dur-scene` | 1000ms | troca de pose do nó de agente |
| `--stagger-item` | 60ms | grupos de habilidades, cartões |
| `--stagger-word` | 100ms | revelação de título por palavra |
| `--ease-out` | `cubic-bezier(0.215, 0.61, 0.355, 1)` (GSAP `power3.out`) | entradas e trocas de pose |
| `--ease-soft` | `cubic-bezier(0.25, 0.46, 0.45, 0.94)` (GSAP `power1.out`) | revelação por palavra |
| `--ease-inout` | `cubic-bezier(0.65, 0, 0.35, 1)` | cenas fixas e movimento horizontal |

### Regras de scroll

- Scroll suave com Lenis: `duration` 1,2, saída exponencial (`t => Math.min(1, 1.001 - 2 ** (-10 * t))`).
- Revelação de título: de `top 90%` a `top 50%`, `scrub: true`, opacidade de 0,35 a 1 por palavra.
- Parallax decorativo: `scrub: 1`, deslocamento máximo de ±10% (`yPercent`).
- Cenas fixas: agentes `+=250%`, nodify `+=350%`. Em tela estreita, sem pin.
- Troca de pose do nó: `overwrite: true`, `--dur-scene`, `--ease-out`.

### O que não anima

- Texto corrido, cartões de certificado ao filtrar, trilho e barra de progresso (acompanham o scroll sem easing próprio).
- Nada nasce em `opacity: 0` esperando gatilho: o conteúdo é legível sem JavaScript.
- **Estado inativo nunca baixa a opacidade do texto.** O passo inativo a 0,62 dá corpo `--muted` em 2,6:1 no claro (3,5:1 no escuro), abaixo de AA. O estado inativo muda de cor (título e corpo em `--muted`, círculo vazio) e mantém `opacity: 1`.
- `prefers-reduced-motion: reduce`: Lenis desligado, nenhum pin, parallax, scrub ou pose. O nó fica na pose do início, estático, e tudo aparece no estado final.

## Componentes

- **Botão**: pílula, borda `--fg`. Primário preenche com `--fg` e texto `--bg`. Pequeno usa borda `--line` e texto `--muted`. Hover sobe 1px em `--dur-fast`.
- **Cartão**: `--sec-surface`, borda 1px `--line`, raio 10px. Sem sombra, salvo painéis grandes.
- **Chip**: pílula mono, borda `--line`, texto `--muted`. Variante "em uso": texto e borda `--ok`.
- **Log de execução**: grade `20px | 8,5rem | texto`, linhas separadas por `--line`, `✓` em `--ok`, `…` em `--accent`.
- **Passos**: círculo numerado de 32px sobre linha vertical. Concluído: preenchido com `--accent`, número `--on-accent`.
- **Marca-texto**: faixa `--signal` entre 58% e 92% da linha. Texto `--fg` no claro e `#0A1325` no escuro.
- **Filtros**: pílulas. Ativo: fundo `--fg`, texto `--bg`.
- **Nó de agente**: círculo, anel e 3 satélites em `--accent`, atrás do texto, `pointer-events: none`.
- **Foco**: contorno 2px `--accent`, offset 3px, visível em todo elemento interativo.
- **Navegação**: trilho lateral com linha de progresso em `--accent` (a partir de 1040px) e barra fina no topo em telas estreitas.

## Voz

Português do Brasil, primeira pessoa, direto. Frases curtas com um fato concreto cada uma (cargo, projeto, número). Diz o que fez e o que ainda é protótipo ("em desenho", "hobby"). Evita "apaixonado por", "solução inovadora", "ecossistema", "sinergia", e promessa sem prova.

## Evitar

- Roxo para azul em degradê, preto com um único neon, Inter ou Space Grotesk por reflexo.
- Creme com serifada e terracota. Jarvis e contato usam amarelo de sinalização com tinta azul e sans.
- Emoji como marcador. Os glifos `✓ ↓ →` são funcionais e ficam.
- Tudo centralizado; o mesmo raio e a mesma sombra em todos os cartões.
- `--signal` como cor de texto.
- Opacidade abaixo de 1 em texto para marcar estado.
- Efeito que esconde conteúdo até o gatilho disparar.
- Contar o que não existe: o Jarvis é hobby, os agentes `code-reviewer` e `orquestrador` estão "em desenho", o Nodify mostra "ilustração do conceito" até haver gestos e comandos reais.
