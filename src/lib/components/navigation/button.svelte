<script lang="ts">
	import type { HTMLAnchorAttributes, HTMLButtonAttributes } from 'svelte/elements';
	import { twMerge } from 'tailwind-merge';

	type $$Props = HTMLButtonAttributes &
		HTMLAnchorAttributes & {
			className?: string;
			href?: string;
			size?: 'sm' | 'md';
			square?: boolean;
			variant?: 'default' | 'primary' | 'transparent' | 'active';
		};

	export let className: $$Props['className'] = '';
	export let href: $$Props['href'] = '';
	export let size: $$Props['size'] = 'md';
	export let square: $$Props['square'] = false;
	export let variant: $$Props['variant'] = 'default';

	const { class: __class, disabled, ...rest } = $$restProps;

	$: _class = twMerge(
		'font-semibold tracking-wide',
		'relative flex items-center justify-center whitespace-nowrap',
		size === 'sm' && 'px-3.5 h-9 text-sm rounded-md',
		size === 'md' && 'px-4 h-10 text-base rounded-md',
		square && size === 'sm' && 'px-0 w-9',
		square && size === 'md' && 'px-0 w-10',
		variant === 'default' &&
			'bg-white text-neutral-800/80 border border-neutral-200 shadow-sm hover:bg-neutral-50',
		variant === 'primary' && 'bg-blue-600/90 text-neutral-50 hover:bg-blue-600',
		variant === 'transparent' && 'text-neutral-800/80 hover:bg-neutral-100/80',
		variant === 'active' && 'text-blue-600 bg-blue-50/90 hover:bg-blue-100/60',
		disabled && 'pointer-events-none opacity-65',
		className,
		__class
	);
</script>

{#if href}
	<a {href} class={_class} {...rest}>
		<slot />
	</a>
{:else}
	<button class={_class} {...rest} on:click>
		<slot />
	</button>
{/if}
