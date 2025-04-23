<script lang="ts">
	import type { Snippet } from 'svelte';
	type Props = {
		children: Snippet;
		class: string;
	};
	let { children, ...rest }: Props = $props();
</script>

<div
	class="flex items-center w-fit p-1 bg-slate-900 border-zinc-900 rounded-full border {rest.class}"
>
	{@render children()}
</div>
