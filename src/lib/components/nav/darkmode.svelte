<script lang="ts">
	import { onMount } from 'svelte';
	import Button from '../ui/button/button.svelte';
	import { Moon, Sun } from 'lucide-svelte';

	let darkMode = false;

	function handleSwitchDarkMode() {
		darkMode = !darkMode;
		localStorage.setItem('darkmode', darkMode ? 'dark' : 'light');

		darkMode
			? document.documentElement.classList.add('dark')
			: document.documentElement.classList.remove('dark');
	}

	onMount(() => {
		switch (localStorage.darkmode) {
			case 'dark':
				document.documentElement.classList.add('dark');
				darkMode = true;
				break;
			case 'light':
				document.documentElement.classList.remove('dark');
				darkMode = false;
				break;
			default:
				localStorage.setItem('darkmode', 'light');
				darkMode = false;
		}
	});
</script>

<Button
	variant="ghost"
	on:click={handleSwitchDarkMode}
	class="!bg-transparent hover:text-primary"
	size="icon"
>
	{#if darkMode}
		<Moon />
	{:else}
		<Sun />
	{/if}
</Button>
