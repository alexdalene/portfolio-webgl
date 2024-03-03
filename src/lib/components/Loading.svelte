<script>
	import { onMount } from 'svelte';

	let counter = 0;
	let text = 'Please wait...';

	// Update the text based on the value of the counter
	$: {
		if (counter < 2) {
			text = 'Laster inn nødvendige ressurser...';
		} else if (counter < 4) {
			text = 'Tror det er snart...';
		} else if (counter < 5) {
			text = 'Tar litt tid...';
		}
	}

	onMount(() => {
		// Increment the counter every second
		setInterval(() => {
			counter++;
		}, 1000);

		return () => {
			clearInterval();
		};
	});
</script>

<div class="loading">
	<div class="loading__spinner"></div>
	{text}
</div>

<style>
	.loading {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: var(--color-background);
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 1000;

		display: flex;
		flex-direction: column;
		gap: var(--spacing-tight);
	}

	.loading__spinner {
		border: 4px solid var(--color-text);
		border-top: 4px solid var(--color-background);
		border-radius: 50%;
		width: 40px;
		height: 40px;
		animation: spin 600ms ease-in-out infinite;
	}

	@keyframes spin {
		0% {
			transform: rotate(0deg);
		}
		100% {
			transform: rotate(360deg);
		}
	}
</style>
