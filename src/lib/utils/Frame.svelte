<script lang="ts">
	import classNames from 'classnames';
	import { setContext } from 'svelte';
	import * as transitions from 'svelte/transition';
	import type { TransitionTypes, TransitionParamTypes } from '../types';

	setContext('background', true);
	$: setContext('color', color);

	export let tag: string = 'div';
	export let color: string = 'default';
	export let rounded: boolean = false;
	export let border: boolean = false;
	export let shadow: boolean = false;

	// Export a prop through which you can set a desired transition
	export let transition: TransitionTypes = undefined;
	// Pass in extra transition params
	export let params: TransitionParamTypes = {};

	// your script goes here
	const bgColors = {
		gray: 'bg-gray-100 dark:bg-gray-200 ',
		red: 'bg-red-100 dark:bg-red-200',
		yellow: 'bg-yellow-100 dark:bg-yellow-200 ',
		green: 'bg-green-100 dark:bg-green-200 ',
		indigo: 'bg-indigo-100 dark:bg-indigo-200 ',
		purple: 'bg-purple-100 dark:bg-purple-200 ',
		pink: 'bg-pink-100 dark:bg-pink-200 ',
		blue: 'bg-blue-100 dark:bg-blue-200 ',
		light: 'bg-gray-50 dark:bg-gray-700',
		dark: 'bg-gray-100 dark:bg-gray-700',
		default: 'bg-white dark:bg-gray-800',
		none: ''
	};
	const textColors = {
		gray: 'text-gray-700 dark:text-gray-800',
		red: 'text-red-700 dark:text-red-800',
		yellow: 'text-yellow-700 dark:text-yellow-800',
		green: 'text-green-700 dark:text-green-800',
		indigo: 'text-indigo-700 dark:text-indigo-800',
		purple: 'text-purple-700 dark:text-purple-800',
		pink: 'text-pink-700 dark:text-pink-800',
		blue: 'text-blue-700 dark:text-blue-800',
		light: 'text-gray-700 dark:text-gray-300',
		dark: 'text-gray-700 dark:text-gray-300',
		default: 'text-gray-500 dark:text-gray-400',
		none: ''
	};

	const borderColors = {
		gray: 'border-gray-500 dark:bg-gray-200 ',
		red: 'border-red-500 dark:bg-red-200 ',
		yellow: 'border-yellow-500 dark:bg-tellow-200 ',
		green: 'border-green-500 dark:bg-green-200 ',
		indigo: 'border-indigo-500 dark:bg-indigo-200 ',
		purple: 'border-purple-500 dark:bg-purple-200 ',
		pink: 'border-pink-500 dark:bg-pink-200 ',
		blue: 'border-blue-500 dark:bg-blue-200 ',
		light: 'border-gray-500',
		dark: 'border-gray-500',
		default: 'border-gray-200 dark:border-gray-700',
		none: ''
	};

	// have a custom transition function that returns the desired transition
	let transitionFunc;
	$: transitionFunc = transitions[transition];

	let divClass: string;

	$: divClass = classNames(
		bgColors[color],
		textColors[color],
		rounded && 'rounded-lg ',
		border && 'border',
		borderColors[color],
		shadow && 'shadow-md',
		$$props.class
	);
</script>

{#if transitionFunc}
	<svelte:element this={tag} transition:transitionFunc={params} {...$$restProps} class={divClass}>
		<slot />
	</svelte:element>
{:else}
	<svelte:element this={tag} {...$$restProps} class={divClass}>
		<slot />
	</svelte:element>
{/if}
