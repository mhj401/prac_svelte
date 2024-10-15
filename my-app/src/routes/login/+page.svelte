<script lang="ts">
	let inputValue = '';
	let passwordValue = '';

	function handleInvalid(event: Event) {
		const target = event.target as HTMLInputElement;
		const { type } = target;

		switch (type) {
			case 'text':
				target.setCustomValidity('아이디를 입력하세요');
				break;
			case 'password':
				target.setCustomValidity('비밀번호를 입력하세요');
				break;
			default:
				target.setCustomValidity('이 필드를 확인하세요');
		}
	}

	// 입력할 때 메시지를 초기화하는 함수
	function handleInput(event: Event) {
		const target = event.target as HTMLInputElement;
		target.setCustomValidity('');
	}
</script>

<div class="login_wrap">
	<img class="logo_img" src="/img/logo_white.png" alt="heradee logo" />
	<form class="login_form">
		<div>
			<input
				class="id_input"
				type="text"
				bind:value={inputValue}
				required
				on:invalid={handleInvalid}
				on:input={handleInput}
				placeholder="아이디를 입력하세요"
			/>
		</div>
		<div>
			<input
				class="pw_input"
				type="password"
				bind:value={passwordValue}
				required
				on:invalid={handleInvalid}
				on:input={handleInput}
				placeholder="비밀번호를 입력하세요"
			/>
		</div>
		<button type="submit" class="login_btn" disabled> 로그인</button>
	</form>
</div>

<style>
	:global(body) {
		background-color: rgb(246, 246, 246);
	}

	.login_wrap {
		text-align: center;
		margin-top: 150px;
	}

	.logo_img {
		filter: invert(100%);
		width: 70px;
	}

	.login_form {
		max-width: 500px;
		width: 100%;
		margin: auto;
		display: flex;
		flex-direction: column;
		padding: 50px 30px;
	}

	input {
		width: 100%;
		display: inline-block;
		height: 60px;
		padding: 0px 5px;
		border: 1px solid rgb(150, 150, 150);
	}

	.login_form div:first-child input {
		border-bottom: 0px;
	}

	button {
		width: 100%;
		border: none;
		height: 65px;
		/* border-radius: 8px; */
		color: white;
		font-size: 18px;
		background-color: #8b93c9;
		margin-top: 20px;
		cursor: pointer;
	}

	button:disabled {
		background-color: rgb(160, 160, 160);
	}
</style>
