<script>
	export let expanded = false;
	export let toggleNav;
</script>

<header class="header">
	<div class="header-container">
		<div class="menu-container" class:expanded={expanded}>
			<span class="logo-text">IM</span>
			<span class="name-text">Ibrahim</span>
			<button class="menu-toggle" on:click={toggleNav} aria-label="Toggle navigation">
				<div class="hamburger-icon">
					<span></span>
					<span></span>
					<span></span>
				</div>
			</button>
			<nav class="nav" class:expanded={expanded}>
				<a href="#home" class="nav-link">Home</a>
				<a href="#about" class="nav-link">About</a>
				<a href="#blog" class="nav-link">Blog</a>
				<a href="#experience" class="nav-link">Experience</a>
				<a href="#contact" class="nav-link">Contact</a>
			</nav>
		</div>
	</div>
</header>

<style>
	.header {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		z-index: 1000;
		padding: 20px 60px;
		background: transparent;
		backdrop-filter: blur(0px);
		-webkit-backdrop-filter: blur(0px);
		border-bottom: none;
		box-shadow: none;
		animation: slideDownFadeIn 0.6s ease-out;
	}

	.header-container {
		max-width: 1400px;
		margin: 0 auto;
		display: flex;
		align-items: center;
		gap: 16px;
	}

	.logo-text {
		font-size: 20px;
		font-weight: 700;
		color: #1e3a5f;
		letter-spacing: 2px;
		text-shadow: 0 2px 8px rgba(255, 255, 255, 0.3);
		flex-shrink: 0;
		margin-right: 6px;
	}

	.name-text {
		font-size: 16px;
		font-weight: 600;
		color: #1e3a5f;
		text-shadow: 0 2px 8px rgba(255, 255, 255, 0.3);
		white-space: nowrap;
		margin-right: 0;
		flex-shrink: 0;
	}

	.menu-container {
		display: flex;
		align-items: center;
		justify-content: space-between;
		background: rgba(255, 255, 255, 0.15);
		backdrop-filter: blur(20px) saturate(180%);
		-webkit-backdrop-filter: blur(20px) saturate(180%);
		border: 1px solid rgba(255, 255, 255, 0.2);
		border-radius: 50px;
		padding: 10px 16px;
		transition: all 0.4s ease;
		box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
		overflow: hidden;
		max-width: 160px;
		min-width: 160px;
		gap: 8px;
	}

	.menu-container.expanded {
		max-width: 600px;
		min-width: auto;
		justify-content: flex-start;
		padding: 8px 20px;
		gap: 0;
	}

	.menu-container.expanded .logo-text {
		margin-right: 6px;
	}

	.menu-container.expanded .name-text {
		margin-right: 12px;
	}

	.menu-container:hover {
		background: rgba(255, 255, 255, 0.2);
	}

	.menu-toggle {
		background: none;
		border: none;
		padding: 0;
		cursor: pointer;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: transform 0.3s ease;
		flex-shrink: 0;
		margin: 0 auto;
	}

	.menu-container.expanded .menu-toggle {
		margin: 0;
	}

	.menu-toggle:hover {
		transform: scale(1.05);
	}

	.menu-toggle:active {
		transform: scale(0.95);
	}

	.hamburger-icon {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		width: 20px;
		height: 16px;
		position: relative;
	}

	.hamburger-icon span {
		display: block;
		height: 2px;
		width: 100%;
		background: #1e3a5f;
		border-radius: 2px;
		transition: all 0.3s ease;
		transform-origin: center;
	}

	.menu-container.expanded .hamburger-icon span:nth-child(1) {
		transform: translateY(7px) rotate(45deg);
	}

	.menu-container.expanded .hamburger-icon span:nth-child(2) {
		opacity: 0;
		transform: translateX(-10px);
	}

	.menu-container.expanded .hamburger-icon span:nth-child(3) {
		transform: translateY(-7px) rotate(-45deg);
	}

	.nav {
		display: flex;
		gap: 0;
		align-items: center;
		overflow: hidden;
		width: 0;
		opacity: 0;
		transform: translateX(-10px);
		transition: width 0.4s ease, opacity 0.4s ease, transform 0.4s ease;
		margin-left: 12px;
	}

	.nav.expanded {
		width: auto;
		opacity: 1;
		transform: translateX(0);
	}

	.nav-link {
		color: #1e3a5f;
		text-decoration: none;
		font-size: 16px;
		font-weight: 500;
		transition: all 0.3s ease;
		position: relative;
		padding: 8px 16px;
		text-shadow: 0 2px 8px rgba(255, 255, 255, 0.3);
		white-space: nowrap;
		opacity: 0;
		transform: translateX(-10px);
		transition: opacity 0.3s ease 0.2s, transform 0.3s ease 0.2s;
	}

	.nav.expanded .nav-link {
		opacity: 1;
		transform: translateX(0);
	}

	.nav-link::after {
		content: '';
		position: absolute;
		bottom: 0;
		left: 0;
		width: 0;
		height: 2px;
		background: #1e3a5f;
		transition: width 0.3s ease;
		box-shadow: 0 2px 4px rgba(30, 58, 95, 0.3);
	}

	.nav-link:hover {
		transform: translateY(-2px);
	}

	.nav-link:hover::after {
		width: 100%;
	}

	@keyframes slideDownFadeIn {
		from {
			opacity: 0;
			transform: translateY(-20px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	@media (max-width: 768px) {
		.header {
			padding: 16px 30px;
		}

		.nav {
			gap: 20px;
		}

		.nav-link {
			font-size: 14px;
		}

		.logo-text {
			font-size: 20px;
		}
	}

	@media (max-width: 480px) {
		.header {
			padding: 12px 20px;
		}

		.nav {
			gap: 16px;
		}

		.nav-link {
			font-size: 13px;
		}

		.logo-text {
			font-size: 18px;
		}
	}
</style>
