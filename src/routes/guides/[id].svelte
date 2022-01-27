<script context="module">
	import { URL_POSTS } from '$lib/env.js';

	export async function load({ fetch, params }) {
		const id = params.id;
		const res = await fetch(`${URL_POSTS}/${id}`);
		const guide = await res.json();

		console.log('Fetching.....guide:', params.id);

		if (res.ok) {
			return {
				props: {
					guide
				}
			};
		}

		return {
			status: 301,
			//error: new Error('Could not fetch the guide')
			redirect: '/guides'
		};
	}
</script>

<script>
	export let guide;
</script>

<div class="guide">
	<h2>{guide.title}</h2>
	<p>{guide.body}</p>
</div>

<style>
	.guide {
		margin-top: 40px;
		padding: 10px;
		border: 1 px dotted rgba(255, 255, 255, 0.2);
	}
</style>
