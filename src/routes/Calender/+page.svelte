<script>
    import Header from '$lib/header.svelte';

    let today = new Date();
    
    $: year = today.getFullYear();
    $: month = today.getMonth() + 1;
    $: day = today.getDate();

    $: firstday = new Date(year,month,1);
    $: lastday = new Date(year,month + 1,0);
    $: daysInMonth = lastday.getDate();
    $: firstYoubi = firstday.getDay();

    $: daysArray = getdaysArray().map((day, index) => ({ ...day, index }));

    const Youbi = ['日', '月', '火', '水', '木', '金', '土'];

    function getdaysArray(){
        const days = [];

        const daysbeforelastday = firstYoubi;//前月の末日から今月初めの間を埋める（日にち）
        const lastdaybeforemonth = new Date(year,month,0).getDate();
        for (let i = 0; i < daysbeforelastday; i++){
            days.unshift({
                day: lastdaybeforemonth - i,
                isnowmonth: false,
                isToday: false
            });
        }

        const month42 = 42 - days.length;
        for (let i = 1; i <= month42; i++){
            days.push({
                day: i,
                isnowmonth: false,
                isToday: false
            });
        }

        // Mark days in the current month and check if they are today
        for (let i = daysbeforelastday; i < daysbeforelastday + daysInMonth; i++) {
            const currentDay = i - daysbeforelastday + 1;
            days[i] = {
                day: currentDay,
                isnowmonth: true,
                isToday: currentDay === day
            };
        }

        return days;

    }

    function movebeforemonth(){
       today = new Date(year, month -1 , 1);
    }

    function movenextmonth(){
        today = new Date(year,month,1);
    }
    
    //本来ならここに日にち比較の関数を入れるが、めんどいのでスルー

</script>

<main>

    <div class="bg-gray-300 h-screen">

        <Header/>

        <div class="bg-white shadow rounded-lg overflow-hidden">
            <div class="flex item-center justify-between p-4 bg-gray-100">
                <button class="px-3 py-1 rounded-md hover:bg-gray-200" on:click={movebeforemonth} aria-label="前月に移動">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M15.707 15.707a1 1 0 01-1.414 0l-5-5a1 1 0 010-1.414l5-5a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 010 1.414z" clip-rule="evenodd" />
                    </svg>
                </button>
                <h2 class="text-lg font-semibold">{year}年{month + 1}月</h2>
                <button class="px-3 py-1 rounded-md hover:bg-gray-200" on:click={movenextmonth} aria-label="次月に移動">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M4.293 15.707a1 1 0 011.414 0L10 11.414l4.293 4.293a1 1 0 011.414-1.414l-5-5a1 1 0 010-1.414l-5-5a1 1 0 111.414 1.414L8.586 10l-4.293 4.293a1 1 0 010 1.414z" clip-rule="evenodd" />
                      </svg>
                </button>
            </div>
            <table class="w-full">
                <thead>
                    <tr>
                        {#each Youbi as youbi}
                            <th class="text-center text-gray-500 font-medium text-sm py-2">{youbi}</th>
                        {/each}
                    </tr>
                </thead>
                <tbody>
                {#each getdaysArray().map((day, index) => ({ ...day, index })) as week }
                    <tr>
                        {#each getdaysArray().slice(week.index * 7,(week.index + 1) * 7) as date}
                        <td class="p-2 text-center text-sm {date.isnowmonth ? 'text-gray-900' : 'text-gray-400'} {date.isToday ? 'font-semibold text-blue-600' : ''}">
                            {date.day}
                        </td>
                        {/each}
                    </tr>
                {/each}
            </table>
        </div>
    </div>
    
</main>