<script lang="ts">
    import { Hamburger } from 'svelte-hamburgers';
    import { Home } from 'svelte-heros-v2';
    import { Calendar } from 'svelte-heros-v2';
    import {  CheckCircle } from 'svelte-heros-v2';
    import { EllipsisHorizontalCircle } from 'svelte-heros-v2';

    let open;
</script>

<main>
    <div class="p-4">
        <header class=" bg-gray-200 p-3 backdrop-blur-2xl rounded-2xl">
            <div class="flex flex-row gap-50">
                <h1 class="text-3xl font-light text-gray-900"> 使える機能はTodoリストだけです。</h1>
                <nav>
                    <ul>
                        <li class="flex gap-20 pl-140">
                            <div>
                                <a href=""><Home /></a>
                            </div>
                            
                            <div>
                                <a href=""> <Calendar /></a>
                            </div>
                            <div>
                                <a href=""><CheckCircle /></a>
                            </div>
                            <div>
                                <a href=""><EllipsisHorizontalCircle /></a>
                            </div>
                        </li>
                    </ul>
                </nav>
            </div>
            <div class="fixed right-2 -mt-11">
                <Hamburger />
                
            </div>
        </header>
    </div>
</main>