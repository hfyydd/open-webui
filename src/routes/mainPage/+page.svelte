<script>
	import { goto } from '$app/navigation';
	import { fly } from 'svelte/transition';
	import { onMount } from 'svelte';

	function handleKeydown(event) {
		if (event.key === 'Enter') {
			goto('/');
		}
	}
	const cards = [
		{
			imgSrc: 'image1.jpg',
			text: 'AI法律专家',
			text2: '与12348公共法律中心坐席律师配合\n打造“AI+律师”模式'
		},
		{ imgSrc: 'image2.jpg', text: '文书生成', text2: '智能生成公共法律服务各类文书' },
		{ imgSrc: 'image3.jpg', text: 'Agent智能体', text2: '自动实现各类业务流程' }
	];
</script>

<!-- <div 
    on:click={() => goto('/')} 
    on:keydown={handleKeydown}  -->
<div class="video-background custom-background">
	<video playsinline="playsinline" autoplay="autoplay" muted="muted" loop="loop">
		<source src="/assets/background.mp4" type="video/mp4" />
	</video>
	<div class="content">
		<div
			role="button"
			tabindex="0"
			class="bg-cover min-h-screen w-full flex flex-col justify-center font-mona"
			in:fly={{ y: -1000, duration: 1000 }}
			out:fly={{ y: -1000, duration: 1000 }}
		>
			<div class="flex flex-col items-center space-y-5 mt-20">
				<div class="centered-text">黑龙江省公共法律服务<br>大模型</div>
				<div
					class="absolute bottom-20 left-1/2 transform -translate-x-1/2 text-center text-lg text-white"
				>
					黑龙江省司法厅技术团队
				</div>
				<div style="height: 3vh;"></div>
				<div class="cards-container flex justify-center space-x-5">
					{#each cards as { imgSrc, text, text2 }}
						<div
							class="card w-72 border border-gray-300 rounded overflow-hidden m-2 text-center"
							on:click={() => {
								if (text === 'AI法律专家') {
									goto('/');
								} else if (text === '文书生成') {
									goto('/playground');
								} else {
									goto('/playground2');
								}
							}}
						>
							<img class="w-full h-48 object-cover" src={imgSrc} alt="Card image" />
							<p class="p-2 text-white">{text}</p>
							<p class="p-2 text-white">{text2}</p>
						</div>
					{/each}
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	.centered-text {
		position: absolute; /* 绝对定位 */
		top: 25%; /* 顶部偏移50% */
		left: 50%; /* 左侧偏移50% */
		transform: translate(-50%, -50%); /* 用于居中 */
		transition: transform 0.5s ease-in-out;
		text-align: center; /* 字体居中 */
		font-size: 4em; /* 字体大小 */
		font-weight: bold; /* 字体粗细 */
		background: linear-gradient(105deg, #d16ba5, #86a8e7, #5ffbf1, #86a8e7, #d16ba5); /* 渐变色 */
		background-size: 200% 200%;
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		animation: gradient 3s ease infinite;
	}
	.video-background {
		position: relative;
		width: 100%;
		height: 100%;
		overflow: hidden;
	}

	.video-background video {
		position: absolute;
		top: 50%;
		left: 50%;
		min-width: 100%;
		min-height: 100%;
		width: auto;
		height: auto;
		z-index: 0;
		transform: translate(-50%, -50%);
        object-fit: cover; 
	}

	.content {
		position: relative;
		z-index: 1;
	}

	@keyframes gradient {
		0% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
		100% {
			background-position: 0% 50%;
		}
	}
</style>
