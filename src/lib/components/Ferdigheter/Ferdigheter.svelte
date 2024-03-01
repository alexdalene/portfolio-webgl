<script>
	import Heading from '../Heading.svelte';

	const ferdigheter = [
		'HTML',
		'CSS',
		'JavaScript',
		'Svelte',
		'React',
		'Node.js',
		'Express',
		'MongoDB',
		'GSAP',
		'WebGL',
		'Three.js',
		'Tailwind',
		'TypeScript',
		'Firebase',
		'GCP',
		'Webflow',
		'WordPress',
		'Figma',
		'Illustrator',
		'Photoshop',
		'Premiere Pro',
		'After Effects'
	];
</script>

<section>
	<Heading title="Ferdigheter" />

	<ul>
		{#each ferdigheter as ferdighet}
			<li>{ferdighet}</li>
		{/each}
	</ul>
</section>

<style>
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
