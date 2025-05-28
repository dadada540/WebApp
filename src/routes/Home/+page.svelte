<script lang="ts">
    import { Hamburger } from 'svelte-hamburgers';
    import Header from '$lib/header.svelte';

    let selectedTodoIndex: number | null = null; // どのTodoが選ばれたか
    let selectedDate: string = ''; // 選択された日付
    let open;

    let todotitle = '';
    let Todos: { title: string; completed: boolean; due?: string }[] = [];

    let clendars = '';

    function calendars(){
        if (clendars === '') {
            alert('期限を選択してください');
            return;
        }

        console.log('選択された日付:', clendars);

        clendars = '';
    }

      // openDatePicker 関数を定義
    function openDatePicker(index: number) {
        selectedTodoIndex = index; // どのToDoが選ばれたかを記録
         selectedDate = Todos[index].due ?? ''; // 期限が既に設定されている場合、それを表示
    }

  // 日付を設定する関数
    function setDueDate() {
        if (selectedTodoIndex !== null && selectedDate !== '') {
        Todos[selectedTodoIndex].due = selectedDate;
         Todos = [...Todos]; // 変更後に再描画
        selectedTodoIndex = null; // リセット
        selectedDate = ''; // リセット
    }
    }


    function add(){
        
        if(todotitle === ''){
            alert('タイトルを入力してください');
            return;
        }


        Todos = [...Todos, {
        title: todotitle,
        completed: false,
        due: clendars
        }];

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

<svelte:head>
    <title>NaKon</title>
</svelte:head>



<main class="bg-linear-to-t h-screen">

    <Header/>

    <div class="p-10">
        <div class="rounded-2xl bg-gray-200 shadow-xl p-6">
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
                                <li class="p-3 font-bold text-xl border-1 border-solid rounded-md my-2 pl-7 flex felx-row  items-center shadow-md"><input type="checkbox" bind:checked={todo.completed} on:click={() => cheak(index)} class="mr-2" />
                                        <button class="bg-gray-500 border rounded-md p-1.5 w-15a mr-4 text-white transition hover:bg-red-800" on:click={() =>  del(index)}>削除</button>
                                        <button class="bg-gray-500 border rounded-md p-1.5 w-15a mr-4 text-white transition hover:bg-red-800" on:click={() => openDatePicker(index)}>期限を設定</button>
                                        {todo.title}

                                        {#if selectedTodoIndex === index}
                                            <input
                                                type="date"
                                                bind:value={selectedDate}
                                                class="ml-4 border px-2 py-1 rounded"
                                                on:change={setDueDate}
                                            />
                                        {/if}
                                        <div class="ml-auto">
                                            {#if todo.due}
                                                <p class="text-right font-normal text-2xl">{todo.due} まで</p>
                                            {/if}
                                        </div>
                                </li>
                    {/each}
                </ul>
            {/if}
        </div>
    </div>
</main>