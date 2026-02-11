<script>
	export let displayedText = '';
</script>

<div class="left-content">
	<div class="badge-container">
		<div class="status-badge">
			<span class="dot"></span>
			<span class="typing-text">{displayedText}<span class="cursor">|</span></span>
		</div>
		<p class="badge-note">*This website was made using SvelteKit</p>
	</div>
	<h1 class="title">
		Full Stack Developer.<br />
		Global Traveler.<br />
		Lifelong Entrepreneur.
	</h1>
</div>

<style>
	.left-content {
		position: absolute;
		left: 60px;
		top: 50%;
		transform: translateY(-50%);
		z-index: 2;
	}

	.badge-container {
		display: flex;
		flex-direction: column;
		gap: 8px;
		margin-bottom: 32px;
		animation: slideUpFadeIn 0.8s ease-out 0.2s both;
	}

	.status-badge {
		display: inline-flex;
		align-items: center;
		gap: 8px;
		background-color: rgba(255, 255, 255, 0.95);
		padding: 8px 16px;
		border-radius: 24px;
		font-size: 14px;
		color: #4a8aa8;
		width: fit-content;
		transition: all 0.15s ease-out;
	}

	.typing-text {
		display: inline-block;
		white-space: nowrap;
	}

	.cursor {
		display: inline-block;
		margin-left: 2px;
		animation: blink 1s step-end infinite;
		color: #4a8aa8;
	}

	.badge-note {
		font-size: 11px;
		color: rgba(255, 255, 255, 0.7);
		margin: 0;
		padding-left: 4px;
		font-style: italic;
		text-shadow: 0 1px 4px rgba(26, 61, 82, 0.2);
	}

	.dot {
		width: 8px;
		height: 8px;
		border-radius: 50%;
		background-color: #4a8aa8;
	}

	.title {
		font-size: 52px;
		font-weight: 700;
		color: #ffffff;
		line-height: 1.1;
		margin: 0;
		text-shadow: 0 2px 8px rgba(26, 61, 82, 0.3);
		animation: slideUpFadeIn 0.8s ease-out 0.2s both;
	}

	@keyframes slideUpFadeIn {
		from {
			opacity: 0;
			transform: translateY(40px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	@keyframes blink {
		0%, 49% {
			opacity: 1;
		}
		50%, 100% {
			opacity: 0;
		}
	}

	@media (max-width: 1400px) {
		.title {
			font-size: 41px;
		}
	}

	@media (max-width: 1024px) {
		.title {
			font-size: 30px;
		}
	}

	@media (max-width: 768px) {
		.left-content {
			left: 30px;
			top: 10%;
			transform: translateY(0);
		}

		.title {
			font-size: 24px;
		}
	}

	@media (max-width: 480px) {
		.title {
			font-size: 18px;
		}

		.status-badge {
			font-size: 12px;
			padding: 6px 12px;
		}
	}
</style>
