# Matemática, Conceito a Conceito

Livro infantil evolutivo: um conceito matemático novo por semana, explicado a
partir de situações reais — não a partir de definições de manual. No mesmo
espírito de "Portugal, Distrito a Distrito" e "A Europa, País a País", mas
com uma diferença importante: **este livro não tem um conteúdo fixo**, cresce
uma folha de cada vez.

## Filosofia

O objetivo não é decorar definições — é perceber a ideia por trás delas,
através de uma situação do dia a dia com a qual uma criança de 10 anos se
relacione (botões, trocos, bolachas, amigos, jogos). O nome "oficial" do
conceito só aparece no fim de cada página, como consequência de já se ter
percebido o resto — nunca como ponto de partida.

Cada tema sugere sempre uma **experiência prática** com objetos comuns de
casa, que a criança consegue fazer sozinha, sem ajuda de um adulto — o
livro é para imprimir, por isso a atividade tem de funcionar em papel
(riscar a lápis, por exemplo, como no crivo de Eratóstenes). Quando faz
sentido, essa mesma atividade é **também interativa** para quem lê
`index.html` no browser (clicar para riscar, contador ao vivo) — um extra
para a versão online, nunca uma substituição da versão em papel.

## Ficheiros

| Ficheiro | O que é |
|---|---|
| `index.html` | O livro. Abre no browser; cada tema é uma folha (`.folha.folha-tema`) escrita à mão. |
| `dados-temas.js` | Registo leve **só para o índice e o contador da capa** — não gera o conteúdo das páginas. |
| `.claude/skills/pagina-matematica/` | Skill para acrescentar um tema novo por semana, mantendo o tom e o formato. |
| `.claude/skills/pagina-matematica/destinatarios.txt` | Lista de emails a avisar quando sai um tema novo (um por linha). **Não vai para o git.** |

## Como usar

1. Abre `index.html` num browser (Chrome de preferência).
2. Exportar: **Imprimir → Guardar como PDF**, tamanho **A4**, margens **Nenhumas**,
   com **"Gráficos de fundo"** ativado.

## Acrescentar um tema novo

Diz "quero uma página sobre [tema]" — a skill `pagina-matematica` trata do
resto: escreve a folha nova em `index.html` (antes do marcador
`PRÓXIMO TEMA` perto do fim do `<body>`) e acrescenta a entrada correspondente
a `dados-temas.js`.

**Cada tema ocupa sempre duas páginas** — página 1 para a ideia, página 2
para a experiência — mas dentro delas o layout é livre, adaptado ao que
fizer mais sentido para esse conceito. A página 1 tem um `id` (`tema-<id>`)
para onde o Índice aponta diretamente. Há uma caixa de ferramentas visual
comum (classes CSS já definidas em `index.html`) para manter o livro
coerente:

| Classe | Para quê |
|---|---|
| `.situacao` | O gancho do dia a dia que abre o tema. |
| `.experimenta` | Atividade prática, sem supervisão de adulto. |
| `.para-recordar` | Frase curta para fixar — não é a definição formal. |
| `.curiosidade-tema` | Um facto real para guardar e contar. |
| `.nota-formal` | O nome/definição oficial, pequena e no fim da página. |

## Aviso por email

**O gatilho é o `git commit`, não a escrita da página.** Escrever, rever e
afinar um tema não envia nada — só quando pedes um commit e esse commit
acrescenta uma entrada nova a `dados-temas.js` (ou seja, publica mesmo um
tema) é que sai um email curto (título + gancho + início da situação real +
link para a página) às pessoas listadas em `destinatarios.txt`. Um commit
só de estrutura/estilo/correções não dispara nada.

Para ativar:

1. Autoriza a ligação Gmail em claude.ai → definições → conectores (só se
   faz uma vez).
2. Edita `.claude/skills/pagina-matematica/destinatarios.txt` e põe lá os
   emails, um por linha.

Sem isto configurado, a skill simplesmente não envia nada — o resto do
fluxo (escrever e publicar o tema) funciona à mesma.

## Créditos

- Tipografia: Fraunces / Work Sans / IBM Plex Mono (Google Fonts) — mesma
  família visual dos outros livros da coleção.
- Texto elaborado com recurso a IA; sem fins comerciais.
