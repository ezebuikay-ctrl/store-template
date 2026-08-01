<script lang="ts">
	import { title as storeTitle, description as storeDescription } from './store';

	let { data } = $props();
	
	// Print your actual database response to the browser console to inspect the keys!
	console.log("RAW APPWRITE DATA:", data?.allProducts);

	const rawProducts = data?.allProducts?.length ? data.allProducts : [
		{ name: 'Heavy Blouse', price: '40', image: 'https://images.unsplash.com/photo-1434389677669-e08b4cac3105?w=500' }
	];

	const products = rawProducts.map((p: any) => {
		let imageUrl = 'https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=500';

		// Universal property mapper: checks every possible variable name your app might use
		const possibleImageKey = 
			p.image || 
			p.imageId || 
			p.fileId || 
			p.file || 
			p.file_id || 
			p.photo || 
			p.imageUrl || 
			p.attachment || 
			(p.images && p.images[0]);

		if (possibleImageKey) {
			if (typeof possibleImageKey === 'string' && possibleImageKey.startsWith('http')) {
				imageUrl = possibleImageKey;
			} else {
				// Uses your Appwrite configuration parameters
				imageUrl = `https://cloud.appwrite.io/v1/storage/buckets/products/files/${possibleImageKey}/view?project=6808761200388d752ca8`;
			}
		}

		return {
			...p,
			displayImage: imageUrl
		};
	});
</script>
