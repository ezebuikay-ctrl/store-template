<script lang="ts">
	import { title as storeTitle, description as storeDescription } from './store';

	let { data } = $props();
	
	// Pull live products from Appwrite backend data or use fallbacks if empty
	const rawProducts = data?.allProducts?.length ? data.allProducts : [
		{ name: 'shoe', price: '0.0', images: ['https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=500'] },
		{ name: 'JORDAN 1 low', price: '0.0', images: ['https://images.unsplash.com/photo-1552346154-21d32810aba3?w=500'] }
	];

	// Map products to guarantee image and price rendering consistency across app & web
	const products = rawProducts.map((p: any) => {
		let imageUrl = 'https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=500';

		if (p.imageId) {
			imageUrl = `https://cloud.appwrite.io/v1/storage/buckets/${p.bucketId || 'default'}/files/${p.imageId}/view?project=${p.projectId || 'default'}`;
		} else if (p.images && p.images.length > 0) {
			imageUrl = p.images[0];
		} else if (p.image) {
			imageUrl = p.image;
		}

		return {
			...p,
			displayImage: imageUrl
		};
	});
</script>

<svelte:head>
	<title>{storeTitle}</title>
	<meta name="description" content={storeDescription} />
</svelte:head>

<div class="min-h-screen bg-[#121212] text-white pb-28">
	<!-- Top Green Header -->
	<header class="bg-[#006400] px-4 py-3 flex items-center justify-between sticky top-0 z-40 shadow-md">
		<h1 class="text-base font-bold tracking-wide text-white">BEX-MARKET.ng</h1>
		<div class="flex items-center space-x-4">
			<svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
			<svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"></path></svg>
		</div>
	</header>

	<!-- Location Bar -->
	<div class="bg-[#005000] px-4 py-2 text-xs flex items-center text-gray-200">
		<span class="mr-1">📍</span> All Locations ▼
	</div>

	<!-- Promo Banner -->
	<div class="p-4">
		<div class="bg-[#ff8c00] rounded-xl p-4 flex justify-between items-center shadow-lg">
			<div>
				<h2 class="text-black font-bold text-base">Buy affordable products</h2>
				<button class="mt-2 bg-white text-black text-xs font-semibold px-3 py-1.5 rounded-full shadow">Shop Now</button>
			</div>
			<div class="text-3xl">🛒</div>
		</div>
	</div>

	<!-- Categories -->
	<div class="px-4 py-2">
		<h3 class="text-sm font-semibold mb-3 text-gray-300">Categories</h3>
		<div class="grid grid-cols-6 gap-2 text-center text-xs text-gray-200">
			<div class="flex flex-col items-center"><div class="w-10 h-10 bg-[#222] border border-gray-700 rounded-full flex items-center justify-center mb-1 text-sm">🛍️</div>All</div>
			<div class="flex flex-col items-center"><div class="w-10 h-10 bg-[#222] border border-gray-700 rounded-full flex items-center justify-center mb-1 text-sm">👔</div>Fashion</div>
			<div class="flex flex-col items-center"><div class="w-10 h-10 bg-[#222] border border-gray-700 rounded-full flex items-center justify-center mb-1 text-sm">💻</div>Electronics</div>
			<div class="flex flex-col items-center"><div class="w-10 h-10 bg-[#222] border border-gray-700 rounded-full flex items-center justify-center mb-1 text-sm">📱</div>Phones</div>
			<div class="flex flex-col items-center"><div class="w-10 h-10 bg-[#222] border border-gray-700 rounded-full flex items-center justify-center mb-1 text-sm">🖥️</div>Computing</div>
			<div class="flex flex-col items-center"><div class="w-10 h-10 bg-[#222] border border-gray-700 rounded-full flex items-center justify-center mb-1 text-sm">💄</div>Beauty</div>
		</div>
	</div>

	<!-- Popular Products Grid -->
	<div class="px-4 py-4">
		<div class="flex justify-between items-center mb-3">
			<h3 class="text-base font-bold text-white">Popular Products</h3>
			<span class="text-xs text-gray-400">View All</span>
		</div>
		
		<div class="grid grid-cols-2 gap-3">
			{#each products as product}
				<div class="bg-[#1e1e1e] rounded-xl overflow-hidden border border-gray-800 shadow-md">
					<div class="w-full h-36 bg-gray-800 flex items-center justify-center overflow-hidden">
						<img 
							src={product.displayImage} 
							alt={product.name} 
							class="w-full h-full object-cover" 
						/>
					</div>
					<div class="p-3">
						<h4 class="text-sm text-gray-200 font-medium truncate">{product.name}</h4>
						<p class="text-white font-bold text-base mt-1">₦{product.price || '0.0'}</p>
					</div>
				</div>
			{/each}
		</div>
	</div>

	<!-- Bottom Navigation Bar -->
	<nav class="fixed bottom-0 left-0 right-0 bg-[#1a1a1a] border-t border-gray-800 flex justify-around items-center py-3 text-sm z-50 shadow-2xl">
		<button class="flex flex-col items-center text-green-500 font-semibold space-y-0.5">
			<span class="text-lg">🏠</span>
			<span>Home</span>
		</button>
		<button class="flex flex-col items-center text-gray-400 hover:text-white font-medium space-y-0.5">
			<span class="text-lg">❤️</span>
			<span>Favorite</span>
		</button>
		<button class="flex flex-col items-center text-gray-400 hover:text-white font-medium space-y-0.5">
			<span class="text-lg">🛒</span>
			<span>Market</span>
		</button>
		<button class="flex flex-col items-center text-gray-400 hover:text-white font-medium space-y-0.5">
			<span class="text-lg">👤</span>
			<span>Profile</span>
		</button>
	</nav>
</div>
