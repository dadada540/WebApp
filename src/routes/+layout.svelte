<script lang="ts">
    import { onMount } from 'svelte';
	import '../app.css';

	
	let { children } = $props();
	let isOpen = false;

	onMount(() => {
		if (typeof window === 'undefined') return;
		const path = window.location.pathname;
		if (path === '/') {
			window.location.href = '/Home';
		}
	})

	
</script>

{@render children()}
