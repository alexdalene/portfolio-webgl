<script>
	export let title;
	export let value;
</script>

<article>
	<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none">
		<path d="M0 19L8.74228e-07 24C1.74846e-07 20 3.33333 19 5 19L0 19Z" fill="#F1F2EE" />
		<path d="M19 0V5C19 1 22.3333 0 24 0L19 0Z" fill="#F1F2EE" />
		<path d="M0 0H19V9.5C19 14.7467 14.7467 19 9.5 19H0V0Z" fill="#F1F2EE" />
	</svg>
	<h3>{title}</h3>
	<p>{value}</p>
</article>

<style>
	article {
		background-color: var(--color-neutral);
		border-radius: 0.25rem;
		padding-block: var(--spacing-loose);
		text-align: center;
		width: 100%;

		position: relative;

		@media (max-width: 768px) {
			padding-block: var(--spacing-tight);
		}
	}

	h3 {
		font-size: 0.75rem;
		text-transform: uppercase;
	}

	p {
		font-size: var(--text-huge);
	}

	svg {
		position: absolute;
		top: 0;
		left: 0;
		width: 1.5rem;
		height: 1.5rem;
	}
</style>
