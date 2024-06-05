<script>
	import Heading from '../Heading.svelte';
</script>

<section>
	<Heading title="Om meg" />
	<p>
		Jeg har en høyere fagskolegrad i frontend-utvikling fra Noroff, og har spesialisert meg i å lage
		interaktive og dynamiske webløsninger, med høyt fokus på brukeropplevelse.
	</p>
	<p>
		Jeg har samtidig som skolegangen jobbet som frontend-utvikler i et lite selskap i Oslo, og har
		fått mye erfaring med å jobbe i team og med kunder.
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
