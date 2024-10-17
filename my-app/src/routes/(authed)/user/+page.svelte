<script lang="ts">
	import { page } from '$app/stores';
	import { json } from '@sveltejs/kit';

	$: ({ params } = $page);

	function formatCount(count: number): string {
		if (count >= 1000000) {
			return (count / 1000000).toFixed(1) + 'M';
		} else if (count >= 1000) {
			return (count / 1000).toFixed(1) + 'K';
		}
		return count.toString();
	}

	interface User {
		nickName: string;
		name: string;
		movieCount: number;
		followerCount: number;
	}

	let users: User[] = [
		{ nickName: 'ralph', name: 'Moon HongJoo', movieCount: 12, followerCount: 31 },
		{ nickName: 'Faker', name: 'Lee Sanghyuk', movieCount: 106, followerCount: 2300 },
		{ nickName: 'Zefa', name: 'Lee Jae-min', movieCount: 45, followerCount: 1500 },
		{ nickName: 'Canna', name: 'Kim Chang-dong', movieCount: 67, followerCount: 2100 },
		{ nickName: 'Teddy', name: 'Park Jin-sung', movieCount: 99, followerCount: 5000 },
		{ nickName: 'Khan', name: 'Kim Dong-ha', movieCount: 54, followerCount: 1200 },
		{ nickName: 'Showmaker', name: 'Heo Su', movieCount: 76, followerCount: 3400 },
		{ nickName: 'Nuguri', name: 'Jang Ha-gwon', movieCount: 43, followerCount: 2100 },
		{ nickName: 'Ruler', name: 'Park Jae-hyuk', movieCount: 132, followerCount: 7100 },
		{ nickName: 'Chovy', name: 'Jeong Ji-hoon', movieCount: 120, followerCount: 8200 },
		{ nickName: 'Deft', name: 'Kim Hyuk-kyu', movieCount: 144, followerCount: 9500 },
		{ nickName: 'ralph', name: 'Moon HongJoo', movieCount: 12, followerCount: 31 },
		{ nickName: 'Faker', name: 'Lee Sanghyuk', movieCount: 106, followerCount: 2300 },
		{ nickName: 'Zefa', name: 'Lee Jae-min', movieCount: 45, followerCount: 1500 },
		{ nickName: 'Canna', name: 'Kim Chang-dong', movieCount: 67, followerCount: 2100 },
		{ nickName: 'Teddy', name: 'Park Jin-sung', movieCount: 99, followerCount: 5000 },
		{ nickName: 'Khan', name: 'Kim Dong-ha', movieCount: 54, followerCount: 1200 },
		{ nickName: 'Showmaker', name: 'Heo Su', movieCount: 76, followerCount: 3400 },
		{ nickName: 'Nuguri', name: 'Jang Ha-gwon', movieCount: 43, followerCount: 2100 },
		{ nickName: 'Ruler', name: 'Park Jae-hyuk', movieCount: 132, followerCount: 7100 },
		{ nickName: 'Chovy', name: 'Jeong Ji-hoon', movieCount: 120, followerCount: 8200 },
		{ nickName: 'Deft', name: 'Kim Hyuk-kyu', movieCount: 144, followerCount: 9500 },
		{ nickName: 'ralph', name: 'Moon HongJoo', movieCount: 12, followerCount: 31 },
		{ nickName: 'Faker', name: 'Lee Sanghyuk', movieCount: 106, followerCount: 2300 },
		{ nickName: 'Zefa', name: 'Lee Jae-min', movieCount: 45, followerCount: 1500 },
		{ nickName: 'Canna', name: 'Kim Chang-dong', movieCount: 67, followerCount: 2100 },
		{ nickName: 'Teddy', name: 'Park Jin-sung', movieCount: 99, followerCount: 5000 },
		{ nickName: 'Khan', name: 'Kim Dong-ha', movieCount: 54, followerCount: 1200 },
		{ nickName: 'Showmaker', name: 'Heo Su', movieCount: 76, followerCount: 3400 },
		{ nickName: 'Nuguri', name: 'Jang Ha-gwon', movieCount: 43, followerCount: 2100 },
		{ nickName: 'Ruler', name: 'Park Jae-hyuk', movieCount: 132, followerCount: 7100 },
		{ nickName: 'Chovy', name: 'Jeong Ji-hoon', movieCount: 120, followerCount: 8200 },
		{ nickName: 'Deft', name: 'Kim Hyuk-kyu', movieCount: 144, followerCount: 9500 },
		{ nickName: 'ralph', name: 'Moon HongJoo', movieCount: 12, followerCount: 31 },
		{ nickName: 'Faker', name: 'Lee Sanghyuk', movieCount: 106, followerCount: 2300 },
		{ nickName: 'Zefa', name: 'Lee Jae-min', movieCount: 45, followerCount: 1500 },
		{ nickName: 'Canna', name: 'Kim Chang-dong', movieCount: 67, followerCount: 2100 },
		{ nickName: 'Teddy', name: 'Park Jin-sung', movieCount: 99, followerCount: 5000 },
		{ nickName: 'Khan', name: 'Kim Dong-ha', movieCount: 54, followerCount: 1200 },
		{ nickName: 'Showmaker', name: 'Heo Su', movieCount: 76, followerCount: 3400 },
		{ nickName: 'Nuguri', name: 'Jang Ha-gwon', movieCount: 43, followerCount: 2100 },
		{ nickName: 'Ruler', name: 'Park Jae-hyuk', movieCount: 132, followerCount: 7100 },
		{ nickName: 'Chovy', name: 'Jeong Ji-hoon', movieCount: 120, followerCount: 8200 },
		{ nickName: 'Deft', name: 'Kim Hyuk-kyu', movieCount: 144, followerCount: 9500 },
		{ nickName: 'ralph', name: 'Moon HongJoo', movieCount: 12, followerCount: 31 },
		{ nickName: 'Faker', name: 'Lee Sanghyuk', movieCount: 106, followerCount: 2300 },
		{ nickName: 'Zefa', name: 'Lee Jae-min', movieCount: 45, followerCount: 1500 },
		{ nickName: 'Canna', name: 'Kim Chang-dong', movieCount: 67, followerCount: 2100 },
		{ nickName: 'Teddy', name: 'Park Jin-sung', movieCount: 99, followerCount: 5000 },
		{ nickName: 'Khan', name: 'Kim Dong-ha', movieCount: 54, followerCount: 1200 },
		{ nickName: 'Showmaker', name: 'Heo Su', movieCount: 76, followerCount: 3400 },
		{ nickName: 'Nuguri', name: 'Jang Ha-gwon', movieCount: 43, followerCount: 2100 },
		{ nickName: 'Ruler', name: 'Park Jae-hyuk', movieCount: 132, followerCount: 7100 },
		{ nickName: 'Chovy', name: 'Jeong Ji-hoon', movieCount: 120, followerCount: 8200 },
		{ nickName: 'Deft', name: 'Kim Hyuk-kyu', movieCount: 144, followerCount: 9500 }
		// ... 더 많은 유저 데이터
	];

	let currentPage = 1;
	const itemsPerPage = 5;
	const totalPages = Math.ceil(users.length / itemsPerPage);

	// $: pages = Array<number>(itemsPerPage)
	// 	.fill(0)
	// 	.map((_, i) => {
	// 		return currentPage + i;
	// 	});

	let currentPageUsers: User[] = getCurrentPageUsers();
	let pageNumbers: number[] = [1, 2, 3, 4, 5];

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
		const maxPagesToShow = 5;

		let startPage = Math.max(1, currentPage - Math.floor(maxPagesToShow / 2));
		let endPage = startPage + maxPagesToShow - 1;

		if (endPage > totalPages) {
			endPage = totalPages;
			startPage = Math.max(1, endPage - maxPagesToShow + 1);
		}

		// 마지막 페이지 클릭 시 페이지 번호 조정
		if (currentPage >= totalPages - 1) {
			startPage = Math.max(1, totalPages - maxPagesToShow + 1);
			endPage = totalPages;
		}

		for (let i = startPage; i <= endPage; i++) {
			pageNumbers[i - startPage] = i;
		}

		console.log('총 페이지:', totalPages);
		console.log('생성된 페이지 번호:', pageNumbers); // 추가된 로그
	}

	currentPageUsers = getCurrentPageUsers();
</script>

<h1>유저 관리</h1>
<div style="margin-left: 200px;">{JSON.stringify(params)}</div>

<div class="user_wrap">
	<div class="list_head tr">
		<div class="td">닉네임</div>
		<div class="td">이름</div>
		<div class="td">동영상</div>
		<div class="td">팔로워</div>
	</div>

	<div class="list_wrap">
		{#each currentPageUsers as user}
			<div class="user_list tr">
				<div class="user_nickname td">{user.nickName}</div>
				<div class="user_name td">{user.name}</div>
				<div class="user_movie td">{user.movieCount}</div>
				<div class="user_follower td">{formatCount(user.followerCount)}</div>
			</div>
		{/each}
	</div>

	<!-- 페이징 버튼 -->
	<div class="pagination">
		<button on:click={() => changePage(currentPage - 1)} disabled={currentPage === 1}>
			이전
		</button>

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

		<button on:click={() => changePage(currentPage + 1)} disabled={currentPage === totalPages}>
			다음
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
		min-width: 120px;
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
