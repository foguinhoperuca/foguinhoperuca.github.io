{% assign challenge = site.data.challenges[page.challenge] %}
# Problem #

<div id="boardProblem" style="width: 320px"></div>
<small>_**{{ challenge.descripton }}**_</small>

## Solution ##

<input type="button" id="showSolutionBtn" value="Show/Hide" />
<div id="boardSolution"></div>

<script>
	var boardProblem = pgnEdit('boardProblem', {
		position: '{{ challenge.fen }}',
		pieceStyle: 'wikipedia',
		theme: 'blue'
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
