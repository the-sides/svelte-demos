<script>
	import Lenis from "lenis";
	import { onMount } from "svelte";
	import { fade } from "svelte/transition";
	$: spread = 0;

	onMount(() => {
		// Initialize Lenis
		const lenis = new Lenis({
			autoRaf: true,
		});

		// Listen for the scroll event and log the event data
		lenis.on("scroll", (e) => {
			console.log(e);
		});
	});
	let links = ["News", "Events", "Interviews", "Media"];
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<svelte:window
	on:scroll={(ev) => {
		spread = window.scrollY;
	}}
/>
<article class="w-full bg-black h-[500vh] relative">
	<main class="relative h-[300vh]">
		<img
			src="logo.svg"
			alt=""
			style="transform: translateY(-{spread < 750 ? spread * 0.1 : 75}%);"
			class="fixed z-50 inset-x-0 pt-[calc(50vh-35px)] m-auto w-[450px] pointer-events-none"
		/>
		<section class="sticky top-0 h-screen grid grid-cols-2 grid-rows-2">
			{#each [...[214851219, 1051217841, 273411755, 26543406].entries()] as [i, id]}
				<div
					class="relative overflow-hidden"
					style="transform:translateX({i % 2 ? '' : '-'}{spread *
						(i < 2 ? 0.4 : 0.2)}px) translateY(-{spread * 0.2}px) rotate({i % 2
						? ''
						: '-'}{spread * 0.0}deg)"
				>
					<div
						class="absolute top-0 left-0 w-full h-full bg-gradient-to-r from-black to-gray-900 flex items-center justify-center opacity-50 z-10"
					></div>
					<button
						class="absolute top-0 left-0 w-full h-full flex items-center justify-center z-20 text-white text-2xl hover:scale-150 transition"
					>
						{links[i]}
					</button>
					<iframe
						src="https://player.vimeo.com/video/{id}?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479&amp;autoplay=1&amp;muted=1&amp;background=1&amp;portrait=1&amp#t=10&amp;loop=1"
						frameborder="0"
						allow="autoplay; fullscreen; picture-in-picture; clipboard-write; encrypted-media"
						style="position:absolute;width:auto;height:auto; aspect-ratio:16/9;min-height: 100%;min-width: 100%;top:0;left:0;right:0;margin:auto"
						title="ef_final"
					></iframe>
				</div>
				<script src="https://player.vimeo.com/api/player.js"></script>
			{/each}
		</section>
	</main>
	<div class="h-[400vh]"></div>
</article>

<style>
	main {
		animation: fadeIn 0.5s ease-in-out forwards;
		animation-delay: 1.5s;
		opacity: 0;
	}

	@keyframes fadeIn {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
</style>
