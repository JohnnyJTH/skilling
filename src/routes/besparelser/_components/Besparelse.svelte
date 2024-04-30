<script lang="ts">
	import * as Card from '$lib/components/ui/card';
	import * as Collapsible from '$lib/components/ui/collapsible';
	import { formatNumber, toTitleCase } from '$lib/utils';

	export let name: string;
	export let used: number;
	export let average: number;
</script>

<Collapsible.Root>
	<Collapsible.Trigger class="w-full">
		<Card.Root>
			<Card.Header>
				<Card.Title>{toTitleCase(name)}</Card.Title>
				<Card.Description>
					{#if used > average}
						Du kan spare <span class="font-bold text-green-500">{formatNumber(used - average)}</span
						>
					{:else}
						Du sparer <span class="font-bold">{formatNumber(average - used)}</span>
					{/if}
				</Card.Description>
			</Card.Header>
			<Collapsible.Content>
				<Card.Content>
					Du har brugt {formatNumber(used)} til {name}, mens den gennemsnitlige udgift for {name} er
					{formatNumber(average)}.
				</Card.Content>
				<Card.Footer class="pt-4 text-sm border-t text-muted-foreground">
					Disse tal er gennemsnitsværdier, og dine behov kan være lavere eller højere end disse.
				</Card.Footer>
			</Collapsible.Content>
		</Card.Root>
	</Collapsible.Trigger>
</Collapsible.Root>
