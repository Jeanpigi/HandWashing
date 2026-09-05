<script>
    export let progress = 0;
</script>

<div
    class="h-3 w-full rounded-full bg-gray-100 overflow-hidden"
    role="progressbar"
    aria-valuemin="0"
    aria-valuemax="100"
    aria-valuenow={Math.round(progress)}
>
    <div
        class="h-full rounded-full bg-brand-500 transition-[width] duration-300 ease-linear"
        style="width:{progress}%"
    ></div>
</div>
