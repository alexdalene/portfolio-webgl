<script>
	import Heading from '../Heading.svelte';

	import { ArrowUpRightFromCircle } from 'lucide-svelte';

	const kontakt = [
		{ title: 'Mail', href: 'mailto:alexdalene@outlook.com' },
		{ title: 'Twitter', href: 'https://twitter.com/xenelad' },
		{ title: 'LinkedIn', href: 'https://www.linkedin.com/in/alex-dalene/' },
		{ title: 'GitHub', href: 'https://github.com/alexdalene' }
	];
</script>

<section id="kontakt">
	<Heading title="Ta kontakt" />

	<p>Ta gjerne kontakt om du har spørsmål, ønsker å samarbeide eller bare vil slå av en prat.</p>

	<ul>
		{#each kontakt as { title, href }}
			<li>
				<a {href}>
					<ArrowUpRightFromCircle size={16} />
					<span class="link">{title}</span>
				</a>
			</li>
		{/each}
	</ul>
</section>

<style>
	p {
		max-width: calc(26rem + 4vw);
		font-size: var(--text-large);
		margin-bottom: var(--spacing-default);
	}

	ul {
		display: flex;
		flex-direction: column;
		gap: var(--spacing-compact);
	}

	a {
		display: flex;
		align-items: center;
		gap: var(--spacing-compact);
		width: fit-content;
	}
</style>
