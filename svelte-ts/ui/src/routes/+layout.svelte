<script lang="ts">
	import '../app.css';
	import { onMount } from 'svelte';
	import { browser } from '$app/environment';

	let isphoneWrapper = false;
	let theme = 'dark';
	const devMode = !(typeof window !== 'undefined' && window['invokeNative']);

	onMount(() => {
		if (!browser) return;
		if (devMode) {
			document.body.style.visibility = 'visible';
			isphoneWrapper = false;
		} else {
			isphoneWrapper = false;
			window.addEventListener('message', (e) => {
				if (e.data !== 'componentsLoaded') return;
				getSettings().then((settings) => {
					theme = settings.display.theme;
				});
				// onSettingsChange((settings) => {
				// 	theme = settings.display.theme;
				// });
			});
		}
	});
</script>

<div id="app-root">
	<h1>Svelte Sample</h1>
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
  