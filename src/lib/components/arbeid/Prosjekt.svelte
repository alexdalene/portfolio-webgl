<script>
	import { onMount } from 'svelte';

	export let type;
	export let client;
	export let href;

	onMount(() => {
		// Select all articles
		const articles = document.querySelectorAll('.prosjekt');

		// Loop through all articles
		articles.forEach((article) => {
			// Add event listener for mouseover
			article.addEventListener('mouseover', () => {
				// On mouseover, add 'faded' class to all articles except the one being hovered
				articles.forEach((otherArticle) => {
					if (otherArticle !== article) {
						otherArticle.style.opacity = 0.5;
					}
				});
			});

			// Add event listener for mouseout
			article.addEventListener('mouseout', () => {
				// On mouseout, remove 'faded' class from all articles
				articles.forEach((otherArticle) => {
					otherArticle.style.opacity = 1;
				});
			});
		});
	});
</script>

<article class="prosjekt">
	<p>{type}</p>
	<h3>{client}</h3>

	<a {href} target="_blank">
		<span class="link">[ LIVE ]</span>
		<svg
			width="16"
			height="16"
			viewBox="0 0 16 16"
			fill="none"
			xmlns="http://www.w3.org/2000/svg"
			aria-hidden="true"
		>
			<mask
				id="mask0_1_514"
				style="mask-type:alpha"
				maskUnits="userSpaceOnUse"
				x="0"
				y="0"
				width="16"
				height="16"
			>
				<rect width="16" height="16" fill="#D9D9D9" />
			</mask>
			<g mask="url(#mask0_1_514)">
				<path
					d="M4.05001 12L3.20001 11.15L9.95001 4.4H4.00001V3.2H12V11.2H10.8V5.25L4.05001 12Z"
					fill="#1C1B1F"
				/>
			</g>
		</svg>
	</a>
</article>

<style>
	.prosjekt {
		position: relative;
		display: grid;
		grid-template-columns: repeat(12, 1fr);
		transition: opacity 200ms ease-in-out;

		width: 100%;
		padding-block: var(--spacing-tight);

		&:not(:first-child) {
			border-bottom: 1px solid var(--color-text);
		}

		&:is(:first-of-type) {
			border-top: 1px solid var(--color-text);
		}

		& p {
			grid-column: 1 / span 2;
		}

		& h3 {
			grid-column: 4 / span 4;
		}

		& a {
			grid-column: 12 / span 2;
			width: min-content;
			white-space: nowrap;
			display: flex;
			align-items: center;
			gap: var(--spacing-compact);
		}
	}
</style>
