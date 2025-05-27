<script lang="ts">
    import Header from '$lib/header.svelte';


    let today = new Date();
    
    $: year = today.getFullYear();
    $: month = today.getMonth();
    $: day = today.getDate();

    $: daysArray = getdaysArray();

    const Youbi = ['日', '月', '火', '水', '木', '金', '土'];

    function getdaysArray(){
        const days = [];

            const firstday = new Date(year,month,1);//今月の初日
            const lastday = new Date(year,month + 1,0);//今月の最終日
            const daysInMonth = lastday.getDate();//今月の日数
            const firstYoubi = firstday.getDay();//今月の初日の曜日

        const daysbeforelastday = new Date(year, month, 1).getDay();;//前月の末日から今月初めの間を埋める（日にち）
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
        if (month === 0) {
            month = 11;
            year -= 1;
        } else {
            month -= 1;
        }
        today = new Date(year, month, 1);
    }

    function movenextmonth(){
        today = new Date(year, month + 1, 1);
    }
    
    //本来ならここに日にち比較の関数を入れるが、めんどいのでスルー

    function datescedule(index : number){
        console.log("選ばれたのは"+ index + "でした");
    }

</script>

<main>

    <div class="bg-gray-300 h-screen">

        <Header/>
        
        <div class="p-14">
         <div class="bg-gray-200 rounded-4xl shadow-2xl">
            <div class="flex item-center justify-between p-4 bg-gray-100 rounded-t-4xl">
                <button class="px-3 py-1 rounded-md hover:bg-gray-200" on:click={movebeforemonth} aria-label="前月に移動">
                    <svg class="h-8 w-8 text-gray-500"  width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round"> 
                         <path stroke="none" d="M0 0h24v24H0z"/>  <polyline points="15 6 9 12 15 18" /></svg>
                </button>
                <h2 class="text-lg font-semibold">{year}年{month + 1}月</h2>
                <button class="px-3 py-1 rounded-md hover:bg-gray-200" on:click={movenextmonth} aria-label="次月に移動">
                    <svg class="h-8 w-8 text-gray-500"  width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round"> 
                         <path stroke="none" d="M0 0h24v24H0z"/>  <polyline points="9 6 15 12 9 18" /></svg>
                </button>
            </div>
            <table class="w-full">
                <thead>
                    <tr>
                        {#each Youbi as youbi}
                            <th class="text-center bg-gray-200 border font-bold p-2">{youbi}</th>
                        {/each}
                    </tr>
                </thead>
                <tbody>
                {#each getdaysArray().map((day, index) => ({ ...day, index })) as week }
                    <tr>
                        {#each getdaysArray().slice(week.index * 7,(week.index + 1) * 7) as date}
                        <td class="text-center rounded-4xl {date.isnowmonth ? 'text-gray-900' : 'text-gray-400'} {date.isToday ? 'font-bold text-2xl p-9' : 'text-sm p-10'}
                         hover:bg-slate-300 transition" on:click={() => datescedule(date.day)}>
                            {date.day}
                        </td>
                        {/each}
                    </tr>
                {/each}
            </table>
         </div>
        </div>
    </div>
    
</main>