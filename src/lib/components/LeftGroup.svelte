<script lang="ts">
	import type { BatteryOutput, CpuOutput, MemoryOutput } from 'zebar';

	import Button from './Button.svelte';
	import Meter from './Meter.svelte';

	type LeftGroupProps = {
		battery: BatteryOutput | null;
		cpu: CpuOutput;
		memory: MemoryOutput;
	};

	let { battery, cpu, memory }: LeftGroupProps = $props();
</script>

<div class="flex flex-row gap-3 items-center">
	<Button class="text-zb-icon" iconClass="md-heart" />
	<div class="flex gap-1 items-center">
		<i class="nf nf-fa-memory"></i>
		<Meter class="bg-zb-memory" percent={Math.round(memory?.usage ?? 0)} />
	</div>
	<div class="flex gap-1 items-center">
		<i class="nf nf-oct-cpu"></i>
		<Meter class="bg-zb-cpu" percent={Math.round(cpu?.usage ?? 0)} />
	</div>
	{#if battery || true}
		<div class="flex gap-1 items-center">
			<i class="nf nf-md-lightning_bolt"></i>
			<Meter class="bg-zb-battery-good" percent={Math.round(battery?.chargePercent || 50)} />
		</div>
	{/if}
</div>
