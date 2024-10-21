<script lang="ts">
	import { Button } from '$lib/components/ui/button/index';
	import * as Card from '$lib/components/ui/card';
	import { onMount } from 'svelte';

	interface Project {
		name: string;
		description: string;
		repoUrl: string;
		pageUrl: string;
		stars: number;
		forks: number;
		license: string;
		topics: string[];
		archived: boolean;
	}

	let activeProjects: Project[] = [];
	let inactiveProjects: Project[] = [];

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
				topics: repo.topics,
				archived: repo.archived
			}));
			activeProjects = projects.filter((repo: any) => !repo.archived && repo.topics?.length > 0);
			inactiveProjects = projects.filter((repo: any) => repo.archived && repo.topics?.length > 0);
		}
	});
</script>

<!-- Projects Section -->
<section class="container mt-12 flex flex-col gap-4">
	{#if activeProjects.length !== 0}
		<h3 class="text-2xl font-semibold">Active Projects</h3>
		<div class="flex flex-row gap-2">
			{#each activeProjects as project}
				<Card.Root class="w-[350px]">
					<Card.Header>
						<Card.Title class="flex flex-row items-center justify-between gap-2 py-2 font-semibold">
							{project.name}

							<div class="flex flex-row items-center gap-1">
								<div
									class="flex flex-row items-center gap-1 rounded-full bg-primary/10 px-2 py-0.5"
								>
									<iconify-icon icon="solar:star-bold-duotone" class="text-primary" width="16" />
									<span class="text-primary/50">{project.stars}</span>
								</div>

								<div
									class="flex flex-row items-center gap-1 rounded-full bg-primary/10 px-2 py-0.5"
								>
									<iconify-icon icon="line-md:fork-right" class="text-primary/50" width="16" />
									<span class="text-primary/50">{project.forks}</span>
								</div>
							</div>
						</Card.Title>
						<Card.Description>{project.description}</Card.Description>
					</Card.Header>
					<Card.Content class="flex flex-row gap-4">
						<Button
							variant="secondary"
							href={project.repoUrl}
							target="_blank"
							class="bg-primary/25 font-semibold hover:bg-primary/50"
						>
							View Repo
						</Button>
						{#if project.pageUrl}
							<Button
								variant="outline"
								href={project.pageUrl}
								target="_blank"
								class="bg-background-muted border-primary/35 font-semibold hover:bg-primary/20"
							>
								Documentation
							</Button>
						{/if}
					</Card.Content>
				</Card.Root>
			{/each}
		</div>
	{/if}

	{#if inactiveProjects.length !== 0}
		<h3 class="text-2xl font-semibold">Archived Projects</h3>
		<div class="flex flex-row gap-2">
			{#each inactiveProjects as project}
				<Card.Root class="w-[350px]">
					<Card.Header>
						<Card.Title class="flex flex-row items-center justify-between gap-2 py-2 font-semibold">
							{project.name.charAt(0).toUpperCase() + project.name.slice(1)}

							<div class="flex flex-row items-center gap-1">
								<div
									class="flex flex-row items-center gap-1 rounded-full bg-primary/10 px-2 py-0.5"
								>
									<iconify-icon icon="solar:star-bold-duotone" class="text-primary" width="16" />
									<span class="text-primary/50">{project.stars}</span>
								</div>

								<div
									class="flex flex-row items-center gap-1 rounded-full bg-primary/10 px-2 py-0.5"
								>
									<iconify-icon icon="line-md:fork-right" class="text-primary/50" width="16" />
									<span class="text-primary/50">{project.forks}</span>
								</div>
							</div>
						</Card.Title>
						<Card.Description>{project.description}</Card.Description>
					</Card.Header>
					<Card.Content class="flex flex-row gap-4">
						<Button
							variant="secondary"
							href={project.repoUrl}
							target="_blank"
							class="bg-primary/25 font-semibold hover:bg-primary/50"
						>
							View Repo
						</Button>
						{#if project.pageUrl}
							<Button
								variant="outline"
								href={project.pageUrl}
								target="_blank"
								class="bg-background-muted border-primary/35 font-semibold hover:bg-primary/20"
							>
								Documentation
							</Button>
						{/if}
					</Card.Content>
				</Card.Root>
			{/each}
		</div>
	{/if}
</section>
