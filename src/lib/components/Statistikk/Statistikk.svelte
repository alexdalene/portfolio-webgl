<script>
	import Heading from '../Heading.svelte';
	import Boks from './Boks.svelte';

	const statistikk = [
		{ title: 'Kodespråk', value: '+10' },
		{ title: 'Klienter', value: '+4' },
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
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: var(--spacing-compact);
		max-width: calc(26rem + 4vw);

		@media (max-width: 768px) {
			grid-template-columns: 1fr;
		}
	}
</style>
