<script>
	import '../app.css';
	import { onMount } from 'svelte';
	import { oeuvres } from '../utils/store.ts';

	// Using ES modules (default)
	import PocketBase from 'pocketbase';

	const pb = new PocketBase('https://artriste-api.beta.andy-cinquin.fr');

	const get_datas = async () => {
		return await pb.collection('oeuvre').getFullList(200 /* batch size */, {
			sort: '-created'
		});
	};

	// set data
	onMount(async () => {
		const records = await get_datas();
		oeuvres.set(records);
	});
</script>

<slot />
