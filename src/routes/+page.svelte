<script lang="ts">
	import { Button } from '$lib/components/ui/button/index';
	import * as Card from '$lib/components/ui/card';
	import { onMount } from 'svelte';

	let activeProjects: any[] = [];
	let inactiveProjects: any[] = [];

	// Only display these projects
	let watch: string[] = ['mantrae'];

	onMount(async () => {
		const res = await fetch('https://api.github.com/users/mizuchilabs/repos');
		if (res.ok) {
			const data = await res.json();

			let projects = data.map((repo: any) => ({
				name: repo.name,
				description: repo.description,
				repoUrl: repo.html_url,
				pageUrl: repo.homepage,
				stars: repo.stargazers_count,
				forks: repo.forks_count,
				license: repo.license?.name,
				archived: repo.archived
			}));
			activeProjects = projects.filter((repo: any) => !repo.archived && repo.name.includes(watch));
			inactiveProjects = projects.filter((repo: any) => repo.archived && repo.name.includes(watch));
		}
	});
</script>

<!-- Projects Section -->
<section class="container mt-12 flex flex-col gap-4">
	{#if activeProjects.length !== 0}
		<h3 class="text-2xl font-semibold">Active Projects</h3>
		{#each activeProjects as project}
			<Card.Root class="w-[350px]">
				<Card.Header>
					<Card.Title class="flex flex-row items-center justify-between gap-2 py-2 font-semibold">
						{project.name}

						<div class="flex flex-row items-center gap-1">
							<div class="flex flex-row items-center gap-1 rounded-full bg-primary/10 px-2 py-0.5">
								<iconify-icon icon="solar:star-bold-duotone" class="text-primary" width="16" />
								<span class="text-primary/50">{project.stars}</span>
							</div>

							<div class="flex flex-row items-center gap-1 rounded-full bg-primary/10 px-2 py-0.5">
								<iconify-icon icon="line-md:fork-right" class="text-primary/50" width="16" />
								<span class="text-primary/50">{project.forks}</span>
							</div>
						</div>
					</Card.Title>
					<Card.Description>{project.description}</Card.Description>
				</Card.Header>
				<Card.Content class="flex flex-row gap-2">
					<Button
						variant="secondary"
						href={project.repoUrl}
						target="_blank"
						class="bg-primary/35 font-semibold"
					>
						View Repo
					</Button>
					{#if project.pageUrl}
						<Button
							variant="outline"
							href={project.pageUrl}
							target="_blank"
							class="border-primary/35 font-semibold"
						>
							Documentation
						</Button>
					{/if}
				</Card.Content>
			</Card.Root>
		{/each}
	{/if}

	{#if inactiveProjects.length !== 0}
		<h3 class="text-2xl font-semibold">Archived Projects</h3>
		{#each inactiveProjects as project}
			<Card.Root class="w-[350px]">
				<Card.Header>
					<Card.Title class="flex flex-row items-center justify-between gap-2 py-2 font-semibold">
						{project.name}

						<div class="flex flex-row items-center gap-1">
							<div class="flex flex-row items-center gap-1 rounded-full bg-primary/10 px-2 py-0.5">
								<iconify-icon icon="solar:star-bold-duotone" class="text-primary" width="16" />
								<span class="text-primary/50">{project.stars}</span>
							</div>

							<div class="flex flex-row items-center gap-1 rounded-full bg-primary/10 px-2 py-0.5">
								<iconify-icon icon="line-md:fork-right" class="text-primary/50" width="16" />
								<span class="text-primary/50">{project.forks}</span>
							</div>
						</div>
					</Card.Title>
					<Card.Description>{project.description}</Card.Description>
				</Card.Header>
				<Card.Content class="flex flex-row gap-2">
					<Button
						variant="secondary"
						href={project.repoUrl}
						target="_blank"
						class="bg-primary/35 font-semibold"
					>
						View Repo
					</Button>
					{#if project.pageUrl}
						<Button
							variant="outline"
							href={project.pageUrl}
							target="_blank"
							class="border-primary/35 font-semibold"
						>
							Documentation
						</Button>
					{/if}
				</Card.Content>
			</Card.Root>
		{/each}
	{/if}
</section>
