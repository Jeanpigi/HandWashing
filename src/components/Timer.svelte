<script>
    import { createEventDispatcher } from 'svelte';
    import ProgressBar from './ProgressBar.svelte';

    const totalSeconds = 20;
    let secondsLeft =  totalSeconds;
    let isRunning = false;
    let isActive = true;
    $: progress = ((totalSeconds - secondsLeft) / totalSeconds) * 100;
    const dispatch = createEventDispatcher();

    function startTimer() {
        isRunning = true;
        isActive = false;
        const timer = setInterval(() => {
            secondsLeft -= 1;
            if (secondsLeft == 0) {
                clearInterval(timer);
                isRunning =  false;
                secondsLeft = totalSeconds;
                dispatch('end', 'end timer');
                isActive = true;
            }
        }, 1000);
    }
</script>

<div class="py-2">
    <h2 class="text-base antialiased py-2 lg:text-xl md:text-lg">Seconds Left: {secondsLeft}</h2>
    <ProgressBar progress={progress}></ProgressBar>
    <div class="flex justify-center pt-10">
        {#if isActive}
            <button class="bg-indigo-600 hover:bg-indigo-500 py-2 px-10 text-center text-white" disabled={isRunning} on:click={startTimer}>Start</button>
        {:else}
            <button class="bg-indigo-600 py-2 px-10 text-center text-white opacity-50 cursor-not-allowed">Start</button>
        {/if}
    </div>
</div>


<style>

</style>