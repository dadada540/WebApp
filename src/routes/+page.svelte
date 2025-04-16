<script lang="ts">
    import { Hamburger } from 'svelte-hamburgers';

    let open;

    let todotitle = '';
    let Todos: string[] =[]; 

    function add(){
        
        if(todotitle === ''){
            alert('タイトルを入力してください');
            return;
        }
        alert(todotitle +`を追加しました`);
        Todos = [...Todos, todotitle];
        todotitle = '';
    }

</script>

<main>
    <div class="p-4">
        <header class=" bg-gray-200 p-3 backdrop-blur-2xl rounded-2xl">
            <h1 class="text-3xl font-light text-gray-900">
                使える機能はTodoリストだけです。
            </h1>  
            <div class="fixed right-2 -mt-11">
                <Hamburger />
                
            </div>
        </header>
    </div>
    <div class="rounded-md border p-4">
        <div class="flex justify-center">
            <div>
                <label>
                    <input class="bg-gray-200 rounded-md transition hover:bg-gray-300" bind:value={todotitle} />
                </label>
                <button class="p-1.5 bg-gray-200 rounded-md transition hover:bg-gray-400" on:click={add}>作成</button>
            </div>
        </div>
        {#if Todos.length === 0}
        <div class="flex justify-center font-bold">Todoを作成してください</div>
        {:else}
             <ul class="px-50">
                  {#each Todos as todo}
                      <li class="p-3 font-bold text-xl bg-gray-200 rounded-md my-2 pl-7">{todo}</li>
                  {/each}
              </ul>
        {/if}
    </div>
    
    
</main>