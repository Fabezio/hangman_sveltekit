<script context="module" lang="ts">
	export const prerender = true;
</script>

<script>
	import Counter from '$lib/Counter.svelte';
	import HG0 from '$lib/shapes/HG0.svelte';
	import HG1 from '$lib/shapes/HG1.svelte';
	import HG2 from '$lib/shapes/HG2.svelte';
	import HG3 from '$lib/shapes/HG3.svelte';
	import HG4 from '$lib/shapes/HG4.svelte';
	import HG5 from '$lib/shapes/HG5.svelte';
	import HG6 from '$lib/shapes/HG6.svelte';
	import HG7 from '$lib/shapes/HG7.svelte';
	import HG8 from '$lib/shapes/HG8.svelte';
	import HG9 from '$lib/shapes/HG9.svelte';
	import About from './about.svelte';
	const title = 'Jeu du Pendu';
	let errors = 0;
	let lost = false;
	let won = false;
	let msg = '';
	let wordComplete = false;
	const words = [
		{mot: 'informaticien', indice: "employé derrière un écran"},
		{mot: "astronomie", indice: "domaine universel"},
		{mot: "chercheur", indice: "s'emploie à trouver"},
		{mot: "chien", indice: "fidèle ami"},
		{mot: "marmotte", indice: "creuse et roupille"},
		{mot: "electricien", indice: "il est au courant"},
		{mot: "ethique", indice: "base du savoir-vivre"},
		{mot: "dentelliere", indice: "fait dans la dentelle"},
		

	]
	const randomWord  = words[Math.floor(Math.random()*words.length)]

	const wordToFind = randomWord.mot;
	const {indice}  = randomWord
	let maskedWord = wordToFind.replace(/\w/g, '_').split('');
	
	let thisLetter = '';

	// for (let l of wordToFind) {
	// 	// l = "_"
	// 	maskedWord[l] = "_"

	// }
	// maskedWord= wordToFind.reduce("_")
	const vowels = 'aeiouy';
	const consonants = 'bcdfghjklmnpqrstvwxz';
	let untriedVowels = [...vowels];
	let untriedConsonants = [...consonants];
	let invalidLetters = [];
	let validLetters = [];
	let started = false;
	
	const options = [
		{},
		{ compo: HG1 },
		{ compo: HG2 },
		{ compo: HG3 },
		{ compo: HG4 },
		{ compo: HG5 },
		{ compo: HG6 },
		{ compo: HG7 },
		{ compo: HG8 },
		{ compo: HG9 },
		{ compo: HG0 }
	];
	let triesLeft = options.length -1;

	let selected;
	function selectLetter(e) {
		if (!started) started = true;
		// errors += 1;
		let foundLetter = false;
		const letter = e.target.innerHTML.trim();
		// console.log(letter.length);
		const wordLetters = wordToFind.split('');
		// console.log(wordLetters.includes(letter))

		wordLetters.map((l, i) => {
			if (letter === l) {
				foundLetter = true;
				maskedWord[i] = letter;
				console.log(maskedWord)
			}
		});
		// console.log(foundLetter);

		// console.log(rightLetter)
		// if(rightLetter) {
		// }
		if (!foundLetter) {
			errors += 1;
			triesLeft-=1
			invalidLetters = [...invalidLetters, letter];
		}
		
		// if(!rightLetter) errors++
		selected = options[errors];
		console.log(triesLeft)
		if (triesLeft == 0) lost = true;
		if(maskedWord.join("") === wordLetters.join("")) won = true;
		// console.log(e.target.innerHtml())
	}
	const letters = vowels.concat(consonants);
	let untriedLetters = [...letters];
	console.log(untriedLetters);
	$: if (lost) msg = 'Pendu 😠';
	$: if (won) msg = 'Sauvé 🙂';

	// console.log(untriedVowels);
	// console.log(consonants.length)
</script>

<svelte:head>
	<title>{title}</title>
</svelte:head>

<section>
	<h1>
		{title}
	</h1>

	<h2>
		<!-- try editing <strong>src/routes/index.svelte</strong> -->
	</h2>
	<article>
		<div class="letters">
			<div
				class="vowels uppercase"
				style="grid-template-columns: repeat({untriedVowels.length}, 1fr)"
			>
				{#each vowels as letter}
					<div on:click={selectLetter} class="letter">
						{letter}
					</div>
				{/each}
			</div>
			<div
				class="consonants uppercase"
				style="grid-template-columns: repeat({untriedConsonants.length}, 1fr)"
			>
				{#each consonants as letter}
					<div on:click={selectLetter} class="letter">
						{letter}
					</div>
				{/each}
			</div>
			
		</div>
		<div class="letters found">
			{#each validLetters as letter}
				
			{/each}
		</div>
		<div class="svg">
			{#if errors > 0}
				<svelte:component this={selected.compo} />
			{:else}
				<svg width="250" height="250" version="1.1" xmlns="http://www.w3.org/2000/svg" />
			{/if}
		</div>

		<!-- {wordToFind.length} lettres -->
		<!-- <h2 class="basic-margin">Mot à trouver</h2> -->
	</article>
	<h2 class="basic-margin uppercase">
		{maskedWord.join(' ')}
	</h2>
	<h3><q>{indice}</q></h3>

	{#if lost || won}
		<h1 class="basic-margin">
			{msg}
		</h1>
	{/if}
	<!-- {#if started}
	{/if} -->

	<!-- <Counter /> -->
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		/* justify-content: center; */
		align-items: center;
		flex: 1;
	}
	article {
		display: flex;
		flex-direction: row;
		justify-content: flex-start;
	}
	.letters {
		display: flex;
		flex-direction: column;
		flex-wrap: wrap;
		justify-content: flex-start;
		flex: 0 1 500px;
	}

	h1 {
		width: 100%;
	}
	h2 {
		font-size: 2em;
	}
	.uppercase {
		text-transform: uppercase;
	}
	.basic-margin {
		margin: 2em 0;
	}
	.vowels,
	.consonants {
		margin: 1em 0;
		display: flex;
		flex-wrap: wrap;
		/* flex: 1; */
		/* grid-gap: 1em; */
		cursor: pointer;
		max-width: 500px;
	}

	.letter {
		font-size: 1.5em;
		width: 1.5em;
		height: 2em;
		font-weight: 400;
		/* border: 1px solid #444;
		padding: 0 5px;
		border-radius: 7px; */
	}
	.letter:hover {
		text-decoration: underline;
	}

	.welcome {
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
