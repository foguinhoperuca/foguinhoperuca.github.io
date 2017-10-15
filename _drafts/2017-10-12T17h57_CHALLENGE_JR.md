---
layout: post
title: Challange JR 2017-10-12 17:57:00
date: 2017-10-12 17:57:00 -0300
categories: chess games challenge
---

# Desafio

<IMAGE_GOES_HERE>

Pretas jogam e dão checkmate.

Neste estudo, inicialmente irei tentar responder algumas perguntas (elencadas abaixo) e posteriormente utilizarei as respostas produzidas como input para propor uma solução para o problema. Resumidamente, levarei em conta o seguinte:

* Análise Numérica
* Análise Posicional
* Empatia

Após essa análise inicial é possível utilizar o trabalho produzido para direcionar uma solução ao problema em questão.

## Análise Numérica

Como estão as forças de cada lado?

### Primeiro: análisar numéricamente a pontuação de cada jogador para ter-se uma visão geral das suas forças:

Brancas: 1 rei (óbvio); 1 rainha; 1 torre; 1 cavalo; 5 peões; TOTAL: 22 pts.
Pretas: 1 rei (óbvio); 1 rainha; 1 torre; 1 bispo; 6 peões; TOTAL: 23 pts.

Veja a tabela para ficar mais fácil a comparação:

// FIXME use markdown table
|----------------------+------------+------------+------------+-----------|
| Peça                 | QNT Branca | Branca Pts | QNT Pretas | Preta Pts |
|----------------------+------------+------------+------------+-----------|
| Rei (K)    : + Inf   |          1 |          - |          1 |         - |
| Rainha (Q) : + 9 pts |          1 |          9 |          1 |         9 |
| Torre (T)  : + 5 pts |          1 |          5 |          1 |         5 |
| Bispo (B)  : + 3 pts |          0 |          0 |          1 |         3 |
| Cavalo (N) : + 3 pts |          1 |          3 |          0 |         0 |
| Peão (P)   : + 1 pt  |          5 |          5 |          6 |         6 |
|----------------------+------------+------------+------------+-----------|
| TOTAL                |          - |         22 |          - |        23 |
|----------------------+------------+------------+------------+-----------|

### Segundo ponto a notar: quais as semelhanças?

No caso, ambos os lados possuem peças grandes em força igual (rainha e torre sendo 1 peça para cada).

### Terceiro ponto a notar: quais as diferenças?

No caso, a diferença começa no ranking inferior: as brancas possuem um cavalo e as pretas possuem um bispo. Isto por si só enseja um repertório diferente para cada lado que deve ser considerado na hora de montar a sua estratégia.

Além da diferença no ranking inferior, na base (peões) há uma ligera superioridade para as pretas considerando a vantagem de 1 peça (5X6). **Será que essa superioridade pode ser refletida na sua estratégia?**

## Análise Posicional.

**Análise posicional é bacana pois ela, de certa forma, conta a história do jogo e é importante saber como chegamos aonde estamos (uma pista para prever o futuro é conhecer o passado e com base no direcionamento das ações conjecturar o futuro).**

Uma vez análisado numéricamente as forças, faz-se uma análise do posicionamento das peças no tabuleiro o que pode levar a detectar algum padrão já conhecido de jogo (e assim desenvolver a sua estratégia de forma mais embasada).

Disposição das peças

### Quem está em posição de ataque/defesa?

### O que está sendo ameçado/cobiçado?

### Existe algum padrão/tática comum desenhada no tabuleiro?

## Empatia.

Sim! O conceito de empatia, de maneira simplificada, é colocar-se no lugar do outro. Aparentemente, esse conceito não tem nada haver com o xadrez mas se você tentar colocar-se na pele do seu adversário e tentar entender como ele funciona e qual a sua estratégia você pode conseguir alguma pista da melhor estratégia a ser adotada para atingir o objetivo proposto pelo desafio.

### Quais são os objetivos originais do meu adversário?

Considerando o meu adversário como as Brancas, podemos especular o seguinte:

* **Defesa**: o rei está de certa forma exposto (apesar de não diretamente mas existem caminhos que levam o rei a levar check). A rainha está sendo atacada indiretamente e a torre está sendo ameaçada diretamente. Já o cavalo também está sendo ameaçado diretamente. A maioria dos peões não encontram-se em posição de ameaça.

* **Ataque**: A rainha, torre, cavalo e nem peões estão efetivamente atacando alguma peça.

Pode-se conjecturar que as Brancas estão em uma posição desfavorável porém não há nenhum ataque direto, forte, iminente no rei ou em qualquer outra peça grande (rainha e torre) que possa colocar uma pressão grande sobre as Brancas. Até as peças menores (cavalo e os peões) estão de certa forma aliviados.

# Solução Proposta.

// TODO Notar que a solução proposta não valeu-se da sua vantagem numérica de peões (vantagem acabou sendo irrelevante para solução proposta)

// TODO js to show/hide content

O coração da solução é a combinação do sacrifício da rainha em nome de uma abertura na defesa já fraca do rei + sequência de check que imobilizará o rei a ponto de conseguir-se o almejado check-mate.

0. Sacrifício 
1. torre
2. bispo
3. bispo
4. bispo
