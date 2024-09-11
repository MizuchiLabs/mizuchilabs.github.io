<script lang="ts">
</script>

<footer
	class="py-38 bottom-0 flex h-52 w-full flex-col items-center justify-between gap-4 bg-primary/10 backdrop-blur-sm"
>
	<div
		class="container flex flex-row items-center justify-between gap-4 pt-8 font-mono text-xl text-primary"
	>
		<span></span>
		<div class="flex flex-row items-center gap-1">
			<span class="opacity-25">Mizuchi</span>
			<span class="opacity-40">Labs</span>
		</div>
	</div>

	<div
		class="container flex flex-row items-center justify-between gap-4 border-t border-primary/25 py-4"
	>
		<!-- Copyright -->
		<div class="flex flex-row items-center gap-1 text-muted-foreground">
			<iconify-icon icon="fa-regular:copyright" width="16" />
			<span class="font-mono text-xs">
				{new Date().getFullYear()} Mizuchi Labs
			</span>
		</div>

		<!-- Social Links -->
		<div class="flex flex-row items-center gap-2">
			<span class="font-mono text-sm italic text-muted-foreground">Made with</span>
			<iconify-icon icon="fluent-emoji-flat:dragon-face" width="24" />
		</div>
	</div>
</footer>
