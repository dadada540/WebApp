<script>
    import { XMark } from 'svelte-heros-v2';
    import { Bars3BottomRight } from 'svelte-heros-v2';

    export let Open = false;
</script>

<button class="relative z-20" on:click={() => Open = !Open}>
    <Bars3BottomRight class="w-9 h-9 text-gray-800" />
</button>


    <div class="fixed top-0 right-0 h-full w-full bg-gray-200 rounded-l-3xl transition-transform duration-300"  style="transform: translateX({Open ? '0' : '100%'})">
        <div class="bg-gray-200 h-full p-6 absolute top-40 right-0 w-55 ">
            <ul class="text-left flex flex-col gap-6 divide-y divide-white">
                <li><a class="text-3xl" href="#">namu</a></li>
                <li><a class="text-3xl" href="#">namu</a></li>
                <li><a class="text-3xl" href="#">namu</a></li>
                <li><a class="text-3xl" href="#">namu</a></li>
            </ul>
        </div>
    </div>

<!--
<label class="cursor-pointer peer">
    <input type="checkbox" class="" />
    <Bars3BottomRight class="w-9 h-9 text-gray-800" />
</label>
-->