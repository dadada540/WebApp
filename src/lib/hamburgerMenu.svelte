<script>
    import { XMark } from 'svelte-heros-v2';
    import { Bars3BottomRight } from 'svelte-heros-v2';
    import { fly } from 'svelte/transition';

    export let Open = false;
</script>

<button class="relative z-20" on:click={() => Open = !Open}>
    <Bars3BottomRight class="w-20 h-9 text-gray-800" />
</button>


{#if Open}
<div class="shadow-2xl">
    <div class="fixed left-0 top-0 w-full bg-gray-200 z-50 shadow-2xl"  transition:fly={{ x: 200, duration: 150 }}>
        <div id="box" class="bg-gray-200 p-6 rounded-2xl absolute right-0 w-55">
            <button class="absolute top-2 right-4" on:click={() => Open = false}>
                <XMark class="w-8 h-8" />
            </button>

            <div class="top-3 ">
                <ul class="text-left flex flex-col gap-10 mt-10  divide-y divide-white">
                    <li><a class="text-3xl mt-20" href="/home">Home</a></li>
                    <li><a class="text-3xl" href="/Calender">Calender</a></li>
                    <li><a class="text-3xl" href="/">ナムはすごいバカ</a></li>
                </ul>
            </div>
        </div>
    </div>
</div>
{/if}

<style>
    #box {
        box-shadow: -3px 5px 7px 2px rgba(0, 0, 0, 0.2);
    }


</style>