<script>
	import Heading from '../Heading.svelte';

	const kontakt = [
		{ title: '[ MAIL ]', href: 'mailto:alexdalene@outlook.com' },
		{ title: '[ TWITTER ]', href: 'https://twitter.com/xenelad' },
		{ title: '[ LINKEDIN ]', href: 'https://www.linkedin.com/in/alex-dalene/' },
		{ title: '[ GITHUB ]', href: 'https://github.com/alexdalene' }
	];
</script>

<section id="kontakt">
	<Heading title="Ta kontakt" />

	<p>Ta gjerne kontakt om du har spørsmål, ønsker å samarbeide eller bare vil slå av en prat.</p>

	<ul>
		{#each kontakt as { title, href }}
			<li>
				<a {href}>
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

	a {
		display: flex;
		align-items: center;
		gap: var(--spacing-compact);
		width: fit-content;
	}
</style>
