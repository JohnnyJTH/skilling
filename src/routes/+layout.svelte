<script>
	import CircleUser from 'lucide-svelte/icons/circle-user';
	import Menu from 'lucide-svelte/icons/menu';
	import Package2 from 'lucide-svelte/icons/package-2';
	import Search from 'lucide-svelte/icons/search';

	import { Button } from '$lib/components/ui/button';
	import { Input } from '$lib/components/ui/input';

	import * as DropdownMenu from '$lib/components/ui/dropdown-menu';
	import * as Sheet from '$lib/components/ui/sheet';

	import '../app.pcss';
	import { page } from '$app/stores';

	const NAV_ITEMS = [
		{
			name: 'Oversigt',
			href: '/'
		},
		{
			name: 'Overførsler',
			href: '/overførsler'
		},
		{
			name: 'Besparelser',
			href: '/besparelser'
		},
		{
			name: 'Mål',
			href: '/mål'
		}
	];

	$: title = $page.url.pathname === '/' ? 'Skilling' : `${decodeURI($page.url.pathname.split('/')[1])} - Skilling`;
</script>

<svelte:head>
	<title>{title}</title>
</svelte:head>

<div class="flex flex-col w-full min-h-screen">
	<header class="sticky top-0 flex items-center h-16 gap-4 px-4 border-b bg-background md:px-6">
		<nav
			class="flex-col hidden gap-6 text-lg font-medium md:flex md:flex-row md:items-center md:gap-5 md:text-sm lg:gap-6"
		>
			<a href="/" class="flex items-center gap-2 text-lg font-semibold size-6 md:text-base">
				<img src="/favicon.png" alt="Skilling" class="size-6" />
				<span class="sr-only">Skilling</span>
			</a>
			{#each NAV_ITEMS as item}
				<a
					href={item.href}
					class="transition-colors {decodeURI($page.url.pathname) === item.href
						? 'text-foreground'
						: 'text-muted-foreground'} hover:text-foreground"
				>
					{item.name}
				</a>
			{/each}
		</nav>
		<Sheet.Root>
			<Sheet.Trigger asChild let:builder>
				<Button variant="outline" size="icon" class="shrink-0 md:hidden" builders={[builder]}>
					<Menu class="w-5 h-5" />
					<span class="sr-only">Toggle navigation menu</span>
				</Button>
			</Sheet.Trigger>
			<Sheet.Content side="left">
				<nav class="grid gap-6 text-lg font-medium">
					<a href="##" class="flex items-center gap-2 text-lg font-semibold">
						<Package2 class="w-6 h-6" />
						<span class="sr-only">Skilling</span>
					</a>
					{#each NAV_ITEMS as item}
						<a
							href={item.href}
							class="transition-colors {decodeURI($page.url.pathname) === item.href
								? 'text-foreground'
								: 'text-muted-foreground'} hover:text-foreground"
						>
							{item.name}
						</a>
					{/each}
				</nav>
			</Sheet.Content>
		</Sheet.Root>
		<div class="flex items-center w-full gap-4 md:ml-auto md:gap-2 lg:gap-4">
			<form class="flex-1 ml-auto sm:flex-initial">
				<div class="relative">
					<Search class="absolute left-2.5 top-2.5 h-4 w-4 text-muted-foreground" />
					<Input
						type="search"
						placeholder="Søg på navn, kategori eller beløb"
						class="pl-8 sm:w-[300px] md:w-[200px] lg:w-[300px]"
					/>
				</div>
			</form>
			<DropdownMenu.Root>
				<DropdownMenu.Trigger asChild let:builder>
					<Button builders={[builder]} variant="secondary" size="icon" class="rounded-full">
						<CircleUser class="w-5 h-5" />
						<span class="sr-only">Toggle user menu</span>
					</Button>
				</DropdownMenu.Trigger>
				<DropdownMenu.Content align="end">
					<DropdownMenu.Label>Min Konto</DropdownMenu.Label>
					<DropdownMenu.Separator />
					<DropdownMenu.Item>Indstillinger</DropdownMenu.Item>
					<DropdownMenu.Item>Hjælp</DropdownMenu.Item>
					<DropdownMenu.Separator />
					<DropdownMenu.Item>Log ud</DropdownMenu.Item>
				</DropdownMenu.Content>
			</DropdownMenu.Root>
		</div>
	</header>
	<main class="flex flex-col flex-1 gap-4 p-4 md:gap-8 md:p-8">
		<slot />
	</main>
</div>
