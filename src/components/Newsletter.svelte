<script>
	// https://rodneylab.com/using-local-storage-sveltekit/
	import { browser } from '$app/environment';
	import { writable } from 'svelte/store';

	const defaultValue = true;
	const initialValue = browser
		? window.localStorage.getItem('isNewsletterOpen') ?? defaultValue
		: defaultValue;

	const isNewsletterOpen = writable(!!initialValue);

	isNewsletterOpen.subscribe((value) => {
		if (browser) {
			window.localStorage.setItem('isNewsletterOpen', value ? 'true' : 'false');
		}
	});

	function toggleNewsletter() {
		$isNewsletterOpen = !$isNewsletterOpen;
	}
</script>

<section class="mb-16 w-full opacity-0 " id="newsletter">
	<div
		class="my border-y border-blue-200 bg-blue-50 p-6 dark:border-gray-600 dark:bg-gray-800 sm:rounded sm:border-x"
	>
		<div class="flex items-center justify-between space-x-4 text-gray-900 dark:text-gray-100">
			<p class="text-lg font-bold md:text-xl">Subscribe to the newsletter</p>

	
		</div>
		{#if isNewsletterOpen}
			<p class="my-1 text-gray-800 dark:text-gray-200">
				Get emails from me about <span class="font-bold"
					>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Libero, ducimus.</span
				>.
			</p>


			<p class="text-sm text-gray-800 dark:text-gray-200">
				5,432 subscribers including my Mom – <a href="/#newsletter">123 issues</a>
			</p>
		{/if}
	</div>
</section>
