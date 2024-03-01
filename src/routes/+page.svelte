<script>
	import Arbeid from '$lib/components/Arbeid/Arbeid.svelte';
	import Ferdigheter from '$lib/components/Ferdigheter/Ferdigheter.svelte';
</script>

<p>
	Mitt navn er Alex Dalene og jeg er en <span role="heading" aria-level="1">kreativ utvikler</span> spesialisert
	i brukeropplevelse og design.
</p>

<Arbeid />

<Ferdigheter />

<style>
	p {
		max-width: calc(16rem + 4vw);
	}
</style>
