<script>
	import Arbeid from '$lib/components/Arbeid/Arbeid.svelte';
	import Ferdigheter from '$lib/components/Ferdigheter/Ferdigheter.svelte';
	import Statistikk from '$lib/components/Statistikk/Statistikk.svelte';
	import Om from '$lib/components/Om/Om.svelte';
	import Kontakt from '$lib/components/Kontakt/Kontakt.svelte';
</script>

<p>
	Mitt navn er Alex Dalene og jeg er en <span role="heading" aria-level="1">kreativ utvikler</span> spesialisert
	i brukeropplevelse og design.
</p>

<Arbeid />

<div id="grid">
	<Ferdigheter />

	<div>
		<Statistikk />

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
	}
</style>
