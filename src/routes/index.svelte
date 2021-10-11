<script context="module">
	import { gql, GraphQLClient } from 'graphql-request';
	export async function load() {
		const graphCmsClient = new GraphQLClient(
			'https://api-eu-central-1.graphcms.com/v2/ckumppsk33ni901xpa4sueigl/master',
			{ headers: {} }
		);
		const query = gql`
			query Launches {
				launches {
					id
					slug
					date
					name
				}
			}
		`;
		const { launches } = await graphCmsClient.request(query);
		return {
			props: { launches }
		};
	}
</script>

<script>
	export let launches;
</script>

<svelte:head>
	<title>SpaceX Explorers</title>
</svelte:head>

<h1>Welcome to SvelteKit</h1>
<p>
	Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the
	documentation
</p>

<ul>
	{#each launches as { slug, name, date }}
		<li>
			<a href={`/mission/${slug}`}>
				<h2>{name}</h2>
				<time>{date}</time>
			</a>
		</li>
	{/each}
</ul>
