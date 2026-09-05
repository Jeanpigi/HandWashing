<script>
	import Timer from './components/Timer.svelte';
	import HowTo from './components/HowTo.svelte';
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';

	let audio;
	function timerEnds() {
		audio?.play().catch(() => {
			// Autoplay can be blocked by the browser; not critical if it fails.
		});
	}
</script>

<main>
	<Header />
	<div class="flex-1 w-full max-w-2xl mx-auto px-4 py-8 sm:px-6 space-y-8">
		<Timer on:end={timerEnds} />
		<HowTo />
		<!-- svelte-ignore a11y-media-has-caption -->
		<audio bind:this={audio}>
			<source src="sound.wav" type="audio/wav" />
		</audio>
	</div>
	<Footer />
</main>
