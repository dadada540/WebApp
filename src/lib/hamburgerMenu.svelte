<script>
    import { XMark } from 'svelte-heros-v2';
    import { Bars3BottomRight } from 'svelte-heros-v2';

    export let Open = false;
</script>

<button class="relative z-20" on:click={() => Open = !Open}>
    <Bars3BottomRight class="w-9 h-9 text-gray-800" />
</button>


<div class="fixed right-0 w-full bg-gray-200 transition-transform duration-300"  style="transform: translateX({Open ? '0' : '100%'})">
    <div class="bg-gray-500 p-6 rounded-2xl absolute right-0 w-55 ">
        <div class="top-3">
            <ul class="text-left flex flex-col gap-6  divide-y divide-white">
                <li><a class="text-3xl" href="#">namu</a></li>
                <li><a class="text-3xl" href="#">namu</a></li>
                <li><a class="text-3xl" href="#">namu</a></li>
                <li><a class="text-3xl" href="#">namu</a></li>
            </ul>
        </div>
    </div>
</div>

<!--
<label class="cursor-pointer peer">
    <input type="checkbox" class="" />
    <Bars3BottomRight class="w-9 h-9 text-gray-800" />
</label>
-->