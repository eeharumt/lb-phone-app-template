<script lang="ts">
	let count = 0;
</script>

<div class="sample-style">
	<h1>Svelte Sample</h1>
	<button class="btn btn-primary btn-wide text-white" on:click={() => count++}>CountUP</button>
	<div >
		Count: {count}
	</div>
</div>

<style>
	.sample-style {
		padding: 80px 40px;
		color: aqua;
	}
</style>