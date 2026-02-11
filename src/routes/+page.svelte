<script>
	import { onMount } from 'svelte';
	import Header from '$lib/components/Header.svelte';
	import HeroLeft from '$lib/components/HeroLeft.svelte';
	import HeroImage from '$lib/components/HeroImage.svelte';
	import HeroRight from '$lib/components/HeroRight.svelte';
	import NameOverlay from '$lib/components/NameOverlay.svelte';

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
		"Freelance Developer",
		"Lake Superior Kayaker"
	];

	const randomThings = [
		"Kayaked 90 miles across Lake Superior",
		"Lived and studied in Singapore for a semester",
		"Benched 250+ pounds",
		"Coded for 30 hours straight",
		"Taught 15 middle schoolers robotics programming",
		"Funded my high school's first vending machine",
		"Traveled to 50+ countries",
		"Built AI for aging populations in Western NC",
		"Scaled a 200 meter vertical cliff in slides",
		"Researched and debated wealth inequality in America for 2 years",
		"Built AI-powered poker glasses",
		"Drove a solar-powered car across UNC's Campus",
		"Founded a protein ice cream business, selling to 300+ customers",
		"Acted in a commercial for my mobile startup",
		"Dropshipped biometric bike locks",
		"Snorkled with sharks in open water",
		"Hit my first birdy on a 220 yard par 3",
		"Learned beatmaking and made my own in a week"
	];

	let currentTitleIndex = 0;
	let displayedText = '';
	let isDeleting = false;
	let typingSpeed = 100;
	let visibleCards = [false, false, false, false, false];
	let blogSectionVisible = false;

	// Newsletter state
	let email = '';
	let isSubmitting = false;
	let isSubscribed = false;

	// Contact title typing animation
	const contactTitleFull = "Let's Connect";
	let contactTitleText = '';
	let contactTitleVisible = false;
	let contactTitleTypingDone = false;

	function handleSubscribe(event) {
		event.preventDefault();
		if (!email || isSubmitting) return;

		isSubmitting = true;

		// Simulate API call
		setTimeout(() => {
			isSubmitting = false;
			isSubscribed = true;
			email = '';

			// Reset after showing success
			setTimeout(() => {
				isSubscribed = false;
			}, 4000);
		}, 1500);
	}

	onMount(() => {
		let timeout = null;
		let contactTypingTimeout = null;
		let contactObserverRef = null;

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

		// Intersection Observer for image cards
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						const element = entry.target;
						const indexAttr = element.getAttribute('data-index');
						const cardIndex = indexAttr ? parseInt(indexAttr) : 0;
						if (!visibleCards[cardIndex]) {
							visibleCards[cardIndex] = true;
							visibleCards = visibleCards; // trigger reactivity
						}
					}
				});
			},
			{
				threshold: 0.2,
				rootMargin: '0px 0px -50px 0px'
			}
		);

		// Observe all image wrappers after a short delay to ensure DOM is ready
		setTimeout(() => {
			const imageWrappers = document.querySelectorAll('.image-wrapper');
			imageWrappers.forEach((wrapper) => {
				observer.observe(wrapper);
			});

			// Observe blog section
			const blogSection = document.querySelector('.blog-section');
			if (blogSection) {
				const blogObserver = new IntersectionObserver(
					(entries) => {
						entries.forEach((entry) => {
							if (entry.isIntersecting) {
								blogSectionVisible = true;
							}
						});
					},
					{
						threshold: 0.2,
						rootMargin: '0px 0px -50px 0px'
					}
				);
				blogObserver.observe(blogSection);
			}

			// Observe contact section for typing animation
			const contactSection = document.querySelector('.contact-section');
			if (contactSection) {
				contactObserverRef = new IntersectionObserver(
					(entries) => {
						entries.forEach((entry) => {
							if (entry.isIntersecting && !contactTitleTypingDone) {
								contactTitleVisible = true;
								contactTitleTypingDone = true;
								let index = 0;
								function typeContactTitle() {
									if (index <= contactTitleFull.length) {
										contactTitleText = contactTitleFull.substring(0, index);
										index++;
										contactTypingTimeout = setTimeout(typeContactTitle, 80);
									}
								}
								typeContactTitle();
							}
						});
					},
					{ threshold: 0.2, rootMargin: '0px 0px -50px 0px' }
				);
				contactObserverRef.observe(contactSection);
			}

		}, 100);

		return () => {
			if (timeout) clearTimeout(timeout);
			if (contactTypingTimeout) clearTimeout(contactTypingTimeout);
			observer.disconnect();
			if (contactObserverRef) contactObserverRef.disconnect();
		};
	});
</script>

<Header {expanded} {toggleNav} />

