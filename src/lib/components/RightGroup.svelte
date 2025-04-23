<script lang="ts">
	import type { DateOutput, GlazeWmOutput, NetworkOutput, WeatherOutput } from 'zebar';

	type RightGroupProps = {
		date: DateOutput;
		glazewm: GlazeWmOutput;
		network: NetworkOutput;
		weather: WeatherOutput;
	};

	let { date, glazewm, network, weather }: RightGroupProps = $props();
</script>

<div class="flex flex-row gap-3 items-center">
	<button class="" onclick={() => glazewm.runCommand('shell-exec ms-settings:network-status')}>
		<div class="flex flex-row items-center gap-1">
			{#if network?.defaultInterface?.type == 'ethernet'}
				<i class="nf nf-md-ethernet_cable"></i>
			{:else if network?.defaultInterface!.type == 'wifi'}
				{#if network.defaultGateway!.signalStrength! >= 80}
					<i class="nf nf-md-wifi"></i>
				{:else if network.defaultGateway!.signalStrength! >= 65}
					<i class="nf nf-md-wifi_strength_3"></i>
				{:else if network.defaultGateway!.signalStrength! >= 40}
					<i class="nf nf-md-wifi_strength_2"></i>
				{:else if network.defaultGateway!.signalStrength! >= 25}
					<i class="nf nf-md-wifi_strength_1"></i>
				{:else}
					<i class="nf nf-md-wifi_strength_outline"></i>
				{/if}
				{network.defaultGateway?.ssid}
			{:else}
				<i class="nf nf-md-wifi_strength_off_outline"></i>
			{/if}
		</div>
	</button>

	{#if weather}
		<div>
			{#if weather.status === 'clear_day'}
				<i class="nf nf-weather-day_sunny"></i>
			{:else if weather.status === 'clear_night'}
				<i class="nf nf-weather-night_clear"></i>
			{:else if weather.status === 'cloudy_day'}
				<i class="nf nf-weather-day_cloudy"></i>
			{:else if weather.status === 'cloudy_night'}
				<i class="nf nf-weather-night_alt_cloudy"></i>
			{:else if weather.status === 'light_rain_day'}
				<i class="nf nf-weather-day_sprinkle"></i>
			{:else if weather.status === 'light_rain_night'}
				<i class="nf nf-weather-night_alt_sprinkle"></i>
			{:else if weather.status === 'heavy_rain_day'}
				<i class="nf nf-weather-day_rain"></i>
			{:else if weather.status === 'heavy_rain_night'}
				<i class="nf nf-weather-night_alt_rain"></i>
			{:else if weather.status === 'snow_day'}
				<i class="nf nf-weather-day_snow"></i>
			{:else if weather.status === 'snow_night'}
				<i class="nf nf-weather-night_alt_snow"></i>
			{:else if weather.status === 'thunder_day'}
				<i class="nf nf-weather-day_lightning"></i>
			{:else if weather.status === 'thunder_night'}
				<i class="nf nf-weather-night_alt_lightning"></i>
			{/if}
			{Math.round(weather.fahrenheitTemp)}°
		</div>
	{/if}

	<i class="nf nf-oct-dot_fill"></i>
	{date?.formatted}
</div>
