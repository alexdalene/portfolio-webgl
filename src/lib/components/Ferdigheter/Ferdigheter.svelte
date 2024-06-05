<script>
	import Heading from '../Heading.svelte';

	const ferdigheter = [
		'HTML',
		'CSS',
		'TailwindCSS',
		'SCSS',
		'JavaScript',
		'TypeScript',
		'Svelte',
		'React',
		'Jest',
		'Cypress',
		'Git',
		'Node.js',
		'WebGL',
		'Three.js',
		'GSAP',
		'GCP',
		'Webflow',
		'WordPress'
	];
</script>

<section id="ferdigheter">
	<Heading title="Ferdigheter" />

	<ul>
		{#each ferdigheter as ferdighet}
			<li>{ferdighet}</li>
		{/each}
	</ul>
</section>

<style>
	section {
		grid-column: 1 / span 3;

		@media (max-width: 768px) {
			grid-column: 1 / span 12;
		}
	}

	ul {
		display: flex;
		flex-wrap: wrap;
		max-width: 15rem;
		gap: var(--spacing-fit);

		& li {
			border-radius: 0.25rem;
			padding: 0.25rem 0.75rem;
			border: 1px solid var(--color-text);
		}
	}
</style>
