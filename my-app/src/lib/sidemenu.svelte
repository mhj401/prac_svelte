<script lang="ts">
	import { page } from '$app/stores';

	$: console.log($page.url.pathname); // 현재 경로를 출력
</script>

<div class="sidebar">
	<a href="/" class:active={$page.url.pathname === '/'}>Main</a>
	<a href="/user" class:active={$page.url.pathname === '/user'}>User</a>
	<a href="/movie" class:active={$page.url.pathname === '/movie'}>Movie</a>
	<a href="/ad" class:active={$page.url.pathname === '/ad'}>AD</a>
</div>

<style>
	.sidebar {
		height: 100%;
		width: 150px;
		position: fixed;
		display: flex;
		flex-direction: column;
		gap: 5px;
		border: 1px solid rgb(220, 220, 220);
		padding-top: 5px;
	}

	.sidebar a {
		text-align: center;
		padding: 10px 0;
		cursor: pointer;
		border: none;
		background-color: white;
		text-decoration: none;
		color: rgb(50, 50, 50);
	}

	a.active {
		color: white;
		background-color: rgb(52, 52, 52);
		/* border: none; */
	}
</style>
