<script>
	// let count = 0;

	const counting = [
		{ label: '총 방문자 수', count: 12450 },
		{ label: '하루 방문자 수', count: 450 },
		{ label: '총 회원 수', count: 3200 },
		{ label: '총 동영상 수', count: 125 },
		{ label: '총 광고 수', count: 50 }
	];
</script>

<h1>대시보드</h1>

<div class="counting_wrap">
	{#each counting as data}
		<div class="counting_box">
			<p>{data.label}</p>
			<span>{data.count.toLocaleString()}</span>
		</div>
	{/each}
</div>

<style>
	h1 {
		padding: 20px 0;
		margin-left: 200px;
	}

	.counting_wrap {
		max-width: 800px;
		margin: auto; /* 양쪽에 150px의 여백을 주어 가운데 정렬 */
		display: flex;
		flex-wrap: wrap;
		align-items: center;
		justify-content: space-between;
		gap: 15px 5px;
	}

	.counting_box {
		/* min-width: 200px; */
		max-width: 250px;
		width: 100%;
		background-color: #8b93c9;
		aspect-ratio: 1/1;
		border-radius: 10px;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		color: white;
		font-size: 16px;
		font-weight: 600;
	}

	.counting_box span {
		font-size: 28px;
	}

	.counting_box:nth-child(1),
	.counting_box:nth-child(2) {
		max-width: 390px;
		width: 100%;
		aspect-ratio: 3/2;
		border-radius: 10px;
	}

	/* 800px + 400px(한쪽200px마진이라) */
	@media (max-width: 1200px) {
		.counting_wrap {
			margin-left: 200px;
		}
	}

	@media (max-width: 1050px) {
		:global(.sidebar) {
			display: none !important;
		}

		h1 {
			margin: auto;
			width: fit-content;
		}

		.counting_wrap {
			margin: auto;
			padding: 0 5px;
			/* justify-content: center; */
			/* gap: 0px; */
		}
	}
</style>
