---
layout: post
title: Challange JR 2018-05-12 10:09:00
date: 2018-05-12 10:09:00 -0300
categories: chess games challenge
custom-javascript-list:
    - "https://code.jquery.com/jquery-3.2.1.min.js"
    - "/js/pgnvjs.js"
    - "/js/chessboard-0.3.0.js"
custom-css-list:
    - "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css"
    - "/css/pgnvjs.css"
    - "/css/chessboard-0.3.0.min.css"
---
# Problem #

<div id="boardProblem" style="width: 400px"></div>
<div id="problemDescription">Brancas jogam. Qual o melhor lance?</div>
<input type="button" id="restartBtn" value="Restart" />

## Solution A ##

<div id="boardSolutionA"></div>

## Solution B ##

<div id="boardSolutionB"></div>

<script>
// Problem
//	pgnBoard('boardProblem', {position: problem, pieceStyle: 'wikipedia', theme: 'green', draggable: true, sparePieces: true})
	var problem = 'r3qrnk/pbp5/1p1pp2b/5pNQ/2PPPP2/2N1B3/PP6/2K3RR w KQkq - 0 1';
	var boardProblem = ChessBoard('boardProblem', {
		position: problem,
		draggable: true,
		sparePieces: true
	});
	$('#restartBtn').on('click', function () {
		boardProblem.position(problem);
	});

// Solution
	pgnView('boardSolutionA', { pgn: '1. e4 e5 2. Nf3 Nc6 3. Bb5', pieceStyle: 'wikipedia', theme: 'green' });
	pgnView('boardSolutionB', { pgn: '1. e4 e5 2. Nf3 Nc6 3. Bb5', pieceStyle: 'wikipedia', theme: 'green' });
</script>
