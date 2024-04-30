<script lang="ts">
	import * as Card from '$lib/components/ui/card';
	import { Progress } from '$lib/components/ui/progress';
	import { formatNumber } from '$lib/utils';

	export let name: string;
	export let achieved: number;
	export let wanted: number;
</script>

<Card.Root class="flex flex-col gap-2 p-2">
	<div class="flex flex-col gap-1">
		<Card.Title>{name}</Card.Title>
		<Card.Description>{formatNumber(achieved)} / {formatNumber(wanted)}</Card.Description>
	</div>
	<Progress class="h-3" value={achieved} max={wanted} />
</Card.Root>
