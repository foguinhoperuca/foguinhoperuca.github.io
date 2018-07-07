---
title: Challange JR 2017-10-12 17:57:00
date: 2017-10-12 17:57:00 -0300
challenge: JR_2017-10-12_17-57-00
layout: post
categories: chess challenge
custom-javascript-list:
    - "https://code.jquery.com/jquery-3.2.1.min.js"
    - "/js/pgnvjs.js"
    - "/js/chessboard-0.3.0.js"
custom-css-list:
    - "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css"
    - "/css/pgnvjs.css"
    - "/css/chessboard-0.3.0.min.css"
---
{% assign challenge = site.data.challenges[page.challenge] %}
# Introdução

## Desafio

<!-- ![Pretas jogam e d'ao checkmate.]({{ "/images/posts/2017-10-12T17h57_CHALLENGE_JR/2017-10-12T17:57_CHALLENGE_JR_CH-01.jpg" | absolute_url }}) -->
<!-- <small>_**Pretas jogam e dão checkmate.**_</small> -->
<div id="boardProblem" style="width: 320px"></div>
<small>_**{{ challenge.descripton }}**_</small>

Neste estudo, inicialmente irei tentar responder algumas perguntas (elencadas abaixo) e posteriormente utilizarei as respostas produzidas como input para propor uma solução para o problema. Resumidamente, levarei em conta o seguinte:

* Análise Numérica
* Análise Posicional
* Empatia

Após essa análise inicial é possível utilizar o trabalho produzido para direcionar uma solução ao problema em questão.

## Análise Numérica

**Como estão as forças de cada lado?**

### Primeiro: Análisar numericamente a pontuação de cada jogador para ter-se uma visão geral das suas forças.

Brancas: 1 rei (óbvio); 1 rainha; 1 torre; 1 cavalo; 5 peões; TOTAL: 22 pts.
Pretas: 1 rei (óbvio); 1 rainha; 1 torre; 1 bispo; 6 peões; TOTAL: 23 pts.

Veja a tabela para ficar mais fácil a comparação:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">
  <colgroup>
	<col  class="org-left" />
	<col  class="org-left" />
	<col  class="org-right" />
	<col  class="org-right" />
	<col  class="org-right" />
	<col  class="org-right" />
  </colgroup>
  <thead>
	<tr>
	  <th scope="col" class="org-left">Peça</th>
	  <th scope="col" class="org-left">Valor</th>
	  <th scope="col" class="org-right">QNT Branca</th>
	  <th scope="col" class="org-right">Branca Pts</th>
	  <th scope="col" class="org-right">QNT Pretas</th>
	  <th scope="col" class="org-right">Preta Pts</th>
	</tr>
  </thead>
  <tbody>
	<tr>
	  <td class="org-left">Rei (K)</td>
	  <td class="org-left">+ Inf</td>
	  <td class="org-right">1</td>
	  <td class="org-right">-</td>
	  <td class="org-right">1</td>
	  <td class="org-right">-</td>
	</tr>
	<tr>
	  <td class="org-left">Rainha (Q)</td>
	  <td class="org-left">+ 9</td>
	  <td class="org-right">1</td>
	  <td class="org-right">9</td>
	  <td class="org-right">1</td>
	  <td class="org-right">9</td>
	</tr>
	<tr>
	  <td class="org-left">Torre (T)</td>
	  <td class="org-left">+ 5</td>
	  <td class="org-right">1</td>
	  <td class="org-right">5</td>
	  <td class="org-right">1</td>
	  <td class="org-right">5</td>
	</tr>
	<tr>
	  <td class="org-left">Bispo (B)</td>
	  <td class="org-left">+ 3</td>
	  <td class="org-right">0</td>
	  <td class="org-right">0</td>
	  <td class="org-right">1</td>
	  <td class="org-right">3</td>
	</tr>
	<tr>
	  <td class="org-left">Cavalo (N)</td>
	  <td class="org-left">+ 3</td>
	  <td class="org-right">1</td>
	  <td class="org-right">3</td>
	  <td class="org-right">0</td>
	  <td class="org-right">0</td>
	</tr>
	<tr>
	  <td class="org-left">Peão (P)</td>
	  <td class="org-left">+ 1</td>
	  <td class="org-right">5</td>
	  <td class="org-right">5</td>
	  <td class="org-right">6</td>
	  <td class="org-right">6</td>
	</tr>
  </tbody>
  <tbody>
	<tr>
	  <td class="org-left">TOTAL</td>
	  <td class="org-left">&#xa0;</td>
	  <td class="org-right">-</td>
	  <td class="org-right">22</td>
	  <td class="org-right">-</td>
	  <td class="org-right">23</td>
	</tr>
  </tbody>
</table>


### Segundo: Quais as semelhanças?

No caso, ambos os lados possuem peças grandes em força igual (rainha e torre sendo 1 peça para cada).

### Terceiro: Quais as diferenças?

No caso, a diferença começa no ranking inferior: as brancas possuem um cavalo e as pretas possuem um bispo. Isto por si só enseja um repertório diferente para cada lado que deve ser considerado na hora de montar a sua estratégia.

Além da diferença no ranking inferior, na base (peões) há uma ligera superioridade para as pretas considerando a vantagem de 1 peça (5 X 6). **Será que essa superioridade pode ser refletida na sua estratégia?**

## Análise Posicional.

**Análise posicional é legal pois ela, de certa forma, conta a história do jogo e é importante saber como chegamos aonde estamos pois teremos uma pista do que o adversário está pensando e o que ele pretende fazer.**

Uma vez análisado numéricamente as forças, faz-se uma análise do posicionamento das peças no tabuleiro o que pode levar a detectar algum padrão já conhecido de jogo (e assim desenvolver a sua estratégia de forma mais embasada).

### Quem está em posição de ataque/defesa?

As pretas estão em uma posição mais agressiva pois a **rainha** está atacando a torre e o cavalo com um **fork**. As **pretas** também tem o bispo, a sua torre e o ph4 **encurralando o rei branca**.

Já as brancas estão em uma posição mais defensiva, com a **rainha** branca **sobrecarregada** guardando a torre, o cavalo e a fileira 1 que dá acesso diretamente ao rei. As brancas não possui nenhuma peça em posição de ataque diretamente.

### O que está sendo ameçado/cobiçado?

Olhando com atenção é possível notar que a chave para o jogo é o rank 1 que está guardado pelo sobrecarregada rainha branca.

### Existe algum padrão/tática comum desenhada no tabuleiro?

O padrão que chama mais a atenção é o **overloading** (quando uma peça está sobrecarregada por várias funções no tabuleiro): a rainha branca está com muitas responsabilidades com a defesa da torre, cavalo e rank 1 (e consequentemente o rei).

Outro padrão em destaque é o **pin**: a torre branca está defendendo a rainha branca mas está presa não podendo sair para atacar sob pena de desguarnecer a rainha branca.

Finalmente, há uma **cadeia** com 2 peões brancos protegendo o rei. A estrutura de cadeia dos peões pe forte contra a torre mas fraca contra bispo/rainha já que essas peças podem passar pela diagonal.

## Empatia.

Sim! O conceito de empatia, de maneira simplificada, é colocar-se no lugar do outro. Aparentemente, esse conceito não tem nada haver com o xadrez mas se você tentar colocar-se na pele do seu adversário e tentar entender como ele funciona e qual a sua estratégia você pode conseguir alguma pista da melhor estratégia a ser adotada para atingir o objetivo proposto pelo desafio.

### Quais são os objetivos originais do meu adversário?

Considerando o meu adversário como as Brancas, podemos especular o seguinte:

* __Defesa__: o rei está de certa forma exposto (apesar de não diretamente mas existem caminhos que levam o rei a levar check). A rainha está sendo atacada indiretamente e a torre está sendo ameaçada diretamente. Já o cavalo também está sendo ameaçado diretamente. A maioria dos peões não encontram-se em posição de ameaça.
* **Ataque**: A rainha, torre, cavalo e nem peões estão efetivamente atacando alguma peça.

Pode-se conjecturar que as Brancas estão em uma posição desfavorável porém não há nenhum ataque direto, forte, iminente no rei ou em qualquer outra peça grande (rainha e torre) que possa colocar uma pressão grande sobre as Brancas. Até as peças menores (cavalo e os peões) estão de certa forma aliviados.

# Solução Proposta.


<input type="button" id="showSolutionBtn" value="Show/Hide" />
<div id="solution">
<div id="boardSolution"></div>

</div>

O coração da solução é a combinação do sacrifício da rainha em nome de uma abertura na defesa já fraca do rei + sequência de check que imobilizará o rei a ponto de conseguir-se o almejado check-mate.

0. **...; q X Rc2**: _Sacrifício da rainha preta ao tomar a torre branca_
1. **Q X qc2; tf1+**: A rainha branca é atraida pela oferta vantajosa de trocar uma torre por uma rainha. As pretas aproveitam-se que a rainha branca desguarneceu o rank 1 e ataca o rei branco
2. **Kh2; bg1+**: O rei branco foge para o rank 2. O bispo preto ataca o rei defendido pela torre que está no rank 1
3. **Kh1; bf2+**: O rei branco foge novamente para o rank 1. O bispo preto sobe para o rank 2 dando um ataque descoberto no rei com a torre. Note que mesmo o bispo exposto ao ataque do cavalo, o descoberto no rei força as brancas ignorarem momentaneamente o bispo preto
4. **Kh2; bg3++**: Novamente o rei branco preisa fugir para o rank 2; O bispo negro vai atacar o rei branco apoiado pelo ph4. Este ataque culmina em um checkmate pois não há para onde o rei branco fugir ou peça que possa cobrir os ataques e nem mesmo atacar as peças de ataque das pretas.


# Conclusão.

O presente trabalho é uma referência de como eu produzi a solução para o problema proposto com a pretensão de ser uma referência futura para outras análises e para que eu possa aperfeiçoar o meu método de análise, ajudando a melhorar o meu repertório e fazer minhas análises em um menor tempo com a mesma ou melhor qualidade.

Assim, o trabalho está divido em 2 aspectos principais: coleta de informações de como apresenta-se o problema juntamente com uma análise dos dados obtidos e outro aspecto que é partindo do resultado obtido no primeiro aspecto, elaborar uma proposta para resolver o problema.

Notar que a solução proposta não valeu-se da sua vantagem numérica de peões (vantagem acabou sendo irrelevante para solução proposta).

Se o sacrifício da rainha preta não tivesse sido aceito, as brancas perderiam a torre e possívelmente o cavalo ou a rainha branca, deixando o jogo desequilibrado em favor das pretas.

Durante a coleta de dados e análise foram considerados algumas heurísticas:

* Tratar da peça mais forte para peça mais fraca (para economizar tempo na análise);
* Comparar o meu repertório de táticas, um a um de forma sistemática, com o problema apresentado;

# Referências.

* Eu mesmo =). Essa análise partiu da minha reflexão sobre o problema;
* [Temas táticos - chesstempo.com](https://pt.chesstempo.com/tactical-motifs.html "Site com vários temas para estudo de táticas.")

<script>
	var boardProblem = pgnEdit('boardProblem', {
		position: '{{ challenge.fen }}',
		pieceStyle: 'wikipedia',
		theme: 'blue',
		orientation: 'black'
	});

	function solution() {
		pgnView('boardSolution', {
			position: '{{ challenge.fen }}',
			pgn: '{{ challenge.pgn }}',
			pieceStyle: 'wikipedia',
			theme: 'informator',
			orientation: 'black'
		});
	}

	$("#showSolutionBtn").click(function(){
		solution();
		$("#solution").toggle();
	});

	$(document).ready(function(){
		solution();
		$("#solution").hide();
	});
</script>
