<script lang="ts">
	import logo from '$lib/images/logo.svg';
	import Darkmode from './darkmode.svelte';
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
			<a href="https://github.com/mizuchilabs" class="hover:text-primary" target="_blank">
				<iconify-icon icon="line-md:github-loop" width="24" />
			</a>
			<Darkmode />
		</nav>
	</div>
</header>
