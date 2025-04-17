<script lang="ts">
    import { Hamburger } from 'svelte-hamburgers';
    import Header from '$lib/header.svelte';

    let open;

    let todotitle = '';
    let Todos: string[] =[]; 

    function add(){
        
        if(todotitle === ''){
            alert('タイトルを入力してください');
            return;
        }
        else if(todotitle === `野獣先輩`){
            alert(`不適切なワードは追加できません`)
            return;
        }
        alert(todotitle +`を追加しました`);
        Todos = [...Todos, todotitle];
        todotitle = '';
    }

</script>
<main>
    <Header/>
    <div class="p-5">
        <div class="rounded-2xl border p-4">
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
                          <button class="bg-gray-200 ">削除</button>
                      {/each}
                  </ul>
            {/if}
        </div>
    </div>
</main>