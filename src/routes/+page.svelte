<script>
	import Arbeid from '$lib/components/Arbeid/Arbeid.svelte';
	import Ferdigheter from '$lib/components/Ferdigheter/Ferdigheter.svelte';
	import Om from '$lib/components/Om/Om.svelte';
	import Kontakt from '$lib/components/Kontakt/Kontakt.svelte';
</script>

<svelte:head>
	<title>Alex Dalene - Frontend Utvikler</title>
	<meta
		name="description"
		content="Alex Dalene er en frontend utvikler med stort engasjement for brukeropplevelse og innovative løsninger."
	/>
	<meta
		name="keywords"
		content="Alex Dalene, portfolio, web development, web design, user experience, portefølje, ux, frontend"
	/>
	<meta name="author" content="Alex Dalene" />
</svelte:head>

<p>
	Mitt navn er Alex Dalene og jeg er en <span role="heading" aria-level="1">frontend utvikler</span>
	spesialisert i å lage interaktive og dynamiske webløsninger.
</p>

<Arbeid />

<div id="grid">
	<Ferdigheter />

	<div>
		<Om />

		<Kontakt />
	</div>
</div>

<style>
	p {
		max-width: calc(16rem + 4vw);
	}

	#grid {
		display: grid;
		grid-template-columns: repeat(12, 1fr);
		width: 100%;

		& div {
			grid-column: 6 / span 5;
		}

		@media (max-width: 768px) {
			grid-template-columns: 1fr;

			& div {
				grid-column: 1 / span 12;
			}
		}
	}
</style>
