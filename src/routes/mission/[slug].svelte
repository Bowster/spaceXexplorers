<script context="module">
	export const prerender = true;

	export async function load({ fetch, page: { params } }) {
		const { slug } = params;
		const res = await fetch(`/mission/${slug}.json`);
		if (res.ok) {
			const { mission } = await res.json();

			return {
				props: { mission }
			};
		}
	}
</script>

<script>
	import Tooltip from '$lib/Tooltip.svelte';
	export let mission;

	const { name, date, launchSuccess, launchSite, link, rocket } =
		mission;
</script>

<svelte:head>
	<title>{name}</title>
</svelte:head>
<article>
	<h1>{name}</h1>
	<time>{date}</time>
	{#if launchSuccess}
		<p>Launched Successfully</p>
	{:else}
		<p>Launched Failed</p>
	{/if}
	<Tooltip title={launchSite.longName}
		><p><strong>Launch Site: </strong>{launchSite.name}</p></Tooltip
	>

	<section>
		<h2>Links:</h2>
		<ul>
			{#if link.articleLink}
				<a href={link.articleLink}>Article</a>
			{/if}
			{#if link.pressKit}
				<a href={link.pressKit}>Press Kit</a>
			{/if}
			{#if link.videoLink}
				<a href={link.videoLink}>Video Link</a>
			{/if}
			{#if link.wikipedia}
				<a href={link.wikipedia}>Wikipedia</a>
			{/if}
		</ul>
		{#if link.flickrImages.length > 0}
			{#each link.flickrImages as image}
				<br />
				<img src={image.url} alt={image.alt} />
			{/each}
		{/if}
	</section>
	<h3>
		Rocket Name: {rocket.name}, Type: {rocket.type}
	</h3>
	<img src={rocket.image.url} alt={rocket.name} />
</article>
