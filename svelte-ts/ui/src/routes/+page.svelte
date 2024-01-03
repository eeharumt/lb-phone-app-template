<script lang="ts">
	let count = 0;
</script>

<div>
	<button class="btn btn-primary btn-wide text-white" on:click={() => count++}>CountUP</button>
	<div>
		Count: {count}
	</div>
</div>
