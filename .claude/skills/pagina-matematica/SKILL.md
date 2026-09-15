---
name: pagina-matematica
description: 'Use quando o utilizador pedir uma página/tema novo para o livro-matematica ("quero uma página sobre X", "acrescenta o tema Y", "novo conceito matemático"), OU quando pedir para publicar/fazer commit/subir alterações neste repositório (para decidir se há aviso por email a enviar). Escreve uma folha nova em index.html seguindo o tom pedagógico e o formato visual do livro, regista o tema em dados-temas.js, e avisa por email quando um commit publica um tema novo (nunca em commits só de estrutura/estilo).'
---

# Página nova para o livro-matematica

O livro-matematica é um livro infantil **evolutivo**: cresce um tema por
semana. Cada tema ocupa sempre **duas folhas A4** (`.folha.folha-tema`)
escritas à mão em `index.html` — página 1 para a ideia, página 2 para a
experiência (ver "Estrutura fixa: 2 páginas" abaixo). Dentro dessas duas
páginas não há um template rígido: o layout deve adaptar-se ao conceito,
não o contrário.

## Regra de ouro

**A situação real vem primeiro, o nome do conceito vem por último.**

O livro destina-se a uma criança de 10 anos (5º ano de escolaridade), sem
supervisão de adulto. O
objetivo não é decorar uma definição — é perceber a ideia através de algo
que a criança já vive ou consegue experimentar (trocos, bolachas, jogos,
irmãos, animais, desportos, tempo, dinheiro da semanada). A definição
formal, quando existe, é sempre a última coisa da página, em letra pequena,
como uma etiqueta que só faz sentido depois de já se ter percebido tudo.

Nunca escrevas a página ao contrário (definição → exemplos). Se um conceito
não tiver uma situação real óbvia, procura-a com mais cuidado antes de
escrever — quase sempre existe (frações → dividir uma piza; percentagens →
descontos numa loja; negativos → temperaturas ou dívidas; probabilidade →
jogos de sorte; perímetro/área → o quintal ou o quarto).

## Antes de escrever

