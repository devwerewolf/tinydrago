<script>
	let placeholder = "Paste any URL here!";
	let URL = "";
	let output = "";
	let successfulCopy = false;
	
	function makeURLComplex() {
		let wordyURL = 
			URL.replaceAll(":", " colon ")
			.replaceAll("/", rollSlash)
			.replaceAll(".", rollDot);
			
		let words = wordyURL.split(" ");
		
		for (let i = 0; i < 100; i++) {
			const index1 = randomNumber(0, words.length);
			const index2 = randomNumber(0, words.length);
			const word1 = words[index1];
			const word2 = words[index2];
			
			words[index1] = word2;
			words[index2] = word1;
		}
		
		output = 
			words.join(" ")
			.split("  ")
			.join(" ");
		
		successfulCopy = false;
	}
	
	async function copyToClipboard() {
		await navigator.clipboard.writeText(output.trim());
		successfulCopy = true;
	}
	
	function rollSlash() {
		const slashList = ["slash", "back slash", "foward slash"];
		const slashReplacement = randomItem(slashList);
		return " " + slashReplacement + " ";
	}
	
	function rollDot() {
		const dotList = ["dot", "stop", "full stop"];
		const dotReplacement = randomItem(dotList);
		return " " + dotReplacement + " ";
	}
	
	function randomItem(list = []) {
		const index = randomNumber(0, list.length);
		return list[index];
	}
	
	function randomNumber(min, max) {
		return Math.floor(Math.random() * max) + min;
	}
</script>

<header>
	<h1>Tiny Dragon's "URL Complex-A-Tron 3000"</h1>
	<h2>Made with 🧡 by WerewolfDev</h2>
</header>

<main>
	<section id="prompt">
		<textarea rows="4" maxlength="2048" {placeholder} bind:value={URL}></textarea>
		<button on:click={makeURLComplex}>Complexify!</button>
	</section>
	
	{#if output}
	<section id="result">
		<div id="output">{output}</div>
		<button on:click={copyToClipboard}>{successfulCopy ? "Copied! 👍" : "Copy?"}</button>
	</section>
	{/if}
	
</main>

<footer>
	<img height="256px" width="256px" src="images/Cry.png" alt="Tiny Cry">
</footer>

	
<style lang="scss">
	header {
		// background-color: #000000dd;
		padding: 1rem;
		text-align: center;
		
		h1 {
			font-size: 2rem;
		}
		
		h2 {
			font-size: 1.25rem;
			font-weight: normal;
		}
	}
	
	
	main {		
		#prompt {
			display: flex;
			flex-direction: column;
			
			padding: 1rem;
			text-align: center;
			
			textarea {
				color: black;
				font-family: 'Roboto Mono', monospace;
				font-size: 1.5rem;
				outline: none;
			}
			
			button {
				background-color: #fa885b;
			}
		}
		
		#result {
			font-size: 1.5rem;
			font-weight: bold;
			padding: 1rem;
			
			display: flex;
			flex-direction: column;
			
			#output {
				font-family: 'Roboto Mono', monospace;
				text-shadow: 2px 2px black;
			}
			
			button {
				background-color: #ab513a;
			}
		}
		
		button {
			font-family: 'Roboto Mono', monospace;
			font-size: 1.75rem;
			margin-top: 1rem;
			padding: 0.25rem;
			border: none;
			outline-color: #fbb55c;
			
			box-shadow: 5px 5px black;
		}
		
		z-index: 10;
	}
	
	footer {
		position: fixed;
		bottom: -5px;
		right: 0;
		z-index: -1;
	}
</style>