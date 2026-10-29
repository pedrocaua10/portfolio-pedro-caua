# DESIGN.md

Portfólio de Pedro Cauã. Atualizado para o que está no `index.html`.

## História da página

Desenvolvedor que constrói software que as pessoas conseguem usar, e usa IA para trabalhar melhor.

## Tese visual

Abre no escuro, com blocos de barro (terracota) sobre marrom quente, um título gigante condensado e texto de leitura em uma sans humanista. Cada seção é um bloco de cor com corte seco, e o movimento aparece onde ajuda a contar a história: o trilho de projetos, o Nodify e o fluxo de agentes.

## Temas

- **Escuro (padrão):** Terracota. Abre assim para todo mundo, mesmo com o sistema em tema claro. A escolha da pessoa fica salva (`localStorage`).
- **Claro:** branco azulado com azul `#1E3FE0`.

Pesquisa que guiou o escuro: sem preto puro, texto levemente suavizado (~14:1, não 21:1), acentos dessaturados e blocos coloridos sem brilho excessivo (fontes: Material Design, Uxcel, UX Design Institute).

### Escuro, Terracota

| Tom | Fundo | Texto | Apoio | Cartão | Destaque |
|---|---|---|---|---|---|
| dark (faixa, projetos, contato) | `#1A1613` | `#EDE6DF` | `#B3A89D` | `#241E19` | `#E8B58A` |
| paper (trajetória, Nodify, habilidades) | `#221C17` | `#EDE6DF` | `#B3A89D` | `#2D2620` | `#E8B58A` |
| accent (início, agentes, sobre) | `#7E4228` | `#FBF4EE` | `#F0DCCB` | `#1A1210` | `#FBF4EE` |

Âmbar de sinalização `#E6B659` (círculo do início, selos). Todas as combinações passam AA (texto principal ≥ 14:1, blocos de cor ≥ 7:1).

### Claro

| Tom | Fundo | Texto | Apoio | Cartão |
|---|---|---|---|---|
| dark | `#0E1A2E` | `#E7EDF8` | `#9AA9C4` | `#16264A` |
| paper | `#F2F5FA` | `#0E1A2E` | `#4A5A74` | `#FFFFFF` |
| accent | `#1E3FE0` | `#FFFFFF` | `#D9E1FF` | `#0E1A2E` |

Nunca dois blocos do mesmo tom lado a lado. Ordem atual: início (accent), faixa (dark), trajetória (paper), projetos (dark), Nodify (paper), agentes (accent), habilidades (paper), sobre (accent), contato (dark).

## Tipografia

| Papel | Fonte | Uso |
|---|---|---|
| Títulos | Big Shoulders Display 800, caixa alta | nome do início, títulos de seção, números |
| Texto | Schibsted Grotesk 400, 500 e 600 | leitura, botões, rótulos, chips, datas |
| Código | JetBrains Mono 400 e 500 | só nomes de agentes e o painel de execução |

Tamanhos (tokens `--fs-*`): corpo 19px com entrelinha 1,65; lede 21px; parágrafos de cartões, trajetória e habilidades 17px; passos e gestos 16px; rótulos de 14 a 16px (mínimo 14). Título de seção `clamp(44px, 6.2vw, 88px)`; nome `clamp(72px, min(14vw, 22svh), 200px)` (celular `clamp(88px, 30vw, 180px)`). Rótulos (eyebrow, chips, datas) em minúsculas, sem espaçamento largo. `text-wrap: pretty` nos parágrafos.

## Início

O círculo âmbar ao lado dos quadrados P e C é um selo com ícone de TI/IA. Três variantes em teste (chip, nó de agente em forma de grafo, código `</>`): abrir `?icones` na URL para trocar; a escolhida fica em `localStorage` até ser fixada no código. Abaixo do texto: a linha "Busco oportunidades..." (do currículo) e os botões Ver projetos e Baixar currículo. No celular a ilustração vem depois do texto, para os botões ficarem na primeira tela.

## Números

Quatro números reais na Trajetória: 2 sistemas no TSE, 15 cursos, 220,5 horas de curso e 3 projetos. Contam de 0 ao valor ao entrar na tela (sem animação, mostram o valor final).

## Foto

Encaixe pronto no cartão do Sobre (`.mono-tile`, 96px), com o quadrado PC como reserva. Arquivos esperados: `assets/foto-pedro-288.webp` e `foto-pedro-576.webp`, quadrados, centrados no rosto, menos de 150 KB. Gerar com o script de recorte (Chrome headless) a partir da foto original.

## Idioma

Português é o padrão (nunca detecta o navegador). Botão PT/EN no cabeçalho e no menu; a troca grava `lang` em `localStorage` e recarrega. O HTML é em português; em inglês o script troca os textos por um dicionário (`EN`), inclusive datas, números, rótulos e meta tags. Currículo só existe em português e o botão em inglês avisa isso. [PENDENTE: currículo em inglês]

## Movimento

Durações 200, 350, 600 e 1000 ms; curvas `power3.out` e `power1.out`. Pins com GSAP + ScrollTrigger 3.12.2, no desktop e no celular (até 900px, com layout próprio que cabe na altura). Faixa de tecnologias e rolagem automática da trajetória em loop, com pausa. O botão de animações no cabeçalho guarda a escolha; sem escolha vale a preferência do sistema.

## Voz

Primeira pessoa, frases de tamanhos diferentes, só fatos que a pessoa deu (cargo, período, projeto, curso). Segue a skill `web-escrita-humana`: sem travessão, sem trio por reflexo, sem tom de vendedor, sem adjetivo sobre si mesmo, sem conclusão genérica.

## Evitar

- Preto puro e branco puro grandes no tema escuro.
- Rótulos em caixa alta com espaçamento largo em tudo.
- `--signal` como cor de texto.
- Opacidade baixa em texto para marcar estado (a única exceção é a revelação por palavra do "Quem sou eu?").
- Contar o que não existe: o que está em desenho aparece como "em desenho", e dado que falta fica como `[PENDENTE]`.
