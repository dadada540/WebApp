<script>
    import { XMark } from 'svelte-heros-v2';
    import { Bars3BottomRight } from 'svelte-heros-v2';

    export let Open = false;
</script>

<button class="relative z-20" on:click={() => Open = !Open}>
    <Bars3BottomRight class="w-20 h-9 text-gray-800" />
</button>


<div class="overflow-x-hidden">
    <div class="fixed left-0 top-0 w-full bg-gray-200 z-30"  style="transform: translateX({Open ? '0' : '-120%'})">
        <div class="bg-gray-200 p-6 rounded-2xl absolute right-0 w-55 ">
            <button class="absolute top-2 right-4" on:click={() => Open = false}>
                <XMark class="w-8 h-8 text-gray-400" />
            </button>

            <div class="top-3">
                <ul class="text-left flex flex-col gap-10  divide-y divide-white">
                    <li><a class="text-3xl" href="#">ナム</a></li>
                    <li><a class="text-3xl" href="#">namu</a></li>
                    <li><a class="text-3xl" href="#">namu</a></li>
                    <li><a class="text-3xl" href="#">namu</a></li>
                </ul>
            </div>
        </div>
    </div>
</div>

<!--
<label class="cursor-pointer peer">
    <input type="checkbox" class="" />
    <Bars3BottomRight class="w-9 h-9 text-gray-800" />
</label>
-->