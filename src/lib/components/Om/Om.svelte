<script>
	import Heading from '../Heading.svelte';
</script>

<section>
	<Heading title="Om meg" />
	<p>
		Jeg er snart ferdig utdannet student i frontend-utvikling og har valgt å gi meg selv tittelen
		“Kreativ Utvikler” - for det er akkurat det jeg er.
	</p>
	<p>
		Jeg er alltid ivrig etter å utfordre meg selv med både nye prosjekter og teknologier, og
		ettersom det som oftest er noe nytt rundt hvert hjørne kommer den motivasjonen aldri dø ut.
	</p>
	<p>
		Har du meg på teamet så kommer du ikke angre, for jeg gir alt jeg har - og er litt små
		perfeksjonist - så det er kvalitet hele veien.
	</p>
</section>

<style>
	p {
		font-size: var(--text-large);
		max-width: calc(26rem + 4vw);
	}

	p:not(:last-child) {
		margin-bottom: var(--spacing-default);
	}
</style>
