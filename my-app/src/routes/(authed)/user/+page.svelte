<script lang="ts">
	import { onMount } from 'svelte';
	import {
		faAnglesRight,
		faAnglesLeft,
		faAngleLeft,
		faChevronRight
	} from '@fortawesome/free-solid-svg-icons';
	import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';

	function formatCount(count: number): string {
		if (count >= 1000000) {
			return (count / 1000000).toFixed(1) + 'M';
		} else if (count >= 1000) {
			return (count / 1000).toFixed(1) + 'K';
		}
		return count.toString();
	}

	interface User {
		name: string;
		createOuting: number;
		joinOuting: number;
		followerCount: number;
	}

	let users: User[] = [
		{ name: 'Moon HongJoo', joinOuting: 30, createOuting: 12, followerCount: 31 },
		{ name: 'Lee Sanghyuk', joinOuting: 0, createOuting: 106, followerCount: 2300 },
		{ name: 'Lee Jae-min', joinOuting: 1, createOuting: 45, followerCount: 1500 },
		{ name: 'Kim Chang-dong', joinOuting: 21, createOuting: 67, followerCount: 2100 },
		{ name: 'Park Jin-sung', joinOuting: 35, createOuting: 99, followerCount: 5000 },
		{ name: 'Kim Dong-ha', joinOuting: 23, createOuting: 54, followerCount: 1200 },
		{ name: 'Heo Su', joinOuting: 11, createOuting: 76, followerCount: 3400 },
		{ name: 'Jang Ha-gwon', joinOuting: 9, createOuting: 43, followerCount: 2100 },
		{ name: 'Park Jae-hyuk', joinOuting: 7, createOuting: 132, followerCount: 7100 },
		{ name: 'Jeong Ji-hoon', joinOuting: 23, createOuting: 120, followerCount: 8200 },
		{ name: 'Kim Hyuk-kyu', joinOuting: 40, createOuting: 144, followerCount: 9500 }
	];

	let currentPage = 1;
	const itemsPerPage = 5;
	const totalPages = Math.ceil(users.length / itemsPerPage);

	let currentPageUsers: User[] = getCurrentPageUsers();
	let pageNumbers: number[] = []; // 빈 배열로 초기화

	function getCurrentPageUsers() {
		const start = (currentPage - 1) * itemsPerPage;
		const end = start + itemsPerPage;
		return users.slice(start, end);
	}

	function changePage(page: number) {
		if (page >= 1 && page <= totalPages) {
			currentPage = page; // currentPage 업데이트
			currentPageUsers = getCurrentPageUsers(); // 현재 페이지의 유저 업데이트
			console.log('현재 페이지:', currentPage); // 추가된 로그
		}
		getPageNumbers();
	}

	// 페이지 번호 생성
	function getPageNumbers() {
		const maxPagesToShow = Math.min(5, totalPages); // Limit to 5 or fewer if totalPages is less
		let startPage = Math.max(1, currentPage - Math.floor(maxPagesToShow / 2));
		let endPage = startPage + maxPagesToShow - 1;

		if (endPage > totalPages) {
			endPage = totalPages;
			startPage = Math.max(1, endPage - maxPagesToShow + 1);
		}

		// Reset pageNumbers based on the actual range
		pageNumbers = [];
		for (let i = startPage; i <= endPage; i++) {
			pageNumbers.push(i);
		}

		console.log('총 페이지:', totalPages);
		console.log('생성된 페이지 번호:', pageNumbers); // 추가된 로그
	}

	onMount(() => {
		getPageNumbers();
	});

	currentPageUsers = getCurrentPageUsers();
</script>

<h1>유저 관리</h1>

<div class="user_wrap">
	<div class="list_head tr">
		<div class="td">이름</div>
		<div class="td">생성한 아우팅</div>
		<div class="td">가입한 아우팅</div>
		<div class="td">팔로워</div>
	</div>

	<div class="list_wrap">
		{#each currentPageUsers as user}
			<div class="user_list tr">
				<div class="user_name td">{user.name}</div>
				<div class="user_movie td">{user.createOuting}</div>
				<div class="user_movie td">{user.joinOuting}</div>
				<div class="user_follower td">{formatCount(user.followerCount)}</div>
			</div>
		{/each}
	</div>

	<!-- 페이징 버튼 -->
	<div class="pagination">
		<!-- 처음 버튼 -->
		<button class="first_btn" on:click={() => changePage(1)} disabled={currentPage === 1}>
			<FontAwesomeIcon icon={faAnglesLeft} />
		</button>
		<!-- 이전 버튼 -->
		<button on:click={() => changePage(currentPage - 1)} disabled={currentPage === 1}>
			<FontAwesomeIcon icon={faAngleLeft} />
		</button>

		<!-- 페이지버튼 -->
		{#each pageNumbers as page}
			<button
				class="num_btn"
				on:click={() => {
					console.log('페이지 번호:', page);
					changePage(page);
				}}
				class:selected={page === currentPage}
			>
				{page}
			</button>
		{/each}

		<!-- 다음 버튼 -->
		<button on:click={() => changePage(currentPage + 1)} disabled={currentPage === totalPages}>
			<FontAwesomeIcon icon={faChevronRight} />
		</button>
		<!-- 끝 버튼 -->
		<button
			class="last_btn"
			on:click={() => changePage(totalPages)}
			disabled={currentPage === totalPages}
		>
			<FontAwesomeIcon icon={faAnglesRight} />
		</button>
	</div>
</div>

<style>
	h1 {
		padding: 20px 0;
		margin-left: 200px;
		color: #4a4a4a;
	}

	.user_wrap {
		max-width: 1000px;
		margin: auto;
	}

	.list_head.tr {
		border: none;
		background-color: #8b93c9;
		margin-bottom: 10px;
		height: 60px;
		line-height: 60px;
	}

	.list_head .td {
		color: white;
		font-size: 14px;
	}

	.list_wrap {
		width: 100%;
		display: flex;
		flex-direction: column;
		gap: 15px 0;
	}

	.tr {
		width: 100%;
		height: 100px;
		line-height: 100px;
		background-color: white;
		display: flex;
		justify-content: space-between;
		border-radius: 10px;
		box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
	}

	.td {
		min-width: 200px;
		text-align: center;
		display: flex;
		align-content: center;
		justify-content: center;
		color: #6650a2;
		font-weight: 900;
		font-size: 16px;
	}

	/* 페이징 스타일 */
	.pagination {
		display: flex;
		justify-content: center;
		align-items: center;
		margin-top: 20px;
	}

	.pagination button {
		background-color: #8b93c9;
		color: white;
		padding: 10px 20px;
		border: none;
		border-radius: 5px;
		margin: 0 10px;
		cursor: pointer;
		transition: background-color 0.3s ease;
	}

	.pagination .first_btn,
	.pagination .last_btn {
		margin: 0px;
		padding: 10px;
	}

	.pagination button:disabled {
		background-color: #ccc;
		cursor: not-allowed;
	}

	.pagination .num_btn {
		background-color: #ccc;
		padding: 10px 15px;
		border: none;
		border-radius: 5px;
		margin: 0 5px;
		cursor: pointer;
		transition: background-color 0.3s ease;
	}

	.pagination .num_btn.selected {
		background-color: #8b93c9;
		color: white;
	}
</style>
