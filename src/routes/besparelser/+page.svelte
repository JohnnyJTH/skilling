<script>
	import Besparelse from './_components/Besparelse.svelte';
</script>

<h1 class="text-4xl font-extrabold tracking-tight scroll-m-20 lg:text-5xl">Besparelser</h1>
<div class="grid grid-cols-2 gap-4">
	<Besparelse name="indkøb" used={2297} average={1557} />
	<Besparelse name="streaming tjenester" used={534} average={300} />  
	<Besparelse name="internet" used={2000} average={2600} /> 
</div>