<div class="hero">
	<div class="container">
		<HeroLeft {displayedText} />
		<HeroImage {heroImage} />
		<HeroRight />
		<NameOverlay />
	</div>

	<div class="image-gallery">
		{#each [1, 2, 3, 4, 5] as num, i}
			<div 
				class="image-wrapper" 
				class:tilt-left={i % 2 === 0} 
				class:tilt-right={i % 2 === 1} 
				class:image-3={i === 2} 
				class:image-4={i === 3}
				class:visible={visibleCards[i]}
				data-index={i}
			>
				<img src={num === 2 ? '/image-2.jpeg' : `/image-${num}.jpg`} alt="Gallery image {num}" />
			</div>
		{/each}
	</div>

	<div class="wave-divider">
		<svg viewBox="0 0 1440 120" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
			<path
				class="wave-shadow"
				d="M0,60 C360,120 1080,0 1440,60 L1440,120 L0,120 Z"
			/>
			<path
				class="wave-fill"
				d="M0,60 C360,120 1080,0 1440,60 L1440,120 L0,120 Z"
			/>
		</svg>
	</div>
</div>

<section class="about-section">
	<div class="about-container">
		<div class="about-content">
			<div class="about-text">
				<h2 class="about-title">About Me</h2>
				<p class="about-body">
					I'm a Morehead-Cain Scholar at UNC Chapel Hill with a passion for building
					impactful technology solutions. From founding startups to consulting for
					enterprise clients, I thrive at the intersection of innovation and execution.
				</p>
				<p class="about-body">
					When I'm not coding, you'll find me lifting weights, hitting the golf course,
					or exploring new places. I believe in continuous learning and pushing boundaries
					— whether that's kayaking across Lake Superior or diving into a new tech stack.
				</p>
			</div>
			<div class="about-image-wrapper">
				<img src="ibrahim-headshot-2.jpg" alt="Ibrahim" class="about-image" />
			</div>
		</div>
	</div>

	<div class="random-things">
		<h3 class="random-things-title">Some Random Things I've Done...</h3>
		<div class="carousel-container">
			<div class="carousel-track">
				{#each [...randomThings, ...randomThings] as item}
					<span class="carousel-item">{item}</span>
				{/each}
			</div>
		</div>
	</div>
</section>

<section class="content-section">
	<div class="blog-section" class:visible={blogSectionVisible}>
		<h2 class="blog-title">What I've Been Up To Recently...</h2>
		<p class="blog-subtitle">Read about my most recent work, project, trips, and stories</p>
		<a href="/blog" class="see-all-link">See All <span class="arrow">→</span></a>
		<div class="blog-cards">
			<article class="blog-card glass">
				<div class="card-image">
					<img src="/image-1.jpg" alt="Blog post 1" />
				</div>
				<div class="card-content">
					<h3 class="card-title">Building My Portfolio</h3>
					<p class="card-body">Exploring the latest web technologies and design trends while creating a personal space to showcase my work and journey.</p>
					<button class="read-more-btn">Read More</button>
				</div>
			</article>
			<article class="blog-card glass">
				<div class="card-image">
					<img src="/image-2.jpeg" alt="Blog post 2" />
				</div>
				<div class="card-content">
					<h3 class="card-title">NUS Exchange Experience</h3>
					<p class="card-body">Reflecting on my semester abroad at the National University of Singapore and the incredible experiences that shaped my perspective.</p>
					<button class="read-more-btn">Read More</button>
				</div>
			</article>
			<article class="blog-card glass">
				<div class="card-image">
					<img src="/image-3.jpg" alt="Blog post 3" />
				</div>
				<div class="card-content">
					<h3 class="card-title">Tech Consulting Insights</h3>
					<p class="card-body">Lessons learned from working with clients across various industries and helping them solve complex technical challenges.</p>
					<button class="read-more-btn">Read More</button>
				</div>
			</article>
		</div>

		<!-- Newsletter Subscription -->
		<div class="newsletter-section">
			<div class="newsletter-box glass">
				{#if isSubscribed}
					<div class="success-message">
						<div class="checkmark-circle">
							<svg class="checkmark" viewBox="0 0 52 52">
								<circle class="checkmark-bg" cx="26" cy="26" r="25" fill="none"/>
								<path class="checkmark-check" fill="none" d="M14.1 27.2l7.1 7.2 16.7-16.8"/>
							</svg>
						</div>
						<h3>You're In!</h3>
						<p>Thanks for subscribing. Stay tuned for updates!</p>
					</div>
				{:else}
					<h3 class="newsletter-title">Stay in the Loop</h3>
					<p class="newsletter-description">Subscribe to my newsletter and never miss a new post or update.</p>
					<form class="newsletter-form" on:submit={handleSubscribe}>
						<div class="input-wrapper">
							<input
								type="email"
								placeholder="Enter your email"
								bind:value={email}
								required
								disabled={isSubmitting}
							/>
							<button type="submit" class="subscribe-btn" disabled={isSubmitting}>
								{#if isSubmitting}
									<span class="spinner"></span>
								{:else}
									Subscribe
								{/if}
							</button>
						</div>
					</form>
				{/if}
			</div>
		</div>
	</div>
</section>

<section class="footer-section">
	<div class="wave-divider-bottom">
		<svg viewBox="0 0 1440 120" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
			<path
				class="wave-shadow-bottom"
				d="M0,60 C360,120 1080,0 1440,60 L1440,0 L0,0 Z"
			/>
			<path
				class="wave-fill-bottom"
				d="M0,60 C360,120 1080,0 1440,60 L1440,0 L0,0 Z"
			/>
		</svg>
	</div>
	<div class="journey-container">
		<h2 class="journey-title">The Journey So Far</h2>
		<p class="journey-subtitle">Milestones, experiences, and the path that brought me here</p>

		<div class="journey-grid">
			<!-- Left Column -->
			<div class="journey-column left-column">
				<div class="journey-card glass">
					<span class="card-icon">💼</span>
					<h3>Experience</h3>
					<div class="experience-item">
						<h4>Senior Tech Consultant</h4>
						<p class="company">Acme Corp • 2023 - Present</p>
						<p class="description">Leading digital transformation initiatives for Fortune 500 clients</p>
					</div>
					<div class="experience-item">
						<h4>Full Stack Developer</h4>
						<p class="company">StartupXYZ • 2021 - 2023</p>
						<p class="description">Built scalable web applications serving 100K+ users</p>
					</div>
					<div class="experience-item">
						<h4>Freelance Developer</h4>
						<p class="company">Self-Employed • 2020 - 2021</p>
						<p class="description">Delivered custom solutions for diverse clients</p>
					</div>
					<button class="cv-btn">See Full CV</button>
				</div>

				<div class="journey-card glass">
					<span class="card-icon">🎓</span>
					<h3>Education</h3>
					<div class="education-item">
						<h4>University of North Carolina at Chapel Hill</h4>
						<p class="degree">B.S. Computer Science • 2020 - 2024</p>
						<p class="honor">Morehead-Cain Scholar</p>
					</div>
					<div class="education-item">
						<h4>National University of Singapore</h4>
						<p class="degree">Exchange Student • Fall 2023</p>
						<p class="honor">Global Experience Program</p>
					</div>
				</div>
			</div>

			<!-- Right Column -->
			<div class="journey-column right-column">
				<div class="journey-card glass">
					<span class="card-icon">🚀</span>
					<h3>Currently Working on...</h3>
					<div class="project-item">
						<h4>AI-Powered Analytics Platform</h4>
						<p>Building next-gen data visualization tools for enterprise clients</p>
					</div>
					<div class="project-item">
						<h4>Open Source Contributions</h4>
						<p>Contributing to SvelteKit and related ecosystem projects</p>
					</div>
				</div>

				<div class="journey-card glass">
					<span class="card-icon">⭐</span>
					<h3>Notable Projects</h3>
					<div class="project-item">
						<h4>E-Commerce Platform</h4>
						<p>Full-stack marketplace with payment integration and real-time inventory</p>
					</div>
					<div class="project-item">
						<h4>Task Management SaaS</h4>
						<p>Collaborative project management tool with team analytics</p>
					</div>
					<div class="project-item">
						<h4>Mobile Fitness App</h4>
						<p>Cross-platform fitness tracker with AI-powered workout recommendations</p>
					</div>
				</div>

				<div class="journey-card glass">
					<span class="card-icon">✨</span>
					<h3>Skills + Interests</h3>
					<div class="skills-section">
						<div class="skill-group">
							<h4>Technical Skills</h4>
							<div class="skill-tags">
								<span class="skill-tag">JavaScript</span>
								<span class="skill-tag">TypeScript</span>
								<span class="skill-tag">React</span>
								<span class="skill-tag">Svelte</span>
								<span class="skill-tag">Node.js</span>
								<span class="skill-tag">Python</span>
								<span class="skill-tag">PostgreSQL</span>
							</div>
						</div>
						<div class="skill-group">
							<h4>Interests</h4>
							<p class="interests-text">🏋️ Weightlifting • ⛳ Golf • 🎵 Phonk Music • 🚣 Kayaking • 📚 Tech Blogs</p>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<section class="contact-section">
	<div class="wave-divider-contact">
		<svg viewBox="0 0 1440 120" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
			<path
				class="wave-shadow-contact"
				d="M0,60 C360,0 1080,120 1440,60 L1440,120 L0,120 Z"
			/>
			<path
				class="wave-fill-contact"
				d="M0,60 C360,0 1080,120 1440,60 L1440,120 L0,120 Z"
			/>
		</svg>
	</div>
	<div class="contact-container">
		<div class="contact-content">
			<div class="contact-left">
				<div class="contact-image-wrapper">
					<img src="/ibrahim-contact-headshot.JPG" alt="Ibrahim" class="contact-image" />
				</div>
			</div>
			<div class="contact-right">
				<h2 class="contact-title">{contactTitleText}<span class="typing-cursor" class:visible={contactTitleVisible}>|</span></h2>
				<p class="contact-description">
					I'm always open to discussing new opportunities, collaborations, or just having a conversation about tech, startups, or anything interesting. Feel free to reach out!
				</p>
				<div class="contact-info">
					<div class="contact-item">
						<svg class="contact-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
							<path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
							<polyline points="22,6 12,13 2,6"/>
						</svg>
						<a href="mailto:imohsin@unc.edu">imohsin@unc.edu</a>
					</div>
					<div class="contact-item">
						<svg class="contact-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
							<path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/>
							<circle cx="12" cy="10" r="3"/>
						</svg>
						<span>Singapore</span>
					</div>
				</div>
				<div class="social-links">
					<a href="https://linkedin.com/in/ibrahimmohsin" target="_blank" rel="noopener noreferrer" class="social-link" aria-label="LinkedIn">
						<svg viewBox="0 0 24 24" fill="currentColor">
							<path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
						</svg>
					</a>
					<a href="https://github.com/ibrahimmohsin" target="_blank" rel="noopener noreferrer" class="social-link" aria-label="GitHub">
						<svg viewBox="0 0 24 24" fill="currentColor">
							<path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
						</svg>
					</a>
					<a href="https://twitter.com/ibrahimmohsin" target="_blank" rel="noopener noreferrer" class="social-link" aria-label="Twitter">
						<svg viewBox="0 0 24 24" fill="currentColor">
							<path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
						</svg>
					</a>
				</div>
			</div>
		</div>
		<div class="contact-footer">
			<p>&copy; 2026 Ibrahim Mohsin. All rights reserved.</p>
		</div>
	</div>
</section>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
		font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
	}

	.hero {
		min-height: 100vh;
		background: linear-gradient(180deg, #e8f4f8 0%, #b8d8e8 15%, #6ba3c0 50%, #4a8aa8 75%, #3d7a96 100%);
		position: relative;
		overflow: visible;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding-bottom: 0;
	}

	.wave-divider {
		position: relative;
		width: 100%;
		margin-top: -1px;
		line-height: 0;
	}

	.wave-divider svg {
		width: 100%;
		height: 120px;
		display: block;
	}

	.wave-shadow {
		fill: none;
		stroke: rgba(0, 0, 0, 0.15);
		stroke-width: 3;
		filter: drop-shadow(0 -4px 8px rgba(0, 0, 0, 0.2));
		transform: translateY(-2px);
	}

	.wave-fill {
		fill: #e8f4f8;
	}

	.footer-section {
		background: #3d7a96;
		min-height: 200px;
		width: 100%;
		margin-top: -1px;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.wave-divider-bottom {
		width: 100%;
		line-height: 0;
	}

	.wave-divider-bottom svg {
		width: 100%;
		height: 120px;
		display: block;
	}

	.wave-shadow-bottom {
		fill: none;
		stroke: rgba(0, 0, 0, 0.15);
		stroke-width: 3;
		filter: drop-shadow(0 -4px 8px rgba(0, 0, 0, 0.2));
		transform: translateY(-2px);
	}

	.wave-fill-bottom {
		fill: #b8d8e8;
	}

	.journey-container {
		width: 100%;
		max-width: 1200px;
		padding: 60px 40px 80px 40px;
		box-sizing: border-box;
	}

	.journey-title {
		text-align: center;
		font-size: 3.5rem;
		font-weight: 700;
		color: #ffffff;
		margin: 0 0 16px 0;
		text-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
	}

	.journey-subtitle {
		text-align: center;
		font-size: 1.125rem;
		color: rgba(255, 255, 255, 0.9);
		margin: 0 0 50px 0;
		line-height: 1.6;
	}

	.journey-grid {
		display: flex;
		gap: 24px;
	}

	.journey-column {
		flex: 1;
		display: flex;
		flex-direction: column;
		gap: 24px;
	}

	.left-column .journey-card.glass {
		flex: 1;
	}

	.right-column .journey-card.glass {
		flex: 1;
	}

	.journey-card.glass {
		padding: 32px;
		border-radius: 20px;
		background: linear-gradient(
			135deg,
			rgba(255, 255, 255, 0.25) 0%,
			rgba(255, 255, 255, 0.1) 100%
		);
		backdrop-filter: blur(20px);
		-webkit-backdrop-filter: blur(20px);
		border: 1px solid rgba(255, 255, 255, 0.3);
		box-shadow:
			0 8px 32px rgba(0, 0, 0, 0.2),
			0 4px 16px rgba(0, 0, 0, 0.15),
			inset 0 1px 0 rgba(255, 255, 255, 0.4),
			inset 0 -1px 0 rgba(255, 255, 255, 0.1);
		transition: transform 0.3s ease, box-shadow 0.3s ease;
		display: flex;
		flex-direction: column;
	}

	.journey-card.glass:hover {
		transform: translateY(-6px);
		box-shadow:
			0 16px 48px rgba(0, 0, 0, 0.3),
			0 8px 24px rgba(0, 0, 0, 0.2),
			inset 0 1px 0 rgba(255, 255, 255, 0.5),
			inset 0 -1px 0 rgba(255, 255, 255, 0.2);
	}

	.journey-card .card-icon {
		font-size: 2.5rem;
		margin-bottom: 16px;
		display: block;
	}

	.journey-card h3 {
		font-size: 1.75rem;
		font-weight: 700;
		color: #ffffff;
		margin: 0 0 20px 0;
	}

	.journey-card h4 {
		font-size: 1.125rem;
		font-weight: 600;
		color: #ffffff;
		margin: 0 0 6px 0;
	}

	.journey-card p {
		font-size: 0.95rem;
		line-height: 1.6;
		color: rgba(255, 255, 255, 0.9);
		margin: 0;
	}

	/* Experience Card */
	.experience-item {
		margin-bottom: 24px;
	}

	.experience-item:last-of-type {
		margin-bottom: 0;
	}

	.experience-item .company {
		font-size: 0.875rem;
		color: rgba(255, 255, 255, 0.75);
		margin-bottom: 8px;
		font-weight: 500;
	}

	.experience-item .description {
		font-size: 0.9rem;
		color: rgba(255, 255, 255, 0.85);
	}

	.cv-btn {
		margin-top: 24px;
		padding: 12px 28px;
		font-size: 0.95rem;
		font-weight: 600;
		color: #ffffff;
		background: linear-gradient(135deg, rgba(255, 255, 255, 0.25) 0%, rgba(255, 255, 255, 0.15) 100%);
		border: 1px solid rgba(255, 255, 255, 0.4);
		border-radius: 30px;
		cursor: pointer;
		backdrop-filter: blur(10px);
		-webkit-backdrop-filter: blur(10px);
		box-shadow:
			0 4px 12px rgba(0, 0, 0, 0.15),
			inset 0 1px 0 rgba(255, 255, 255, 0.3);
		transition: all 0.3s ease;
		align-self: flex-start;
	}

	.cv-btn:hover {
		background: linear-gradient(135deg, rgba(255, 255, 255, 0.35) 0%, rgba(255, 255, 255, 0.25) 100%);
		box-shadow:
			0 6px 16px rgba(0, 0, 0, 0.2),
			inset 0 1px 0 rgba(255, 255, 255, 0.4);
		transform: translateY(-2px);
	}

	/* Education Card */
	.education-item {
		margin-bottom: 24px;
	}

	.education-item:last-child {
		margin-bottom: 0;
	}

	.education-item .degree {
		font-size: 0.875rem;
		color: rgba(255, 255, 255, 0.75);
		margin-bottom: 4px;
		font-weight: 500;
	}

	.education-item .honor {
		font-size: 0.875rem;
		color: rgba(255, 255, 255, 0.85);
		font-style: italic;
	}

	/* Project Items */
	.project-item {
		margin-bottom: 20px;
	}

	.project-item:last-child {
		margin-bottom: 0;
	}

	.project-item h4 {
		margin-bottom: 8px;
	}

	.project-item p {
		font-size: 0.9rem;
		color: rgba(255, 255, 255, 0.85);
	}

	/* Skills Section */
	.skills-section {
		display: flex;
		flex-direction: column;
		gap: 20px;
	}

	.skill-group h4 {
		margin-bottom: 12px;
		font-size: 1rem;
	}

	.skill-tags {
		display: flex;
		flex-wrap: wrap;
		gap: 8px;
	}

	.skill-tag {
		display: inline-block;
		padding: 6px 14px;
		background: rgba(255, 255, 255, 0.2);
		border: 1px solid rgba(255, 255, 255, 0.3);
		border-radius: 20px;
		font-size: 0.85rem;
		color: #ffffff;
		font-weight: 500;
		transition: all 0.3s ease;
	}

	.skill-tag:hover {
		background: rgba(255, 255, 255, 0.3);
		transform: translateY(-2px);
	}

	.interests-text {
		font-size: 0.95rem;
		color: rgba(255, 255, 255, 0.9);
		line-height: 1.8;
	}

	@media (max-width: 1024px) {
		.journey-grid {
			flex-direction: column;
		}

		.journey-column {
			flex: none;
		}

		.left-column .journey-card.glass,
		.right-column .journey-card.glass {
			flex: none;
		}

		.journey-card.glass {
			padding: 28px;
		}

		.journey-card h3 {
			font-size: 1.5rem;
		}
	}

	@media (max-width: 768px) {
		.journey-title {
			font-size: 2.5rem;
		}

		.journey-subtitle {
			font-size: 1rem;
			margin-bottom: 30px;
		}

		.journey-grid {
			grid-template-columns: 1fr;
			gap: 16px;
		}

		.journey-card.glass {
			padding: 24px;
		}

		.journey-card .card-icon {
			font-size: 2rem;
			margin-bottom: 12px;
		}

		.journey-card h3 {
			font-size: 1.35rem;
			margin-bottom: 16px;
		}

		.journey-card h4 {
			font-size: 1rem;
		}
	}

	@media (max-width: 480px) {
		.journey-container {
			padding: 40px 20px 60px 20px;
		}

		.journey-title {
			font-size: 2rem;
		}

		.journey-card.glass {
			padding: 20px;
		}

		.journey-card .card-icon {
			font-size: 1.75rem;
		}

		.journey-card h3 {
			font-size: 1.25rem;
		}

		.journey-card h4 {
			font-size: 0.95rem;
		}

		.skill-tags {
			gap: 6px;
		}

		.skill-tag {
			padding: 5px 12px;
			font-size: 0.8rem;
		}
	}

	.content-section {
		background: linear-gradient(180deg, #e8f4f8 0%, #d0e8f2 50%, #b8d8e8 100%);
		min-height: 50vh;
		padding: 0 40px 80px 40px;
	}

	.blog-section {
		max-width: 1200px;
		margin: 0 auto;
		opacity: 0;
		transform: translateY(40px);
		transition: opacity 0.8s ease, transform 0.8s ease;
	}

	.blog-section.visible {
		opacity: 1;
		transform: translateY(0);
	}

	.blog-title {
		text-align: center;
		font-size: 4rem;
		font-weight: 700;
		color: #1a365d;
		margin: 0 0 16px 0;
		text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	}

	.blog-subtitle {
		text-align: center;
		font-size: 1.125rem;
		color: #4a5568;
		margin: 0 0 12px 0;
		line-height: 1.6;
	}

	.see-all-link {
		display: block;
		text-align: center;
		font-size: 1rem;
		font-weight: 600;
		color: #4a8aa8;
		text-decoration: none;
		margin: 0 0 50px 0;
		transition: color 0.3s ease;
	}

	.see-all-link:hover {
		color: #3d7a96;
	}

	.see-all-link .arrow {
		margin-left: 4px;
		display: inline-block;
		transition: transform 0.3s ease;
	}

	.see-all-link:hover .arrow {
		transform: translateX(4px);
	}

	.blog-cards {
		display: flex;
		justify-content: center;
		gap: 30px;
		flex-wrap: wrap;
	}

	.blog-card.glass {
		flex: 1;
		max-width: 400px;
		min-width: 320px;
		border-radius: 24px;
		overflow: hidden;
		background: linear-gradient(
			135deg,
			rgba(255, 255, 255, 0.4) 0%,
			rgba(255, 255, 255, 0.1) 100%
		);
		backdrop-filter: blur(20px);
		-webkit-backdrop-filter: blur(20px);
		border: 1px solid rgba(255, 255, 255, 0.5);
		box-shadow:
			0 8px 32px rgba(31, 38, 135, 0.15),
			0 4px 16px rgba(0, 0, 0, 0.1),
			inset 0 1px 0 rgba(255, 255, 255, 0.6),
			inset 0 -1px 0 rgba(255, 255, 255, 0.2);
		transition: transform 0.3s ease, box-shadow 0.3s ease;
	}

	.blog-card.glass:hover {
		transform: translateY(-8px);
		box-shadow:
			0 16px 48px rgba(31, 38, 135, 0.2),
			0 8px 24px rgba(0, 0, 0, 0.15),
			inset 0 1px 0 rgba(255, 255, 255, 0.7),
			inset 0 -1px 0 rgba(255, 255, 255, 0.3);
	}

	.card-image {
		width: 100%;
		height: 240px;
		overflow: hidden;
	}

	.card-image img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		transition: transform 0.3s ease;
	}

	.blog-card.glass:hover .card-image img {
		transform: scale(1.05);
	}

	.card-content {
		padding: 24px;
		text-align: center;
	}

	.card-title {
		font-size: 1.25rem;
		font-weight: 600;
		color: #1a365d;
		margin: 0 0 12px 0;
	}

	.card-body {
		font-size: 0.95rem;
		line-height: 1.6;
		color: #2d3748;
		margin: 0 0 20px 0;
	}

	.read-more-btn {
		padding: 10px 24px;
		font-size: 0.9rem;
		font-weight: 600;
		color: #1a365d;
		background: linear-gradient(
			135deg,
			rgba(255, 255, 255, 0.6) 0%,
			rgba(255, 255, 255, 0.3) 100%
		);
		border: 1px solid rgba(255, 255, 255, 0.6);
		border-radius: 30px;
		cursor: pointer;
		backdrop-filter: blur(10px);
		-webkit-backdrop-filter: blur(10px);
		box-shadow:
			0 4px 12px rgba(31, 38, 135, 0.1),
			inset 0 1px 0 rgba(255, 255, 255, 0.5);
		transition: all 0.3s ease;
	}

	.read-more-btn:hover {
		background: linear-gradient(
			135deg,
			rgba(255, 255, 255, 0.8) 0%,
			rgba(255, 255, 255, 0.5) 100%
		);
		box-shadow:
			0 6px 16px rgba(31, 38, 135, 0.15),
			inset 0 1px 0 rgba(255, 255, 255, 0.7);
		transform: translateY(-2px);
	}

	@media (max-width: 768px) {
		.blog-title {
			font-size: 2.5rem;
			margin-bottom: 12px;
		}

		.blog-subtitle {
			font-size: 1rem;
			margin-bottom: 30px;
		}

		.blog-cards {
			gap: 20px;
		}

		.blog-card.glass {
			max-width: 100%;
		}
	}

	@media (max-width: 480px) {
		.blog-title {
			font-size: 2rem;
		}

		.blog-subtitle {
			font-size: 0.9rem;
		}
	}

	/* Newsletter Section */
	.newsletter-section {
		margin-top: 60px;
		display: flex;
		justify-content: center;
	}

	.newsletter-box.glass {
		max-width: 850px;
		width: 100%;
		padding: 28px 40px;
		border-radius: 24px;
		text-align: center;
		background: linear-gradient(
			135deg,
			rgba(255, 255, 255, 0.5) 0%,
			rgba(255, 255, 255, 0.2) 100%
		);
		backdrop-filter: blur(20px);
		-webkit-backdrop-filter: blur(20px);
		border: 1px solid rgba(255, 255, 255, 0.6);
		box-shadow:
			0 8px 32px rgba(31, 38, 135, 0.15),
			0 4px 16px rgba(0, 0, 0, 0.1),
			inset 0 1px 0 rgba(255, 255, 255, 0.7),
			inset 0 -1px 0 rgba(255, 255, 255, 0.3);
	}

	.newsletter-title {
		font-size: 1.75rem;
		font-weight: 700;
		color: #1a365d;
		margin: 0 0 12px 0;
	}

	.newsletter-description {
		font-size: 1rem;
		color: #4a5568;
		margin: 0 0 18px 0;
		line-height: 1.6;
	}

	.newsletter-form {
		width: 100%;
	}

	.input-wrapper {
		display: flex;
		gap: 12px;
		width: 100%;
	}

	.input-wrapper input {
		flex: 1;
		padding: 14px 20px;
		font-size: 1rem;
		border: 1px solid rgba(255, 255, 255, 0.6);
		border-radius: 30px;
		background: linear-gradient(
			135deg,
			rgba(255, 255, 255, 0.7) 0%,
			rgba(255, 255, 255, 0.4) 100%
		);
		backdrop-filter: blur(10px);
		-webkit-backdrop-filter: blur(10px);
		color: #1a365d;
		outline: none;
		transition: all 0.3s ease;
		box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.5);
	}

	.input-wrapper input::placeholder {
		color: #718096;
	}

	.input-wrapper input:focus {
		border-color: rgba(59, 130, 246, 0.5);
		box-shadow:
			0 0 0 3px rgba(59, 130, 246, 0.2),
			inset 0 1px 0 rgba(255, 255, 255, 0.5);
	}

	.input-wrapper input:disabled {
		opacity: 0.7;
		cursor: not-allowed;
	}

	.subscribe-btn {
		padding: 14px 28px;
		font-size: 1rem;
		font-weight: 600;
		color: white;
		background: linear-gradient(135deg, #4a8aa8 0%, #3d7a96 100%);
		border: none;
		border-radius: 30px;
		cursor: pointer;
		transition: all 0.3s ease;
		box-shadow:
			0 4px 15px rgba(74, 138, 168, 0.4),
			inset 0 1px 0 rgba(255, 255, 255, 0.2);
		min-width: 120px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.subscribe-btn:hover:not(:disabled) {
		background: linear-gradient(135deg, #5a9ab8 0%, #4d8aa6 100%);
		transform: translateY(-2px);
		box-shadow:
			0 6px 20px rgba(74, 138, 168, 0.5),
			inset 0 1px 0 rgba(255, 255, 255, 0.3);
	}

	.subscribe-btn:disabled {
		opacity: 0.8;
		cursor: not-allowed;
	}

	/* Spinner Animation */
	.spinner {
		width: 20px;
		height: 20px;
		border: 2px solid rgba(255, 255, 255, 0.3);
		border-top-color: white;
		border-radius: 50%;
		animation: spin 0.8s linear infinite;
	}

	@keyframes spin {
		to {
			transform: rotate(360deg);
		}
	}

	/* Success Message */
	.success-message {
		animation: fadeInUp 0.5s ease forwards;
	}

	.success-message h3 {
		font-size: 1.5rem;
		font-weight: 700;
		color: #1a365d;
		margin: 16px 0 8px 0;
	}

	.success-message p {
		font-size: 1rem;
		color: #4a5568;
		margin: 0;
	}

	@keyframes fadeInUp {
		from {
			opacity: 0;
			transform: translateY(20px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	/* Checkmark Animation */
	.checkmark-circle {
		width: 80px;
		height: 80px;
		margin: 0 auto;
	}

	.checkmark {
		width: 100%;
		height: 100%;
	}

	.checkmark-bg {
		stroke: #4a8aa8;
		stroke-width: 2;
		stroke-dasharray: 166;
		stroke-dashoffset: 166;
		animation: strokeCircle 0.6s ease forwards;
	}

	.checkmark-check {
		stroke: #4a8aa8;
		stroke-width: 3;
		stroke-linecap: round;
		stroke-linejoin: round;
		stroke-dasharray: 48;
		stroke-dashoffset: 48;
		animation: strokeCheck 0.4s ease forwards 0.4s;
	}

	@keyframes strokeCircle {
		to {
			stroke-dashoffset: 0;
		}
	}

	@keyframes strokeCheck {
		to {
			stroke-dashoffset: 0;
		}
	}

	@media (max-width: 768px) {
		.newsletter-box.glass {
			padding: 30px 24px;
			margin: 0 20px;
		}

		.newsletter-title {
			font-size: 1.5rem;
		}

		.input-wrapper {
			flex-direction: column;
		}

		.subscribe-btn {
			width: 100%;
		}
	}

	.container {
		position: relative;
		width: 100%;
		max-width: 1400px;
		height: 100vh;
		margin: 0 auto;
		padding: 0 60px;
	}

	.image-gallery {
		display: flex;
		justify-content: space-between;
		align-items: flex-start;
		width: 100%;
		min-height: 600px;
		padding: 60px 60px 180px;
		box-sizing: border-box;
	}

	.image-wrapper {
		position: relative;
		border-radius: 20px;
		overflow: hidden;
		box-shadow:
			0 0 30px rgba(59, 130, 246, 0.5),
			0 0 60px rgba(59, 130, 246, 0.3),
			0 10px 40px rgba(0, 0, 0, 0.3);
		transition: opacity 0.6s ease, transform 0.6s ease, box-shadow 0.3s ease;
		flex: 1;
		max-width: 320px;
		margin: 0 15px;
		opacity: 0;
		transform: translateY(40px);
	}

	.image-wrapper.visible {
		opacity: 1;
	}

	.image-wrapper.visible.tilt-left {
		transform: translateY(0) rotate(-3deg);
	}

	.image-wrapper.visible.tilt-right {
		transform: translateY(0) rotate(3deg);
	}

	.image-wrapper.visible:not(.tilt-left):not(.tilt-right) {
		transform: translateY(0);
	}

	.image-wrapper:hover {
		box-shadow:
			0 0 40px rgba(59, 130, 246, 0.7),
			0 0 80px rgba(59, 130, 246, 0.4),
			0 15px 50px rgba(0, 0, 0, 0.4);
	}

	.image-wrapper.tilt-left {
		transform: translateY(40px) rotate(-3deg);
	}

	.image-wrapper.tilt-right {
		transform: translateY(40px) rotate(3deg);
	}

	.image-wrapper.tilt-left:hover {
		transform: translateY(0) rotate(-3deg) scale(1.05);
	}

	.image-wrapper.tilt-right:hover {
		transform: translateY(0) rotate(3deg) scale(1.05);
	}

	.image-wrapper img {
		display: block;
		width: 100%;
		height: 400px;
		object-fit: cover;
		border-radius: 20px;
	}

	.image-wrapper.image-3 img {
		object-position: 40% 40%;
	}

	.image-wrapper.image-4 img {
		object-position: 80% center;
	}

	@media (max-width: 1200px) {
		.image-gallery {
			min-height: 550px;
			padding: 50px 40px 160px;
		}

		.image-wrapper {
			max-width: 260px;
			margin: 0 10px;
		}

		.image-wrapper img {
			height: 330px;
		}
	}

	@media (max-width: 1024px) {
		.image-gallery {
			min-height: 500px;
			padding: 40px 30px 140px;
		}

		.image-wrapper {
			max-width: 210px;
			margin: 0 8px;
		}

		.image-wrapper img {
			height: 270px;
		}
	}

	@media (max-width: 768px) {
		.container {
			padding: 0 30px;
		}

		.image-gallery {
			flex-wrap: wrap;
			justify-content: center;
			gap: 20px;
			min-height: auto;
			padding: 40px 20px 120px;
		}

		.image-wrapper {
			max-width: 160px;
			margin: 0;
			border-radius: 14px;
		}

		.image-wrapper img {
			height: 210px;
			border-radius: 14px;
		}
	}

	@media (max-width: 480px) {
		.image-gallery {
			gap: 12px;
			min-height: auto;
			padding: 30px 15px 100px;
		}

		.image-wrapper {
			max-width: 115px;
			border-radius: 10px;
		}

		.image-wrapper img {
			height: 150px;
			border-radius: 10px;
		}

		.image-wrapper.tilt-left {
			transform: rotate(-2deg);
		}

		.image-wrapper.tilt-right {
			transform: rotate(2deg);
		}
	}

	/* About Section */
	.about-section {
		background: linear-gradient(180deg, #e8f4f8 0%, #e8f4f8 100%);
		padding: 80px 40px 60px 40px;
	}

	.about-container {
		max-width: 1200px;
		margin: 0 auto;
	}

	.about-content {
		display: flex;
		align-items: center;
		gap: 60px;
	}

	.about-text {
		flex: 1;
	}

	.about-title {
		font-size: 3.5rem;
		font-weight: 700;
		color: #1a365d;
		margin: 0 0 24px 0;
		text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	}

	.about-body {
		font-size: 1.125rem;
		line-height: 1.8;
		color: #2d3748;
		margin: 0 0 20px 0;
	}

	.about-body:last-child {
		margin-bottom: 0;
	}

	.about-image-wrapper {
		flex-shrink: 0;
		width: 320px;
		height: 320px;
		border-radius: 50%;
		overflow: hidden;
		box-shadow:
			0 0 40px rgba(59, 130, 246, 0.4),
			0 0 80px rgba(59, 130, 246, 0.2),
			0 20px 60px rgba(0, 0, 0, 0.3);
		border: 4px solid rgba(255, 255, 255, 0.8);
	}

	.about-image {
		width: 100%;
		height: 100%;
		object-fit: cover;
		object-position: center top;
	}

	/* Random Things Carousel */
	.random-things {
		margin-top: 60px;
		overflow: hidden;
	}

	.random-things-title {
		text-align: center;
		font-size: 1.5rem;
		font-weight: 600;
		color: #4a5568;
		margin: 0 0 24px 0;
		letter-spacing: 0.5px;
	}

	.carousel-container {
		width: 100%;
		overflow: hidden;
		mask-image: linear-gradient(to right, transparent 0%, black 10%, black 90%, transparent 100%);
		-webkit-mask-image: linear-gradient(to right, transparent 0%, black 10%, black 90%, transparent 100%);
		padding: 20px 0;
	}

	.carousel-track {
		display: flex;
		gap: 40px;
		animation: scroll 45s linear infinite;
		width: max-content;
	}

	.carousel-item {
		flex-shrink: 0;
		padding: 12px 28px;
		background: linear-gradient(
			135deg,
			rgba(255, 255, 255, 0.6) 0%,
			rgba(255, 255, 255, 0.3) 100%
		);
		backdrop-filter: blur(10px);
		-webkit-backdrop-filter: blur(10px);
		border: 1px solid rgba(255, 255, 255, 0.6);
		border-radius: 30px;
		font-size: 1rem;
		font-weight: 500;
		color: #1a365d;
		white-space: nowrap;
		box-shadow:
			0 4px 12px rgba(31, 38, 135, 0.1),
			inset 0 1px 0 rgba(255, 255, 255, 0.5);
	}

	@keyframes scroll {
		0% {
			transform: translateX(0);
		}
		100% {
			transform: translateX(-50%);
		}
	}

	@media (max-width: 1024px) {
		.about-content {
			gap: 40px;
		}

		.about-image-wrapper {
			width: 280px;
			height: 280px;
		}

		.about-title {
			font-size: 3rem;
		}
	}

	@media (max-width: 768px) {
		.about-section {
			padding: 60px 30px 50px 30px;
		}

		.about-content {
			flex-direction: column-reverse;
			text-align: center;
		}

		.about-image-wrapper {
			width: 240px;
			height: 240px;
		}

		.about-title {
			font-size: 2.5rem;
		}

		.about-body {
			font-size: 1rem;
		}

		.random-things {
			margin-top: 40px;
		}

		.random-things-title {
			font-size: 1.25rem;
		}

		.carousel-item {
			padding: 10px 20px;
			font-size: 0.9rem;
		}

		.carousel-track {
			gap: 24px;
		}
	}

	@media (max-width: 480px) {
		.about-section {
			padding: 50px 20px 40px 20px;
		}

		.about-image-wrapper {
			width: 200px;
			height: 200px;
		}

		.about-title {
			font-size: 2rem;
		}

		.about-body {
			font-size: 0.95rem;
			line-height: 1.7;
		}

		.carousel-item {
			padding: 8px 16px;
			font-size: 0.85rem;
		}

		.carousel-track {
			gap: 16px;
			animation-duration: 30s;
		}
	}

	/* Contact Section */
	.contact-section {
		background: #e8f4f8;
		width: 100%;
		margin-top: -1px;
	}

	.wave-divider-contact {
		width: 100%;
		line-height: 0;
	}

	.wave-divider-contact svg {
		width: 100%;
		height: 120px;
		display: block;
	}

	.wave-shadow-contact {
		fill: none;
		stroke: rgba(0, 0, 0, 0.1);
		stroke-width: 3;
		filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.15));
		transform: translateY(2px);
	}

	.wave-fill-contact {
		fill: #e8f4f8;
	}

	.contact-container {
		width: 100%;
		max-width: 1200px;
		margin: 0 auto;
		padding: 0 40px 40px 40px;
		box-sizing: border-box;
	}

	.contact-content {
		display: flex;
		align-items: center;
		gap: 60px;
	}

	.contact-left {
		flex-shrink: 0;
	}

	.contact-image-wrapper {
		width: 340px;
		height: 340px;
		border-radius: 20px;
		overflow: hidden;
		box-shadow:
			0 0 30px rgba(59, 130, 246, 0.3),
			0 0 60px rgba(59, 130, 246, 0.15),
			0 15px 40px rgba(0, 0, 0, 0.2);
		border: 3px solid rgba(255, 255, 255, 0.8);
		transition: transform 0.3s ease, box-shadow 0.3s ease;
	}

	.contact-image-wrapper:hover {
		transform: translateY(-5px);
		box-shadow:
			0 0 40px rgba(59, 130, 246, 0.4),
			0 0 80px rgba(59, 130, 246, 0.2),
			0 20px 50px rgba(0, 0, 0, 0.25);
	}

	.contact-image {
		width: 100%;
		height: 100%;
		object-fit: cover;
		object-position: center;
	}

	.contact-right {
		flex: 1;
	}

	.contact-title {
		font-size: 3rem;
		font-weight: 700;
		color: #1a365d;
		margin: 0 0 16px 0;
		text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	}

	.typing-cursor {
		opacity: 0;
		animation: none;
	}

	.typing-cursor.visible {
		opacity: 1;
		animation: blink 0.7s step-end infinite;
	}

	@keyframes blink {
		50% {
			opacity: 0;
		}
	}

	.contact-description {
		font-size: 1.125rem;
		line-height: 1.8;
		color: #2d3748;
		margin: 0 0 28px 0;
	}

	.contact-info {
		display: flex;
		flex-direction: column;
		gap: 16px;
		margin-bottom: 28px;
	}

	.contact-item {
		display: flex;
		align-items: center;
		gap: 12px;
		font-size: 1rem;
		color: #4a5568;
	}

	.contact-item a {
		color: #2d3748;
		text-decoration: none;
		transition: color 0.3s ease;
	}

	.contact-item a:hover {
		color: #1a202c;
		text-decoration: underline;
	}

	.contact-icon {
		width: 22px;
		height: 22px;
		color: #2d3748;
		flex-shrink: 0;
	}

	.social-links {
		display: flex;
		gap: 16px;
	}

	.social-link {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 48px;
		height: 48px;
		border-radius: 50%;
		background: linear-gradient(
			135deg,
			rgba(255, 255, 255, 0.8) 0%,
			rgba(255, 255, 255, 0.4) 100%
		);
		backdrop-filter: blur(10px);
		-webkit-backdrop-filter: blur(10px);
		border: 1px solid rgba(255, 255, 255, 0.6);
		box-shadow:
			0 4px 12px rgba(31, 38, 135, 0.1),
			inset 0 1px 0 rgba(255, 255, 255, 0.5);
		color: #4a8aa8;
		transition: all 0.3s ease;
	}

	.social-link:hover {
		background: linear-gradient(135deg, #4a8aa8 0%, #3d7a96 100%);
		color: white;
		transform: translateY(-3px);
		box-shadow:
			0 8px 20px rgba(74, 138, 168, 0.4),
			inset 0 1px 0 rgba(255, 255, 255, 0.2);
	}

	.social-link svg {
		width: 24px;
		height: 24px;
	}

	.contact-footer {
		margin-top: 50px;
		padding-top: 24px;
		border-top: 1px solid rgba(74, 138, 168, 0.2);
		text-align: center;
	}

	.contact-footer p {
		font-size: 0.9rem;
		color: #718096;
		margin: 0;
	}

	@media (max-width: 1024px) {
		.contact-content {
			gap: 40px;
		}

		.contact-image-wrapper {
			width: 280px;
			height: 280px;
		}

		.contact-title {
			font-size: 2.5rem;
		}
	}

	@media (max-width: 768px) {
		.contact-container {
			padding: 0 30px 30px 30px;
		}

		.contact-content {
			flex-direction: column;
			text-align: center;
		}

		.contact-image-wrapper {
			width: 260px;
			height: 260px;
		}

		.contact-title {
			font-size: 2.25rem;
		}

		.contact-description {
			font-size: 1rem;
		}

		.contact-info {
			align-items: center;
		}

		.social-links {
			justify-content: center;
		}
	}

	@media (max-width: 480px) {
		.contact-container {
			padding: 0 20px 24px 20px;
		}

		.contact-image-wrapper {
			width: 220px;
			height: 220px;
		}

		.contact-title {
			font-size: 1.875rem;
		}

		.contact-description {
			font-size: 0.95rem;
			line-height: 1.7;
		}

		.social-link {
			width: 44px;
			height: 44px;
		}

		.social-link svg {
			width: 20px;
			height: 20px;
		}

		.contact-footer {
			margin-top: 30px;
		}
	}
</style>
