<script>
	import Heading from '../Heading.svelte';

	const ferdigheter = [
		'HTML',
		'CSS',
		'JavaScript',
		'Svelte',
		'React',
		'Node.js',
		'Jest',
		'Cypress',
		'GSAP',
		'Git',
		'WebGL',
		'Three.js',
		'TailwindCSS',
		'SASS',
		'TypeScript',
		'Google Cloud',
		'Webflow',
		'WordPress',
		'Figma',
		'Illustrator',
		'Photoshop',
		'Premiere Pro',
		'After Effects'
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
		max-width: 25rem;
		gap: var(--spacing-fit);

		& li {
			border-radius: 0.25rem;
			background: rgba(22, 19, 20, 0.6);
			padding: 0.25rem 0.75rem;
			color: var(--color-background);
		}
	}
</style>