1. Lê `index.html` para veres o layout do tema já existente ("Números
   primos") e a caixa de ferramentas CSS disponível (ver tabela abaixo).
   Isto dá o tom e o nível de linguagem a seguir.
2. Pensa numa situação real e concreta ligada à vida de uma criança de 10
   anos — nunca uma situação abstrata ou "de manual".
3. Decide que peças da caixa de ferramentas fazem sentido para este
   conceito em concreto. Não é obrigatório usar todas, nem pela mesma
   ordem da página anterior.

## Caixa de ferramentas visual (classes já definidas em `index.html`)

| Classe | Para quê | Obrigatória? |
|---|---|---|
| `.tema-eyebrow` / `.tema-titulo` / `.tema-gancho` | Cabeçalho do tema (número da semana, data, título, frase de gancho) | Sim — todas as páginas começam assim |
| `.situacao` | O gancho do dia a dia — a primeira coisa que a criança lê a seguir ao título | Sim |
| `.tema-texto` | Parágrafos de explicação livre, fora de caixa | Conforme necessário |
| `.experimenta` | Atividade prática com objetos comuns de casa, sem adulto — é o corpo da página 2 | Sim — ver secção abaixo |
| `.para-recordar` | Frase curta e memorável, não é a definição formal | Recomendada |
| `.curiosidade-tema` | Um facto real do mundo, para guardar e contar a alguém | Opcional, boa quando existir algo genuinamente interessante |
| `.nota-formal` | Nome/definição oficial, sempre no fim, sempre pequena | Sim, exceto se o conceito não tiver mesmo um nome formal a introduzir |

Se um conceito pedir uma peça visual nova (uma grelha, uma linha do tempo,
um diagrama), cria a classe CSS nova dentro do bloco de estilos existente
(mesma paleta: `--quadro`, `--laranja`, `--giz`, `--paper`, `--ink`) em vez
de inventar uma paleta ou tipografia diferente — o livro é uma coleção, tem
de parecer o mesmo objeto de semana para semana.

## Sobre a "Experimenta"

Base: sempre uma atividade física e real, com materiais que quase todas as
casas têm (moedas, botões, Lego, lápis e papel, comida da cozinha, o
próprio corpo/passos, um relógio) — isto é o que garante que o livro
impresso funciona sozinho, sem ecrã nenhum.

**Por cima disso**, quando a atividade se prestar (contar, riscar, agrupar,
ordenar, combinar), torna-a também clicável para quem está a ler
`index.html` no browser — é uma oferta extra para quem lê online, nunca uma
substituição da versão em papel. Padrão a seguir (ver `grelha-crivo` do
tema "Números primos" como exemplo completo):

- Gera os elementos por JS a partir de um array simples (números, cartas,
  etiquetas — o que fizer sentido), com uma classe `interativa` no
  contentor e `data-*` no que for preciso.
- Um clique **alterna** um estado visual (ex.: `.riscado`) — nunca navega
  para outro sítio nem depende de rede.
- Se ajudar a fechar o ciclo, mostra um contador ao vivo (ex.: "Por riscar:
  N") e um botão pequeno "🔄 Recomeçar" que limpa o estado.
- Esconde os controlos que só fazem sentido no ecrã (o botão de recomeçar,
  dicas de "clica aqui") com `@media print{ display:none; }` — no papel a
  criança usa lápis, o resto do conteúdo mantém-se igual.
- Vanilla JS, sem bibliotecas novas nem `localStorage` — é um exercício de
  uma sessão, não precisa de guardar estado entre visitas.
- **Feedback imediato, mas não intrusivo**: cada clique tem de mostrar logo
  que aconteceu algo — uma transição/animação curta (150–250ms) no próprio
  elemento clicado, como o `pop` (scale) e a mudança de cor já usados na
  grelha do crivo. Nunca `alert()`, `confirm()` ou toasts/modais a
  interromper — o feedback vive sempre dentro do próprio elemento ou ao
  lado dele (ex.: o contador "Por riscar: N" a reagir também com `pop`).

## Estrutura fixa: 2 páginas

Cada tema usa sempre exatamente **duas folhas** (`.folha.folha-tema`):

- **Página 1 — a ideia**: cabeçalho (`.tema-eyebrow` / `.tema-titulo` /
  `.tema-gancho`), `.situacao`, os parágrafos de explicação
  (`.tema-texto`), e normalmente `.para-recordar` e/ou
  `.curiosidade-tema` se couberem confortavelmente.
- **Página 2 — a experiência**: repete o `.tema-eyebrow` com
  "· continuação", um título mais pequeno, e a `.experimenta` (incluindo a
  versão interativa quando existir). A `.nota-formal` fecha a página 2,
  encostada ao fundo (`margin-top:auto` já trata disso).

Isto é uma decisão deliberada (não um limite técnico): mantém o ritmo de
produção previsível — uma dupla de páginas por semana — mesmo sabendo que
`.folha` tem altura fixa (297mm) e `overflow:hidden`, o que corta sem aviso
qualquer conteúdo a mais. Depois de escrever as duas folhas, tira sempre um
screenshot (ex.: `chrome --headless --screenshot`, ou o skill `run`) para
confirmar que nada ficou cortado no fundo de nenhuma das páginas — e testa
também o clique da parte interativa, se existir.

## Passos para acrescentar o tema

1. Escreve as duas folhas novas em `index.html`, imediatamente **antes** do
   comentário `<!-- ⬇⬇⬇ PRÓXIMO TEMA: acrescentar a folha nova aqui, antes
   desta linha ⬇⬇⬇ -->`.
2. Cada uma é `<div class="folha folha-tema">`; a primeira folha leva
   também `id="tema-<id>"` (o mesmo `id` da entrada em `dados-temas.js` —
   é para ali que o Índice aponta) e `.tema-eyebrow` a indicar
   `Tema da semana · NN · <data de hoje>` (NN = próximo número
   sequencial); a segunda folha é igual mas sem `id` e com "· continuação"
   no eyebrow.
3. Se a experiência tiver uma versão interativa, o JS correspondente entra
   no `<script>` final, ao lado do `renderGrelhaCrivo()` existente (um
   `render<Nome>()` novo, chamado no fim do script tal como os outros).
4. Acrescenta a entrada correspondente a `dados-temas.js` (mesma ordem),
   com `id`, `titulo`, `emoji`, `resumo` (uma frase, tom de índice) e
   `dataAdicionado`.
5. Não é preciso tocar em mais nada — o contador da capa (`.n-temas`) e o
   índice atualizam-se sozinhos a partir de `dados-temas.js`.

Escrever a página **não** envia nada — o aviso por email só acontece na
publicação (ver secção seguinte). É normal escrever, rever e afinar um tema
várias vezes antes de isso acontecer.

## Aviso por email — só no commit que publica o tema, nunca ao escrever

**O gatilho é o `git commit` neste repositório, não a escrita da página.**
Só se envia email quando um commit for efetivamente pedido pelo utilizador
(nunca faças commit por iniciativa própria) **e** esse commit acrescentar
uma entrada nova a `dados-temas.js`. Isso é o sinal de "tema pronto a
publicar" — um commit que só mexe em CSS, estrutura, correções de layout,
interatividade, etc., sem entrada nova em `dados-temas.js`, **não** deve
disparar email nenhum, mesmo que toque em `index.html`.

Antes de fazer o commit pedido, olha para o diff staged
(`git diff --cached -- dados-temas.js`, ou equivalente): se acrescenta uma
entrada nova, é uma publicação de conteúdo; se não, é só estrutura.

Quando for mesmo uma publicação de conteúdo:

1. Faz o commit normalmente (mensagem describe o tema, como habitual).
2. Lê `destinatarios.txt` (nesta pasta da skill; uma linha por email,
   linhas `#` ignoradas). Vazio ou só comentários → não há ninguém
   configurado; avisa o utilizador disso e para por aqui.
3. Envia um email (via Gmail, depois de autorizado) para essas moradas:
   - **Assunto**: `Novo tema no livro: <título do tema>`
   - **Corpo**: um "teaser" — título, a frase-gancho (`.tema-gancho`) e o
     início da situação real (o primeiro parágrafo de `.situacao`, o
     suficiente para dar vontade de abrir o livro sem contar tudo) —
     seguido do link direto: `https://www.jnvasconcelos.com/livro-matematica#tema-<id>`.
   - Tom simpático e curto, como um bilhete, não como uma newsletter
     formal.
4. Diz ao utilizador para quem foi e um resumo do corpo do email — nunca
   envies em silêncio.

Se o utilizador pedir um commit que mistura as duas coisas (tema novo +
arrumação de estrutura), o critério continua a ser só "há entrada nova em
`dados-temas.js` neste commit?" — se sim, envia; a parte de arrumação não
impede o aviso.

## Tom e língua

Português europeu, segunda pessoa ("tu"), frases curtas, sem tecnicismos
desnecessários. Está bem usar humor leve e comparações do quotidiano
português. Evita qualquer coisa que soe a manual escolar.
