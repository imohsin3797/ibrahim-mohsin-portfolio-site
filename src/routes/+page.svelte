<script>
	import { onMount } from 'svelte';

	const heroImage = '/Ibrahim_Headshot.png';
	let expanded = false;

	function toggleNav() {
		expanded = !expanded;
	}

	// Typing animation
	const titles = [
		"Morehead-Cain Scholar",
		"Lifter",
		"Founder",
		"NUS Exchange",
		"UI Designer",
		"Tech Consultant",
		"Golfer",
		"Phonk Enthusiast",
		"Freelance Developer"
	];

	let currentTitleIndex = 0;
	let displayedText = '';
	let isDeleting = false;
	let typingSpeed = 100;

	onMount(() => {
		let timeout;

		function type() {
			const currentTitle = titles[currentTitleIndex];

			if (isDeleting) {
				displayedText = currentTitle.substring(0, displayedText.length - 1);
				typingSpeed = 50;
			} else {
				displayedText = currentTitle.substring(0, displayedText.length + 1);
				typingSpeed = 100;
			}

			if (!isDeleting && displayedText === currentTitle) {
				// Pause at end of word
				typingSpeed = 2000;
				isDeleting = true;
			} else if (isDeleting && displayedText === '') {
				isDeleting = false;
				currentTitleIndex = (currentTitleIndex + 1) % titles.length;
				typingSpeed = 500;
			}

			timeout = setTimeout(type, typingSpeed);
		}

		type();

		return () => clearTimeout(timeout);
	});
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
				<a href="#projects" class="nav-link">Projects</a>
				<a href="#contact" class="nav-link">Contact</a>
			</nav>
		</div>
	</div>
</header>

<div class="hero">
	<div class="container">
		<!-- Left side content -->
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

		<!-- Center image -->
		<div class="hero-image">
			<img src={heroImage} alt="Ibrahim" />
		</div>

		<!-- Right side content -->
		<div class="right-content">
			<p class="description">
				Hi, I'm Ibrahim Mohsin – a full stack<br />
				developer and designer passionate about<br />
				building innovative solutions and<br />
				beautiful user experiences.
			</p>
			<button class="cta-button">
				<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
					<path d="M5 12H19M19 12L12 5M19 12L12 19" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
				</svg>
				See my works
			</button>
			<div class="social-icons">
				<a href="https://x.com/IbrahimMohsin_" target="_blank" rel="noopener noreferrer" class="social-icon" aria-label="X (Twitter)">
					<svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
						<path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
					</svg>
				</a>
				<a href="https://www.linkedin.com/in/ibrahim-mohsin-16a1b8261/" target="_blank" rel="noopener noreferrer" class="social-icon" aria-label="LinkedIn">
					<svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
						<path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
					</svg>
				</a>
				<a href="https://github.com/imohsin3797" target="_blank" rel="noopener noreferrer" class="social-icon" aria-label="GitHub">
					<svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
						<path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.82-.26.82-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
					</svg>
				</a>
			</div>
		</div>

		<!-- Large name overlay -->
		<div class="name-overlay">
			<h2>Ibrahim</h2>
		</div>
	</div>
</div>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
		font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
	}

	/* Header with liquid glass effect */
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
	}

	.menu-container.expanded {
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

	.hero {
		min-height: 100vh;
		background: linear-gradient(180deg, #e8f4f8 0%, #b8d8e8 25%, #6ba3c0 75%, #4a8aa8 100%);
		position: relative;
		overflow: hidden;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.container {
		position: relative;
		width: 100%;
		max-width: 1400px;
		height: 100vh;
		margin: 0 auto;
		padding: 0 60px;
	}

	/* Left content */
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

	/* Center image */
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
	}

	.hero-image img {
		width: 100%;
		height: auto;
		display: block;
		object-fit: contain;
	}

	/* Right content */
	.right-content {
		position: absolute;
		right: 100px;
		top: 50%;
		transform: translateY(-50%);
		z-index: 2;
		text-align: left;
	}

	.description {
		font-size: 16px;
		font-weight: 600;
		line-height: 1.6;
		color: #ffffff;
		margin: 0 0 32px 0;
		animation: slideUpFadeIn 0.8s ease-out 0.2s both;
		text-shadow: 0 2px 8px rgba(26, 61, 82, 0.3);
	}

	.cta-button {
		display: inline-flex;
		align-items: center;
		gap: 12px;
		background-color: #ffffff;
		color: #4a8aa8;
		font-size: 16px;
		font-weight: 600;
		padding: 16px 32px;
		border-radius: 48px;
		border: 2px solid #ffffff;
		cursor: pointer;
		transition: transform 0.2s, box-shadow 0.2s, background-color 0.2s, color 0.2s;
		animation: slideUpFadeIn 0.8s ease-out 0.2s both;
	}

	.cta-button:hover {
		transform: translateY(-2px);
		background-color: rgba(255, 255, 255, 0.9);
		box-shadow: 0 8px 24px rgba(255, 255, 255, 0.3);
	}

	.cta-button svg {
		width: 20px;
		height: 20px;
	}

	.social-icons {
		display: flex;
		gap: 16px;
		margin-top: 24px;
		align-items: center;
		animation: slideUpFadeIn 0.8s ease-out 0.2s both;
	}

	.social-icon {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 40px;
		height: 40px;
		color: #ffffff;
		transition: all 0.3s ease;
		border-radius: 50%;
		background: rgba(255, 255, 255, 0.1);
		backdrop-filter: blur(10px);
		-webkit-backdrop-filter: blur(10px);
	}

	.social-icon:hover {
		transform: translateY(-3px) scale(1.1);
		background: rgba(255, 255, 255, 0.2);
		color: #ffffff;
	}

	.social-icon svg {
		width: 20px;
		height: 20px;
	}

	/* Large name overlay */
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

	/* Animations */
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

	@keyframes typing {
		from {
			width: 0;
		}
		to {
			width: 100%;
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

	/* Responsive adjustments */
	@media (max-width: 1400px) {
		.title {
			font-size: 41px;
		}

		.name-overlay h2 {
			font-size: 170px;
		}

		.hero-image {
			max-width: 500px;
		}
	}

	@media (max-width: 1024px) {
		.title {
			font-size: 30px;
		}

		.hero-image {
			max-width: 450px;
		}

		.name-overlay h2 {
			font-size: 140px;
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

		.container {
			padding: 0 30px;
		}

		.left-content {
			left: 30px;
			top: 10%;
			transform: translateY(0);
		}

		.right-content {
			right: 40px;
			top: auto;
			bottom: 150px;
			transform: translateY(0);
		}

		.title {
			font-size: 24px;
		}

		.description {
			font-size: 14px;
		}

		.name-overlay h2 {
			font-size: 80px;
		}

		.hero-image {
			max-width: 350px;
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

		.title {
			font-size: 18px;
		}

		.name-overlay h2 {
			font-size: 60px;
		}

		.hero-image {
			max-width: 280px;
		}

		.status-badge {
			font-size: 12px;
			padding: 6px 12px;
		}

		.description {
			font-size: 13px;
		}
	}
</style>
