<div class="name-overlay">
	<h2>Ibrahim</h2>
</div>

<style>
	.name-overlay {
		position: absolute;
		left: 50%;
		bottom: 6%;
		transform: translateX(-50%);
		z-index: 2;
		pointer-events: none;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.name-overlay h2 {
		font-size: 240px;
		font-weight: 900;
		color: #ffffff;
		margin: 0;
		line-height: 1;
		letter-spacing: -0.02em;
		white-space: nowrap;
		text-transform: lowercase;
		text-shadow: 0 6px 24px rgba(26, 61, 82, 0.6), 0 2px 8px rgba(26, 61, 82, 0.4);
		animation: slideUpFadeIn 0.8s ease-out 0.7s both;
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

	@media (max-width: 1400px) {
		.name-overlay h2 {
			font-size: 170px;
		}
	}

	@media (max-width: 1024px) {
		.name-overlay h2 {
			font-size: 140px;
		}
	}

	@media (max-width: 768px) {
		.name-overlay h2 {
			font-size: 80px;
		}
	}

	@media (max-width: 480px) {
		.name-overlay h2 {
			font-size: 60px;
		}
	}
</style>
