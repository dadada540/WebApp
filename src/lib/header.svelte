<script lang="ts">
    import { Home } from 'svelte-heros-v2';
    import { Calendar } from 'svelte-heros-v2';
    import {  CheckCircle } from 'svelte-heros-v2';
    import { Bars3BottomRight } from 'svelte-heros-v2';
    import { XMark } from 'svelte-heros-v2';
    import Hamburger from '$lib/hamburgerMenu.svelte';

    let open;
</script>

<main>
    <div class="p-4">
        <header class=" bg-gray-200 p-3 rounded-2xl backdrop-blur-sm shadow-lg">
            <div class="flex justify-between items-center">
                <div class="text-3xl text-gray-900"></div>
                <nav>
                    <ul class="">
                        <li class="flex justify-end-safe gap-20 w-full">
                            <div>
                                <a href="Home"><Home size="35"  /></a>
                            </div>
                            <div>
                                <a href="Calender"> <Calendar size="35" /></a>
                            </div>
                            <div>
                                <a href=""><CheckCircle size="35" /></a>
                            </div>
                            <label class="cursor-pointer peer">
                                <input type="checkbox" class="hidden" />
                                <Bars3BottomRight class="w-9 h-9 text-gray-800" />
                            </label>
                            <div class="bg-gray-200 backdrop-blur-none relative h-200 w-60 left-520 rounded-l-3xl hidden transition-all not-peer-has-checked:opacity-0 peer-has-checked:block">
                                <button class="flex justify-end ">
                                    <a href=""><XMark size="35" /></a>
                                </button>
                            
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
                        </li>
                    </ul>
                </nav>
            </div>
        </header>
    </div>

    <Hamburger />
</main>