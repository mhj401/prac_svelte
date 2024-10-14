<script>
	import Header from '$lib/header.svelte';
	import Menu from '$lib/sidemenu.svelte';
</script>

<Header />
<Menu />
<div class="app">
	<slot />
</div>

<style>
	.app {
		margin-left: 200px;
	}
</style>
