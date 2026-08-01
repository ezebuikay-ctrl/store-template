<script lang="ts">
	import { page } from '$app/stores';
	import { derived } from 'svelte/store';
	import { name as storeName, title as storeTitle, description as storeDescription } from './store';
	import StaggeredGrid from '$lib/components/grid/StaggeredGrid.svelte';
	import Pagination from '$lib/components/pagination/Pagination.svelte';
	import ScrollToTop from '$lib/components/pagination/ScrollToTop.svelte';

	let { data } = $props();
	const allProducts = $derived(data.allProducts);
</script>

<svelte:head>
	<title>{storeTitle}</title>
	<meta name="description" content={storeDescription} />
</svelte:head>

<div class="min-h-screen bg-[#121212] text-white pb-20">
	<!-- App Header -->
	<header class="bg-[#006400] px-4 py-3 flex items-center justify-between shadow-md sticky top-0 z-40">
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

	<!-- Categories Bar -->
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

	<!-- Main Product Section -->
	<div class="px-4 py-4" id="navigation">
		<div class="flex justify-between items-center mb-3">
			<h3 class="text-base font-bold text-white">Popular Products</h3>
			<span class="text-xs text-gray-400">View All</span>
		</div>
		
		<!-- Dynamic Product Feed -->
		<StaggeredGrid products={allProducts} />
	</div>

	<!-- Bottom Navigation Bar (App Style) -->
	<nav class="fixed bottom-0 left-0 right-0 bg-[#1a1a1a] border-t border-gray-800 flex justify-around py-2.5 text-xs text-gray-400 z-50">
		<button class="flex flex-col items-center text-green-500 font-medium">🏠 Home</button>
		<button class="flex flex-col items-center hover:text-white">❤️ Favorite</button>
		<button class="flex flex-col items-center hover:text-white">🛒 Market</button>
		<button class="flex flex-col items-center hover:text-white">👤 Profile</button>
	</nav>

	<ScrollToTop />
</div>
