<script>
	import Timer from './components/Timer.svelte';
	import HowTo from './components/HowTo.svelte';
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';

	let audio;
	function timerEnds(e) {
		audio.play();
	}
</script>

<main>
	<Header></Header>
	<div class="container mx-auto px-4 py-2">
		<Timer on:end={timerEnds}></Timer>
		<HowTo></HowTo>
		<audio bind:this={audio} >
			<source src="sound.wav" />
		</audio>
	</div>
	<Footer></Footer>
</main>


<style>

</style>