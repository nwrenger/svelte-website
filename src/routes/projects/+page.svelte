<script lang="ts">
	import { projects } from '$lib';
	import { Badge } from '$lib/components/ui/badge';
	import * as Card from '$lib/components/ui/card';
	import { ExternalLink } from 'lucide-svelte';
	import ImageLoader from './../ImageLoader.svelte';
</script>

<svelte:head>
	<title>Projects - Portfolio</title>
	<meta
		name="description"
		content="Here you can find all the projects I have worked on so far. They range from web development to game development and even to algorithms."
	/>
</svelte:head>

<div class="space-y-4">
	<div class="flex items-center justify-between pb-2">
		<h2>Projects</h2>

		<code>
			Total: {projects.length}
		</code>
	</div>

	<div class="grid w-full gap-6 md:grid-cols-2">
		{#each projects as { title, summary, picture, description, link, archived }}
			<Card.Root
				class="flex h-full transform-gpu flex-col items-start justify-start overflow-hidden rounded-lg border-none shadow transition-all duration-300 ease-out hover:scale-[102%] hover:shadow-lg"
			>
				<a href={'projects/' + picture} target="_blank" class="w-full">
					<ImageLoader
						src={'projects/' + picture}
						alt={title}
						height="h-52 md:h-64"
						rounded="rounded-t-md rounded-b-none"
					/>
				</a>
				<Card.Header class="w-full p-4">
					<div class="flex w-full items-center justify-between">
						<Card.Title class="text-2xl font-semibold">
							{title}
						</Card.Title>
						{#if archived}
							<Badge variant="secondary">Archived</Badge>
						{/if}
					</div>
					<Card.Description class="mb-2 text-base leading-7">
						{summary}
					</Card.Description>
					<p>{@html description}</p>
					<div class="mt-4">
						<a href={link} class="link flex w-fit items-center" target="_blank">
							See the {archived ? 'archived' : ''} Project here
							<ExternalLink class="size- pl-2 pt-[2px]" />
						</a>
					</div>
				</Card.Header>
			</Card.Root>
		{/each}
	</div>
</div>
