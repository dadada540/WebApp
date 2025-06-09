<script>
    import { XMark } from 'svelte-heros-v2';
    import { Bars3BottomRight } from 'svelte-heros-v2';

    let isOpen = false;
</script>

<button class="absolute top-0 right-3" on:click={() => isOpen = true}>
    <Bars3BottomRight class="w-9 h-9 text-gray-800" />
</button>

<div class="bg-gray-200  h-200 w-60 rounded-l-3xl transition-all  peer-has-checked:block fixed -right-60 top-0 ">
    <div class="relative">
        <div class="absolute top-40  w-55 ">
            <ul class="text-left ml-4 top-20 flex flex-col gap-6 divide-y divide-white">
                <li class="top-20 ">
                    <a class="text-3xl" href="">namu</a>
                </li>
                <li>
                    <a class="text-3xl" href="">namu</a>
                </li>
                <li>
                    <a class="text-3xl" href="">namu</a>
                </li>
                <li>
                    <a class="text-3xl" href="">namu</a>
                </li>
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