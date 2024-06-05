<script>
	import { fade } from 'svelte/transition';
	import { cubicOut, cubicIn } from 'svelte/easing';
	import { onMount } from 'svelte';

	import gsap from 'gsap';
	import TextPlugin from 'gsap/dist/TextPlugin';

	import { Code, CircleArrowOutUpRight } from 'lucide-svelte';

	export let type;
	export let client;
	export let href;
	export let texture;
	export let changeTexture;

	let isHovered = false;
	let tl;

	onMount(() => {
		gsap.registerPlugin(TextPlugin);

		tl = gsap.timeline();

		return () => {
			tl.kill();
		};
	});

	function handleMouseEnter() {
		tl.play();
	}

	function handleMouseLeave() {
		tl.reverse();
	}
</script>

<article
	class="project"
	on:mouseenter={() => {
		isHovered = true;
		changeTexture(texture);
	}}
	on:mouseleave={() => (isHovered = false)}
>
	<p><Code size={16} />{type}</p>
	<h3>{client}</h3>

	<a {href} target="_blank" class:not-active={!href}>
		<span>Besøk</span>
		<CircleArrowOutUpRight size={16} />
	</a>

	{#if isHovered}
		<article
			class="project-overlay"
			on:mouseleave={() => (isHovered = false)}
			in:fade={{ duration: 200, easing: cubicOut }}
			out:fade={{ duration: 200, easing: cubicIn }}
		>
			<p><Code size={16} /> {type}</p>
			<h3>{client}</h3>

			{#if href}
				<a {href} target="_blank">
					<span
						on:mouseenter={handleMouseEnter}
						on:mouseleave={handleMouseLeave}
						role="link"
						tabindex="0">Besøk</span
					>
					<CircleArrowOutUpRight size={16} />
				</a>
			{/if}
		</article>
	{/if}
</article>

<style>
	.project {
		display: grid;
		grid-template-columns: repeat(12, 1fr);
		position: relative;

		width: 100%;
		padding-block: var(--spacing-tight);

		border-top: 1px solid var(--color-text);

		& p {
			grid-column: 1 / span 2;
			display: flex;
			align-items: center;
			gap: var(--spacing-compact);
		}

		& h3 {
			grid-column: 4 / span 4;

			@media (max-width: 768px) {
				grid-column: 5 / span 4;
			}
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

	.not-active {
		pointer-events: none;
		opacity: 0;
	}

	.project-overlay {
		display: grid;
		grid-template-columns: repeat(12, 1fr);
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		transition: opacity 300ms ease;
		padding-block: var(--spacing-tight);
		z-index: 1;
		border-block: 1px solid var(--color-background);
		color: var(--color-background);

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
