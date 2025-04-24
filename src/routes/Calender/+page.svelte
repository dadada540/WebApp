<script>
    import Header from '$lib/header.svelte';

    const today = new Date();
    
    $: year = today.getFullYear();
    $: month = today.getMonth() + 1;
    $: day = today.getDate();

    $: firstday = new Date(year,month,1);
    $: lastday = new Date(year,month + 1,0);
    $: daysInMonth = lastday.getDate();
    $: firstYoubi = firstday.getDay();

    const Youbi = [`日`, `月`, `火`, `水`, `木`, `金`, `土`];

    function getdaysArray(){
        const days = [];

        const daysbeforelastday = firstYoubi;//前月の末日から今月初めの間を埋める（日にち）
        const lastdaybeforemonth = new Date(year,month,0).getDate();
        for (let i = 0; i < daysbeforelastday; i++){
            days.unshift({day: lastdaybeforemonth - i , isnowmonth: false});
        }

    }

</script>

<main>

    <div class="bg-gray-300 h-screen">

        <Header/>

        

    </div>
    
</main>