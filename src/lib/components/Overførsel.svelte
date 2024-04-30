<script lang="ts">
	import ShoppingCart from 'lucide-svelte/icons/shopping-cart';
	import CreditCard from 'lucide-svelte/icons/credit-card';
	import DollarSign from 'lucide-svelte/icons/dollar-sign';
	import { formatNumber } from '$lib/utils';

	const TYPER = {
		Indkøb: {
			farve: 'text-green-500',
			bgfarve: 'bg-green-500/30',
			ikon: ShoppingCart
		},
		Andet: {
			farve: 'text-zinc-500', 
			bgfarve: 'bg-zinc-500/30',
			ikon: CreditCard
		},
		Fritid: {
			farve: 'text-primary',
			bgfarve: 'bg-primary/30',
			ikon: DollarSign
		}
	};

	export let navn = 'Rema 1000';
	export let kategori: keyof typeof TYPER = 'Indkøb';
	$: type = TYPER[kategori] ?? TYPER.Andet; 
	export let beløb: number;
</script>

<div class="flex items-center gap-4">
	<div class="flex items-center justify-center rounded-full size-9 {type.bgfarve} p-1"> 
		<svelte:component this={type.ikon} class="size-5 {type.farve}" />	
	</div>
	<div class="grid gap-1">
		<p class="text-sm font-medium leading-none">{navn}</p>
		<p class="text-sm text-muted-foreground">{kategori}</p>
	</div>
	<div class="ml-auto font-medium {beløb > 0 && 'rounded bg-primary p-1 text-white'}">
		{formatNumber(beløb)}
	</div>
</div>
