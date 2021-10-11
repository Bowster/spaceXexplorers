<script context="module">
	export async function load({ error, status }) {
		return {
			props: { error, status }
		};
	}
</script>

<script>
	export let error, status;
</script>

<svelte:head>
	<title>{status}</title>
</svelte:head>

<h1>Uh no!</h1>

<p>looks like you hit a page that doesn't exist</p>

<h2>{status}: {error.message}</h2>
