<script>
    import { Hamburger } from 'svelte-hamburgers';

    let open;
</script>

<main>
    <div class="p-4">
        <header class=" bg-gray-200 p-3 backdrop-blur-2xl rounded-2xl">
            <h1 class="text-3xl font-light text-gray-900">
                AppName
            </h1>  
            <div class="fixed right-2 -mt-11">
                <Hamburger />
                
            </div>
        </header>
    </div>
</main>