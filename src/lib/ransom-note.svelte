<script lang="ts">
	let text: string;
	import { onMount } from 'svelte';
	let characterArray: string[];

	onMount(async () => {
		Parse();
	});

	let fonts: string[] = ['font-exclusive-serif', 'font-newyork', 'font-vogue', 'font-typewriter'];

	function Parse(): void {
		characterArray = text.split('');
	}

	function GetRandomFont(): string {
		return 'font-family:' + fonts[Math.floor(Math.random() * fonts.length)] + ';';
	}

	function GetRandomSize(): string {
		return 'font-size:' + (Math.floor(Math.random() * 30) + 40) + 'px;';
	}

	function GetRandomColor(): string {
		let hue = Math.random() * 360;
		return `background-color:hsla(${hue},100%,80%,1.0);`;
	}

	function GetTransform(): string {
		let range = 10;
		let deg = Math.floor(Math.random() * range) - range / 2;
		return 'transform:rotate(' + deg + 'deg);';
	}

	function GetStyle(): string {
		let style: string = '';
		style += GetRandomFont();
		style += GetTransform();
		style += GetRandomSize();
		style += GetRandomColor();
		return style;
	}
</script>

<span style="display:none" contenteditable="true" bind:innerHTML={text}><slot /></span>

{#if characterArray}
	<p>
		{#each characterArray as character}
			{#if character == ' '}
				<span class="space" />
			{:else}
				<span class="letter" style={GetStyle()}>{character}</span>
			{/if}
		{/each}
	</p>
{/if}

<style>
	.space {
		width: 1rem;
	}

	.letter,
	.space {
		display: inline-block;
		margin: 0.1rem;
	}

	@font-face {
		font-family: font-exclusive-serif;
		src: url(font-exclusive-serif.ttf);
	}

	@font-face {
		font-family: font-newyork;
		src: url(font-newyork.otf);
	}

	@font-face {
		font-family: font-vogue;
		src: url(font-vogue.ttf);
	}

	@font-face {
		font-family: font-typewriter;
		src: url(font-typewriter.ttf);
	}
</style>
