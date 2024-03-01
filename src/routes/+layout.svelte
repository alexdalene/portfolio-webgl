<slot />

<style>
	@import url('https://fonts.googleapis.com/css2?family=Gilda+Display&display=swap');
	@import url('https://fonts.googleapis.com/css2?family=Gilda+Display&family=Raleway:ital,wght@0,100..900;1,100..900&display=swap');

	:root {
		--color-background: #f1f2ee;
		--color-text: #161314;
		--color-neutral: #fdfdfc;

		--font-display: 'Gilda Display', serif;
		--font-body: 'Raleway', sans-serif;

		--spacing-loose: 7.5rem; /* 120px */
		--spacing-default: 2.5rem; /* 40px */
		--spacing-tight: 1.25rem; /* 20px */
		--spacing-compact: 0.625rem; /* 10px */
		--spacing-fit: 0.3125rem; /* 5px */

		--text-default: clamp(0.75rem, 2vw, 1rem);
		--text-large: clamp(1rem, 2vw, 1.25rem);
	}

	:global(body) {
		background-color: var(--color-background);
		color: var(--color-text);

		font-family: var(--font-body);
		font-weight: 500;
		font-size: var(--text-default);
		font-optical-sizing: auto;
		color-scheme: light;
	}

	:global(html) {
		text-rendering: optimizeLegibility;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}
</style>
