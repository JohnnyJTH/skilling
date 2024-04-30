<script>
	import { Button } from '$lib/components/ui/button';
import Mål from './_components/Mål.svelte';
</script>

<div class="flex justify-between">
	<h1 class="text-4xl font-extrabold tracking-tight scroll-m-20 lg:text-5xl">Mål</h1>
	<Button disabled>Nyt mål</Button>
</div>
<div class="flex flex-col gap-4">
	<Mål name="Sko" achieved={300} wanted={1400} /> 
	<Mål name="Telefon" achieved={4000} wanted={7000} /> 
</div>
