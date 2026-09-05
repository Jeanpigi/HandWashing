<script>
    import { onDestroy, createEventDispatcher } from 'svelte';
    import ProgressBar from './ProgressBar.svelte';

    const totalSeconds = 20;
    let secondsLeft = totalSeconds;
    let isRunning = false;
    $: progress = ((totalSeconds - secondsLeft) / totalSeconds) * 100;
    const dispatch = createEventDispatcher();

    let intervalId;

    function startTimer() {
        if (isRunning) return;
        isRunning = true;
        intervalId = setInterval(() => {
            secondsLeft -= 1;
            if (secondsLeft === 0) {
                clearInterval(intervalId);
                isRunning = false;
                secondsLeft = totalSeconds;
                dispatch('end', 'end timer');
            }
        }, 1000);
    }

    onDestroy(() => {
        if (intervalId) clearInterval(intervalId);
    });
</script>

<div class="bg-white rounded-2xl shadow-sm p-6 sm:p-8 text-center">
    <p class="text-sm font-medium text-gray-500 uppercase tracking-wide">Time remaining</p>
    <p class="mt-1 font-display text-5xl sm:text-6xl font-bold text-brand-700 tabular-nums" aria-live="polite">
        {secondsLeft}s
    </p>

    <div class="mt-6">
        <ProgressBar progress={progress} />
    </div>

    <div class="flex justify-center mt-8">
        <button
            class="w-full sm:w-auto rounded-full bg-brand-600 hover:bg-brand-500 active:bg-brand-700 disabled:bg-gray-300 disabled:cursor-not-allowed transition-colors py-3 px-10 text-center font-semibold text-white shadow-sm"
            disabled={isRunning}
            on:click={startTimer}
        >
            {isRunning ? 'Washing…' : 'Start'}
        </button>
    </div>
</div>
