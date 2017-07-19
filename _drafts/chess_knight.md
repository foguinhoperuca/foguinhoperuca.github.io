---
layout: post
title: (Cavalo) Knight - Estudo Detalhado
date: 2017-05-21 22:32:00 -0300
categories: chess pieces knight 
---

# The Knight (O Cavalo).

O cavalo é a peça mais excêntrica. Seu movimento - descrito normalmente em "L" - e sua habilidade (única) de "pular" as demais peças no tabuleiro são as suas principais características.

As demais peças possuem uma relação entre os movimentos: os bispos movem-se nas diagonais por um número ilimitado de casas; as torres movem-se em linha reta por um número ilimitados de casas; a rainha comporta-se como uma junção entre o bispo e a torre movimentando-se livremente para qualquer casa na diagonal ou em linha reta desde que não haja nenhuma peça no caminho (assim como as demais peças, exceto o cavalo). Ainda temos os peões que movem-se uma casa a frente (apesar da particularidade de tomar na diagonal) e o próprio rei que movimenta-se, tal qual a rainha, livremente limitado a uma casa por vez. Assim, o cavalo demanda uma atenção especial na hora de calcular os seus movimentos pois eles não são tão óbvios quanto aos demais movimentos das outras peças.

A notação para o cavalo é a letra n de k**N**ight.

# Movimento e Forma de Tomar

Conforme mencionado anteriormente, o movimento do cavalo consistem em um L: anda-se 3 casas em linha reta **e** 2 casas à direita ou à esquerda conforme conveniência do jogador - contando já a 3 casa da linha reta como a primeira casa da virada.

As peças que eventualmente encontrarem-se no caminho serão "puladas" (desviadas) excetuando-se a peça que encontrar-se na última casa do movimento. Se for uma peça da cor oposta ela será tomada. Se for da mesma cor que o cavalo então o cavalo **não** poderá mover-se para esta casa pois a mesma já está ocupada - no xadrez duas peças não podem ocupar a mesma casa ao mesmo tempo.

FALAR SOBRE EM L PARA OS LADOS D TABULEIRO E L NA DIREÇÃO DE CIMA/BAIXO.
De uma forma geral, pode-se enxergar o movimento do cavalo no tabuleiro andando na horizontal - andando mais casas na mesma linha e depois mudando para a linha (rank) imediatamente adjacente (superior ou inferior) ou pode-se enxegar o movimento do cavalo no tabuleiro


(porém ele irá sair da sua linha - rank) indo para as linhas imediatamente superior ou inferior ou pode-se enxergar o movimento do cavalo no tabuleiro andando vertical (porém 

Pela sua característica de movimentar-se, nota-se que o cavalo não consegue atingir casas adjacente à si de forma imediata sendo necessário considerar 2 ou mais rodas para que essas casas sejam atingidas.

http://www.techiedelight.com/chess-knight-problem-find-shortest-path-source-destination/

## Casas Imediatamente Adjacentes

### Casa Diagonal.

Dada a casa atual do cavalo, para atingir a casa que fica na diagonal é necessário pelo menos 2 movimentos para atingi-la. Por exemplo, partindo do cavalo na f5 (nf5) para atingir e4, e6, g4 e g6 é necessário 2 movimentos:

**_TODO create a gif to show the moviments_**

* e4: d6 >> e4
* e6: d4 >> e6
* g4: h6 >> g4
* g6: h4 >> g6

Nota-se que para atingir a coluna adjacente é necessário ir para coluna imediatamente após e voltar para coluna adjacente. Também nota-se que para atingir a casa desejada é necessário primeiro ir para direção inversa (para atingir a casa inferior é necessário subir primeiro para depois descer).

Inicialmente, anda-se na horizontal e depois anda-se na vertical. Assim, é interessante notar, durante o movimento do cavalo, se ele não vai comprometer-se por andar horizontalmente e ser interceptado antes de chegar em seu destino.

No geral, nota-se que é preciso ir por um caminho indireto para atingir a casa desejada.

#### Hipótese de Quantidade Mínima de Passos.

Para atingir a diagonal imediata são necessários, no mínimo, 2 passos.

**_TODO provar a hipotese_**

### Casa Paralela.

3 movimentos

# Vantagens e Desvantagens

# Comportamento Inicío do Jogo, Meio do Jogo e Fim do Jogo

# Relacionamento com as Demais Peças (versus e uso combinado)

# Táticas

