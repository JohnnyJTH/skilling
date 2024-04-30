<script lang="ts">
	import Activity from 'lucide-svelte/icons/activity';
	import ArrowUpRight from 'lucide-svelte/icons/arrow-up-right';
	import CreditCard from 'lucide-svelte/icons/credit-card';
	import DollarSign from 'lucide-svelte/icons/dollar-sign';
	import ShoppingCart from 'lucide-svelte/icons/shopping-cart';

	import { Overførsel } from '$lib/components';
	import { Button } from '$lib/components/ui/button/index.js';
	import * as Card from '$lib/components/ui/card/index.js';
	import { formatNumber } from '$lib/utils';
	import { onMount } from 'svelte';
	import { DateTime } from 'luxon';

	let chartEl: HTMLElement;
	let treeEl: HTMLElement;
	onMount(async () => {
		// @ts-ignore
		const ApexCharts = (await import('apexcharts')).default;
		const areaChart = new ApexCharts(chartEl, {
			chart: {
				type: 'area'
			},
			colors: ['#2563eb', '#dc2626'],
			datalabels: {
				enabled: false
			},
			series: [
				{
					name: 'Indkomst',
					data: [19947, 17846, 17984, 19947]
				},
				{
					name: 'Udgifter',
					data: [16845, 15362, 13043, 16845]
				}
			],
			xaxis: {
				categories: [...Array(4)]
					.map((_, i) =>
						DateTime.now().setLocale('da-DK').minus({ months: i }).toLocaleString({ month: 'long' })
					)
					.reverse()
			},
			stroke: {
				curve: 'smooth'
			}
		});
		areaChart.render();

		const treeChart = new ApexCharts(treeEl, {
			chart: {
				type: 'treemap',
				height: 400
			},
			colors: ['#2563eb', '#dc2626'],
			series: [
				{
					name: 'Indkomst',
					data: [
						{
							x: 'Løn',
							y: 16000
						},
						{
							x: 'SU',
							y: 1400
						}
					]
				},
				{
					name: 'Udgifter',
					data: [
						{
							x: 'Indkøb',
							y: 1500
						},
						{
							x: 'El',
							y: 2000
						},
						{
							x: 'Vand',
							y: 1500
						},
						{
							x: 'Husleje',
							y: 7500
						},
						{
							x: 'Andet',
							y: 1000
						}
					]
				}
			]
		});
		treeChart.render();
	});
</script>

<div class="grid gap-4 md:grid-cols-2 md:gap-8 lg:grid-cols-4">
	<Card.Root>
		<Card.Header class="flex flex-row items-center justify-between pb-2 space-y-0">
			<Card.Title class="text-sm font-medium">Indkomst</Card.Title>
			<DollarSign class="w-4 h-4 text-muted-foreground" />
		</Card.Header>
		<Card.Content>
			<div class="text-2xl font-bold">{formatNumber(19947)}</div>
			<p class="text-xs text-primary">+20,1% fra siste måned</p>
		</Card.Content>
	</Card.Root>
	<Card.Root>
		<Card.Header class="flex flex-row items-center justify-between pb-2 space-y-0">
			<Card.Title class="text-sm font-medium">Faste udgifter</Card.Title>
			<ShoppingCart class="w-4 h-4 text-muted-foreground" />
		</Card.Header>
		<Card.Content>
			<div class="text-2xl font-bold">{formatNumber(10845)}</div>
			<p class="text-xs text-destructive">+5,3% fra sidste måned</p>
		</Card.Content>
	</Card.Root>
	<Card.Root>
		<Card.Header class="flex flex-row items-center justify-between pb-2 space-y-0">
			<Card.Title class="text-sm font-medium">Andre udgifter</Card.Title>
			<Activity class="w-4 h-4 text-muted-foreground" />
		</Card.Header>
		<Card.Content>
			<div class="text-2xl font-bold">{formatNumber(5845)}</div>
			<p class="text-xs text-destructive">+17,1% fra sidste måned</p>
		</Card.Content>
	</Card.Root>
	<Card.Root>
		<Card.Header class="flex flex-row items-center justify-between pb-2 space-y-0">
			<Card.Title class="text-sm font-medium">Mulige besparelser</Card.Title>
			<CreditCard class="w-4 h-4 text-muted-foreground" />
		</Card.Header>
		<Card.Content>
			<div class="text-2xl font-bold">{formatNumber(1498)}</div>
			<a href="/besparelser" class="text-xs text-primary">Se dine besparelser</a>
		</Card.Content>
	</Card.Root>
</div>
<div class="grid gap-4 md:gap-8 lg:grid-cols-2 xl:grid-cols-3">
	<Card.Root>
		<Card.Header class="flex flex-row items-center">
			<div class="grid gap-2">
				<Card.Title>Overførsler</Card.Title>
				<Card.Description>Nyeste aktiviteter på din konto.</Card.Description>
			</div>
			<Button href="/overførsler" variant="secondary" size="sm" class="gap-1 ml-auto">
				Se alle
				<ArrowUpRight class="w-4 h-4" />
			</Button>
		</Card.Header>
		<Card.Content class="grid gap-8">
			<Overførsel navn="Rema 1000" kategori="Indkøb" beløb={-856} />
			<Overførsel navn="Tandlæge" kategori="Andet" beløb={-1200} />
			<Overførsel navn="MobilePay" kategori="Andet" beløb={500} />
			<Overførsel navn="Bowling" kategori="Fritid" beløb={-259} />
		</Card.Content>
	</Card.Root>
	<Card.Root>
		<div bind:this={chartEl} class="w-full" />
	</Card.Root>
	<Card.Root class="col-span-2">
		<div bind:this={treeEl} class="w-full" />
	</Card.Root>
</div>
