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

	let background;
</script>

<section
	id="arbeid"
	on:mouseover={() => ((background.style.opacity = 1), (background.style.zIndex = 1))}
	on:mouseout={() => ((background.style.opacity = 0), (background.style.zIndex = -1))}
	on:focus={() => ((background.style.opacity = 1), (background.style.zIndex = 1))}
	on:blur={() => ((background.style.opacity = 0), (background.style.zIndex = -1))}
	role="complementary"
>
	<Heading title="Fremhevet arbeid" />

	{#each prosjekter as prosjekt}
		<Prosjekt {...prosjekt} />
	{/each}
</section>

<div bind:this={background} id="background"></div>

<style>
	#background {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: -1;
		opacity: 0;
		background-color: #7d7f7bac;
		transition: opacity 200ms ease-in-out;
	}
</style>
