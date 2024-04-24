<script>
	import Heading from '../Heading.svelte';
</script>

<section>
	<Heading title="Om meg" />
	<p>
		Jeg studerer foreløpig på Noroff i Kristiansand, og har snart en høyere fagskolegrad i
		Frontend-utvikling.
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
