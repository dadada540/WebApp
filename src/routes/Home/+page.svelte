
<script lang="ts">
    import Header from '$lib/header.svelte';
    import { onMount } from 'svelte'; 
    import Cookies from 'js-cookie';

    let selectedTodoIndex: number | null = null; // どのTodoが選ばれたか
    let selectedDate: string = ''; // 選択された日付
    let open;
    let todotitle = '';
    let Todos: { title: string; completed: boolean; due?: string }[] = [];
    let clendars = '';
    let isInitialized: boolean = false;

    onMount(() => {
    if (typeof window !== 'undefined') {
        try {
        const savedTodos = localStorage.getItem('todos');
        if (savedTodos) {
            Todos = JSON.parse(savedTodos);
        }
        } catch (e) {
        console.error('Failed to load todos from localStorage:', e);
        } finally {
            isInitialized = true;
        }
        }
    });


    const savedDate = Cookies.get('deadline');
    if (savedDate) {
        selectedDate = savedDate;
    }

  // Todos が変化したら保存
    $: Cookies.set('todoList', JSON.stringify(Todos), { expires: 7 });

  // selectedDate も保存（期限用）
    $: if (clendars) {
        Cookies.set('deadline', clendars, { expires: 7 });
    }

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
    try {
        localStorage.setItem('todos', JSON.stringify(Todos));
    } catch (e) {
        console.error('ローカルストレージへの保存に失敗しました', e);
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

        try {
        localStorage.setItem('todos', JSON.stringify(Todos));
    } catch (e) {
        console.error('ローカルストレージへの保存に失敗しました', e);
        }
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



<main class="bg-linear-to-t from-gray-400 to-gray-300 h-screen">

    <Header/>

    <div class="p-10">
        <div class="rounded-2xl bg-gray-200 shadow-xl p-3">
            <div class="flex  justify-center">
                <div class="flex justify-center gap-3">
                    <label>
                        <input class="bg-gray-200 rounded-md transition hover:bg-gray-300 md:w-60 md:h-13 2xl:w-70 2xl:h-13" bind:value={todotitle} />
                    </label>
                    <button class="border p-1.5 bg-gray-200 rounded-md transition hover:bg-blue-300 md:text-2xl 2xl:text-3xl" on:click={add}>作成</button>
                </div>
            </div>
            {#if Todos.length === 0}
            <div class="flex justify-center font-bold">Todoがまだ1つもありません</div>
            {:else}
                <ul class="flex flex-col justify-center items-center">
                    {#each Todos as todo, index}
                                <li class="p-3 font-bold text-xl border-1 border-solid rounded-md my-2 flex felx-row justify-center items-center shadow-md md:w-170 lg:w-170  2xl:h-30 2xl:w-300">
                                        <input type="checkbox" class="mr-4" checked={todo.completed} on:change={() => cheak(index)} />
                                        <button class="bg-gray-500 border rounded-md p-1.5 w-15a mr-4 text-white transition hover:bg-red-800 2xl:h-17 2xl:w-19" on:click={() =>  del(index)}>削除</button>
                                        <button class="bg-gray-500 border rounded-md p-1.5 w-15a mr-4 text-white transition hover:bg-red-800 2xl:h-17" on:click={() => openDatePicker(index)}>期限を設定</button>
                                        <div class="2xl:text-3xl 2xl:h-15 overflow-auto pl-5">
                                            {todo.title}
                                        </div>
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