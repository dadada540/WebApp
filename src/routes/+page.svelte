<script lang="ts">
    import { Hamburger } from 'svelte-hamburgers';
    import Header from '$lib/header.svelte';

    let open;

    let todotitle = '';
    let Todos: { title: string; completed: boolean}[] =[]; 

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
        Todos = [...Todos, { title: todotitle, completed: false}];
        todotitle = '';
    }

    function del(index: number){
         Todos.splice(index,1)
         Todos = [...Todos];
    }

    function cheak(index: number){
        Todos[index].completed = !Todos[index].completed;
    }
</script>

<title>使える機能はTodoリストだけです。</title>

<main class="bg-linear-to-t bg-indigo-500 to-gray-300 h-screen">

    <Header/>

    <div class="p-10">
        <div class="rounded-2xl bg-gray-300 shadow-md p-6">
            <div class="flex justify-center">
                <div>
                    <label>
                        <input class="bg-gray-200 rounded-md transition hover:bg-gray-300" bind:value={todotitle} />
                    </label>
                    <button class="border p-1.5 bg-gray-200 rounded-md transition hover:bg-blue-300" on:click={add}>作成</button>
                </div>
            </div>
            {#if Todos.length === 0}
            <div class="flex justify-center font-bold">Todoがまだ1つもありません</div>
            {:else}
                 <ul class="px-50">
                      {#each Todos as todo, index}
                          <li class="p-3 font-bold text-xl bg-gray-200 rounded-md my-2 pl-7"><input type="checkbox" bind:checked={todo.completed} on:click={() => cheak(index)} class="mr-2" />
                            <button class="bg-gray-400 border rounded-md p-1.5 w-15a mr-4 text-white transition hover:bg-red-800" on:click={() =>  del(index)}>削除</button>
                            {todo.title}
                          </li>
                      {/each}
                  </ul>
            {/if}
        </div>
    </div>
</main>