<script>
	export let title = 'Heading';
</script>

<h2>
	{title}
	<svg
		width="16"
		height="16"
		viewBox="0 0 16 16"
		fill="none"
		xmlns="http://www.w3.org/2000/svg"
		aria-hidden="true"
	>
		<path
			d="M3.19998 4L10.6 4L10.6 10.9L12.75 8.75L13.6 9.6L9.99998 13.2L6.39998 9.6L7.24998 8.75L9.39998 10.9L9.39998 5.2L3.19998 5.2L3.19998 4Z"
			fill="currentColor"
		/>
	</svg>
</h2>

<style>
	h2 {
		margin-bottom: var(--spacing-tight);
		opacity: 0.6;

		& svg {
			display: inline-block;
			margin-left: var(--spacing-compact);
		}
	}
</style>
