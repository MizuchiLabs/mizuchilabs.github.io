<script lang="ts">
	import { Button } from '$lib/components/ui/button/index';
	import logo from '$lib/images/logo.svg';
	import Darkmode from './darkmode.svelte';
	import { Github, Coffee } from 'lucide-svelte';
</script>

<header class="w-full bg-primary/10 py-3 shadow-md backdrop-blur-sm">
	<div class="container mx-auto flex items-center justify-between">
		<div class="flex flex-row items-center gap-4">
			<img src={logo} alt="Mizuchi Labs Logo" width="40" />
			<div class="flex flex-row items-center gap-1 font-mono text-2xl italic text-primary">
				<h1 class="opacity-80">Mizuchi</h1>
				<h1 class="opacity-50">Labs</h1>
			</div>
		</div>
		<nav>
			<div class="flex flex-row items-center">
				<Button
					variant="ghost"
					href="https://github.com/mizuchilabs"
					target="_blank"
					size="icon"
					class="!bg-transparent hover:text-primary"
				>
					<Github />
				</Button>
				<Button
					variant="ghost"
					href="https://buymeacoffee.com/d34dscene"
					target="_blank"
					size="icon"
					class="mr-2 !bg-transparent hover:text-primary"
				>
					<Coffee />
				</Button>
				<Darkmode />
			</div>
		</nav>
	</div>
</header>
