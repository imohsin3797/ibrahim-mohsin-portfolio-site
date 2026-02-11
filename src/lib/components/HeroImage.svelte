<script>
	export let heroImage = '';
</script>

<div class="hero-image">
	<img src={heroImage} alt="Ibrahim" />
</div>

<style>
	.hero-image {
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		z-index: 1;
		max-width: 600px;
		max-height: 80vh;
		animation: slideUpFadeInCenter 0.8s ease-out 0.2s both;
		pointer-events: none;
		-webkit-mask-image: linear-gradient(to bottom, black 0%, black 90%, transparent 100%);
		mask-image: linear-gradient(to bottom, black 0%, black 90%, transparent 100%);
	}

	.hero-image img {
		width: 100%;
		height: auto;
		display: block;
		object-fit: contain;
	}

	@keyframes slideUpFadeInCenter {
		from {
			opacity: 0;
			transform: translate(-50%, calc(-50% + 40px));
		}
		to {
			opacity: 1;
			transform: translate(-50%, -50%);
		}
	}

	@media (max-width: 1400px) {
		.hero-image {
			max-width: 500px;
		}
	}

	@media (max-width: 1024px) {
		.hero-image {
			max-width: 450px;
		}
	}

	@media (max-width: 768px) {
		.hero-image {
			max-width: 350px;
		}
	}

	@media (max-width: 480px) {
		.hero-image {
			max-width: 280px;
		}
	}
</style>
