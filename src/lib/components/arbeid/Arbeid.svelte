<script>
	import Heading from '../Heading.svelte';
	import Prosjekt from './Prosjekt.svelte';

	const prosjekter = [
		{
			type: 'Organisasjon',
			client: 'Sound of Happiness',
			href: 'https://www.kunde1.no'
		},
		{
			type: 'Bedrift',
			client: 'Omsorgskollektivet',
			href: 'https://www.kunde2.no'
		},
		{
			type: 'Restaurant',
			client: 'Le Monde Tapas',
			href: 'https://www.kunde3.no'
		},
		{
			type: 'Tatovering',
			client: 'Blekksprut Tattoo',
			href: 'https://www.kunde3.no'
		}
	];
</script>

<section id="arbeid">
	<Heading title="Fremhevet arbeid" />

	{#each prosjekter as prosjekt}
		<Prosjekt {...prosjekt} />
	{/each}
</section>
