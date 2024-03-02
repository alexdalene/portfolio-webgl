<script>
	import Heading from '../Heading.svelte';
	import Boks from './Boks.svelte';

	const statistikk = [
		{ title: 'Kodespråk', value: '+10' },
		{ title: 'Nettsider', value: '+5' },
		{ title: 'Arbeidserfaring', value: '+7 år' }
	];
</script>

<section>
	<Heading title="Statistikk" />

	<div>
		{#each statistikk as stat}
			<Boks {...stat} />
		{/each}
	</div>
</section>

<style>
	div {
		display: flex;
		flex-direction: row;
		gap: var(--spacing-compact);
		max-width: calc(26rem + 4vw);
	}
</style>
