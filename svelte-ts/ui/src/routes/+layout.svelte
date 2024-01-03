<script lang="ts">
	import '../app.css';
	import { onMount } from 'svelte';
	import { browser } from '$app/environment';

	let theme = 'dark';
	const devMode = !(typeof window !== 'undefined' && window['invokeNative']);

	function loaddata() {
		window.getSettings().then((settings) => {
			theme = settings.display.theme;
		});
	}

	onMount(() => {
		if (!browser) return;
		if (devMode) {
			document.body.style.visibility = 'visible';
		} else {
			if (typeof window.getSettings === 'function') {
				loaddata();
			} else {
				window.addEventListener('message', (event) => {
					if (event.data === 'componentsLoaded') {
						loaddata();
					}
				});
			}
		}
	});
</script>

<div id="app-root">
	<slot />
</div>

<style>
	#app-root {
		position: relative;
		width: 100%;
		height: 100vh;
		/*上下方向にはみ出した要素ををスクロールさせる*/
		overflow-y: scroll;
		/*スクロールバー非表示（IE・Edge）*/
		-ms-overflow-style: none;
		/*スクロールバー非表示（Firefox）*/
		scrollbar-width: none;
	}
	#app-root::-webkit-scrollbar {
		display: none;
	}
</style>
