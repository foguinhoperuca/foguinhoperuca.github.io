{% assign challenge = site.data.challenges[page.challenge] %}
# Problem #

<div id="boardProblem"></div>
<div id="problemDescription">{{ challenge.descripton }}</div>
<input type="button" id="restartBtn" value="Restart" />

## Solution ##

<input type="button" id="showSolutionBtn" value="Show/Hide" />
<div id="boardSolution"></div>

<script>
	var boardProblem = ChessBoard('boardProblem', {
		position: '{{ challenge.fen }}',
		draggable: true,
		sparePieces: true
	});
	$('#restartBtn').on('click', function () {
		boardProblem.position('{{ challenge.fen }}');
		solution();
		$("#boardSolution").hide();
	});

	function solution() {
		pgnView('boardSolution', {
			position: '{{ challenge.fen }}',
			pgn: '{{ challenge.pgn }}',
			pieceStyle: 'wikipedia',
			theme: 'informator'
		});
	}

	$("#showSolutionBtn").click(function(){
		solution();
		$("#boardSolution").toggle();
	});

	$(document).ready(function(){
		solution();
		$("#boardSolution").hide();
	});
</script>
