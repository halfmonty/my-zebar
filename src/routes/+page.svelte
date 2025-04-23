<script lang="ts">
	import { onMount } from 'svelte';
	import * as zebar from 'zebar';
	import type {
		CpuOutput,
		DateOutput,
		GlazeWmOutput,
		MemoryOutput,
		NetworkOutput,
		BatteryOutput,
		WeatherOutput
	} from 'zebar';

	import Group from '$lib/components/Group.svelte';
	import LeftGroup from '$lib/components/LeftGroup.svelte';
	import RightGroup from '$lib/components/RightGroup.svelte';

	let battery = $state<BatteryOutput | null>(null);
	let cpu = $state<CpuOutput | null>(null);
	let date = $state<DateOutput | null>(null);
	let glazewm = $state<GlazeWmOutput | null>(null);
	let memory = $state<MemoryOutput | null>(null);
	let network = $state<NetworkOutput | null>(null);
	let weather = $state<WeatherOutput | null>(null);

	onMount(() => {
		const providers = zebar.createProviderGroup({
			battery: { type: 'battery' },
			cpu: { type: 'cpu' },
			date: { type: 'date', formatting: 'FF' },
			glazewm: { type: 'glazewm' },
			memory: { type: 'memory' },
			network: { type: 'network' },
			weather: { type: 'weather' }
		});

		providers.onOutput(() => {
			battery = providers.outputMap.battery;
			cpu = providers.outputMap.cpu;
			date = providers.outputMap.date;
			glazewm = providers.outputMap.glazewm;
			memory = providers.outputMap.memory;
			network = providers.outputMap.network;
			weather = providers.outputMap.weather;
		});
	});
</script>

<div class="grid grid-cols-3 items-center text-white font-display">
	<Group class="justify-self-start">
		<LeftGroup {battery} cpu={cpu!} memory={memory!} />
	</Group>
	<Group class="justify-self-center font-display">
		<p>{date?.formatted}</p>
	</Group>
	<Group class="justify-self-end">
		<RightGroup network={network!} date={date!} weather={weather!} glazewm={glazewm!} />
	</Group>
</div>
