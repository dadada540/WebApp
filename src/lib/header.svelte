<script lang="ts">
    import { Home } from 'svelte-heros-v2';
    import { Calendar } from 'svelte-heros-v2';
    import {  CheckCircle } from 'svelte-heros-v2';
    import { Bars3BottomRight } from 'svelte-heros-v2';
    import { XMark } from 'svelte-heros-v2';
    import Hamburger from '$lib/hamburgerMenu.svelte';

    let Open = false;
    
</script>

<main>
    <div class="p-4">
        <header class=" bg-gray-200 p-3 rounded-2xl backdrop-blur-sm shadow-lg">
            <div class="flex justify-between items-center">
                <div class="text-3xl text-gray-900"></div>
                <nav>
                    <ul class="">
                        <li class="flex justify-end-safe gap-20 w-full">
                            <div class="transition hover:bg-gray-300 rounded-full p-2">
                                <a href="Home"><Home size="35"  /></a>
                            </div>
                            <div class="transition hover:bg-gray-300 rounded-full p-2">
                                <a href="Calender"> <Calendar size="35" /></a>
                            </div>
                            <div class="transition hover:bg-gray-300 rounded-full p-2">
                                <a href=""><CheckCircle size="35" /></a>
                            </div>
                            <div class="">
                                <Hamburger />
                            </div>
                        </li>
                    </ul>
                </nav>
            </div>
        </header>
    </div>
</main>