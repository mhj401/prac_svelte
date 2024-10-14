<script>
	let count = 0;

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
	}

	.counting_wrap {
		max-width: 800px;
		margin: auto;
		display: flex;
		flex-wrap: wrap;
		align-items: center;
		justify-content: space-between;
		gap: 15px 0px;
	}

	.counting_box {
		min-width: 200px;
		max-width: 250px;
		width: 100%;
		background-color: rgb(70, 70, 70);
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
</style>
