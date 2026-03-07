<script>
	import { onMount } from 'svelte';
	import Header from '$lib/components/Header.svelte';
	import HeroLeft from '$lib/components/HeroLeft.svelte';
	import HeroImage from '$lib/components/HeroImage.svelte';
	import HeroRight from '$lib/components/HeroRight.svelte';
	import NameOverlay from '$lib/components/NameOverlay.svelte';

	const heroImage = '/Ibrahim_Headshot_optimized.png';
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
	let aboutVisible = false;
	let journeyVisible = false;
	let contactVisible = false;

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

		// Generic section observer
		const sectionObserver = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						const id = entry.target.getAttribute('data-section');
						if (id === 'about') aboutVisible = true;
						if (id === 'blog') blogSectionVisible = true;
						if (id === 'journey') journeyVisible = true;
						if (id === 'contact') contactVisible = true;
					}
				});
			},
			{ threshold: 0.15, rootMargin: '0px 0px -60px 0px' }
		);

		// Observe all image wrappers after a short delay to ensure DOM is ready
		setTimeout(() => {
			const imageWrappers = document.querySelectorAll('.image-wrapper');
			imageWrappers.forEach((wrapper) => {
				observer.observe(wrapper);
			});

			// Observe sections
			document.querySelectorAll('[data-section]').forEach((el) => {
				sectionObserver.observe(el);
			});

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
			sectionObserver.disconnect();
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
				<img src={num === 1 ? '/taiwan.jpg' : num === 2 ? '/image-2.jpeg' : `/image-${num}.jpg`} alt="Gallery image {num}" />
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

<!-- About Section -->
<section id="about" class="about-section" data-section="about">
	<div class="about-container" class:visible={aboutVisible}>
		<div class="about-content">
			<div class="about-text">
				<span class="section-label">Get to Know Me</span>
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

<!-- Blog Section -->
<section class="content-section">
	<div id="blog" class="blog-section" data-section="blog" class:visible={blogSectionVisible}>
		<span class="section-label center">Latest Updates</span>
		<h2 class="blog-title">What I've Been Up To Recently...</h2>
		<p class="blog-subtitle">Read about my most recent work, projects, trips, and stories</p>
		<a href="/blog" class="see-all-link">See All <span class="arrow">&rarr;</span></a>
		<div class="blog-cards">
			<article class="blog-card">
				<div class="card-image">
					<img src="/workly_blog_cover.jpg" alt="Building the Plane as it Flies" />
				</div>
				<div class="card-content">
					<div class="card-meta">
						<span class="card-tag">Startup</span>
						<span class="card-date">December 2025</span>
					</div>
					<h3 class="card-title">Building the Plane as it Flies</h3>
					<p class="card-body">Lessons learned launching my first venture: the chaos, the pivots, and what I'd do differently.</p>
					<a href="/blog/building-the-plane" class="read-more-link">Read More <span class="arrow">&rarr;</span></a>
				</div>
			</article>
			<article class="blog-card">
				<div class="card-image">
					<img src="/skynav_blog.JPG" alt="SkyNav: Building AI for the Elderly" />
				</div>
				<div class="card-content">
					<div class="card-meta">
						<span class="card-tag">Professional</span>
						<span class="card-date">July 2025</span>
					</div>
					<h3 class="card-title">SkyNav: Building AI for the Elderly</h3>
					<p class="card-body">How our team designed and built an AI platform to improve accessibility and information access for aging populations in Western NC.</p>
					<a href="/blog/skynav" class="read-more-link">Read More <span class="arrow">&rarr;</span></a>
				</div>
			</article>
			<article class="blog-card">
				<div class="card-image">
					<img src="/22_days_away.jpg" alt="22 Days Away: Stories from the Wilderness of Lake Superior" />
				</div>
				<div class="card-content">
					<div class="card-meta">
						<span class="card-tag">Travel</span>
						<span class="card-date">July 2024</span>
					</div>
					<h3 class="card-title">22 Days Away</h3>
					<p class="card-body">Stories from 90 miles of open water and 22 days away having never camped a night before in my life.</p>
					<a href="/blog/lake-superior" class="read-more-link">Read More <span class="arrow">&rarr;</span></a>
				</div>
			</article>
		</div>

	</div>
</section>

<!-- Journey Section -->
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
	<div id="experience" class="journey-container" data-section="journey" class:visible={journeyVisible}>
		<span class="section-label center light">My Background</span>
		<h2 class="journey-title">The Journey So Far</h2>
		<p class="journey-subtitle">Milestones, experiences, and the path that brought me here</p>

		<div class="journey-grid">
			<!-- Left Column: Experience, Education, Skills (bottom) -->
			<div class="journey-column left-column">
				<div class="journey-card experience-card">
					<div class="card-header">
						<span class="card-icon">💼</span>
						<h3>Experience</h3>
					</div>
					<div class="card-body">
						<div class="experience-item with-logo">
							<img src="/ai_consulting.jpeg" alt="AI Consulting @ UNC" class="item-logo" />
							<div class="item-text">
								<h4>VP of Technology</h4>
								<p class="company">AI Consulting @ UNC &middot; Oct – Dec 2025</p>
							</div>
						</div>
						<div class="experience-item with-logo">
							<img src="/land_of_sky_regional_council.jpeg" alt="Land of Sky Regional Council" class="item-logo" />
							<div class="item-text">
								<h4>Full Stack Developer</h4>
								<p class="company">Land of Sky Regional Council &middot; May – Jul 2025</p>
							</div>
						</div>
						<div class="experience-item with-logo">
							<img src="/palmetto_and_pine.jpeg" alt="Palmetto and Pine" class="item-logo" />
							<div class="item-text">
								<h4>Private Equity Analyst</h4>
								<p class="company">Palmetto and Pine &middot; Jun – Nov 2025</p>
							</div>
						</div>
						<div class="experience-item with-logo">
							<img src="/ics.png" alt="Impact Consulting Studio" class="item-logo" />
							<div class="item-text">
								<h4>Project Lead</h4>
								<p class="company">Impact Consulting Studio &middot; Sep – Nov 2025</p>
							</div>
						</div>
					</div>
					<div class="cv-actions">
						<a
							href="/MOHSIN%20Ibrahim_Resume.pdf"
							class="cv-btn"
							target="_blank"
							rel="noopener noreferrer"
						>
							See Full CV
							<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
						</a>
						<a
							href="https://linkedin.com/in/ibrahimmohsin"
							target="_blank"
							rel="noopener noreferrer"
							class="linkedin-glass-btn"
							aria-label="View LinkedIn profile"
						>
							<svg viewBox="0 0 24 24" aria-hidden="true">
								<path
									fill="currentColor"
									d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"
								/>
							</svg>
						</a>
					</div>
				</div>

				<div class="journey-card education-card">
					<div class="card-header">
						<span class="card-icon">🎓</span>
						<h3>Education</h3>
					</div>
					<div class="card-body">
						<div class="education-item with-logo">
							<img src="/unc_chapel_hill.jpeg" alt="UNC Chapel Hill" class="item-logo" />
							<div class="item-text">
								<h4>University of North Carolina at Chapel Hill</h4>
								<p class="degree">B.S. Computer Science &amp; Business Administration, PPE Minor &middot; 2024 – 2028</p>
								<p class="honor">Morehead-Cain Scholar &middot; Honors Carolina</p>
							</div>
						</div>
						<div class="education-item with-logo">
							<img src="/NUS-logo.png" alt="National University of Singapore" class="item-logo" />
							<div class="item-text">
								<h4>National University of Singapore</h4>
								<p class="degree">Exchange Program, School of Computing &middot; Spring 2026</p>
							</div>
						</div>
						<div class="education-item with-logo">
							<img src="/park_tudor_school.png" alt="Park Tudor School" class="item-logo" />
							<div class="item-text">
								<h4>Park Tudor School</h4>
								<p class="degree">High School Diploma &middot; Indianapolis, 2020 – 2024</p>
							</div>
						</div>
					</div>
				</div>

				<div class="journey-card skills-card">
					<div class="card-header">
						<span class="card-icon">✨</span>
						<h3>Skills + Interests</h3>
					</div>
					<div class="skills-section">
						<div class="skill-group">
							<h4>Technical Skills</h4>
							<div class="skill-tags">
								<span class="skill-tag">JavaScript / TypeScript</span>
								<span class="skill-tag">Python</span>
								<span class="skill-tag">RAG Architecture</span>
								<span class="skill-tag">PostgreSQL</span>
								<span class="skill-tag">React</span>
							</div>
						</div>
						<div class="skill-group">
							<h4>Interests</h4>
							<div class="skill-tags">
								<span class="skill-tag interest">🏋️ Weightlifting</span>
								<span class="skill-tag interest">⛳ Golf</span>
								<span class="skill-tag interest">🎛️ DJing</span>
								<span class="skill-tag interest">🚣 Kayaking</span>
								<span class="skill-tag interest">📖 Teaching</span>
								<span class="skill-tag interest">✈️ Travel</span>
							</div>
						</div>
					</div>
				</div>
			</div>

			<!-- Right Column: Newsletter + Currently Working + Notable Projects -->
			<div class="journey-column right-column">
				<div class="journey-card newsletter-card">
					<div class="card-header">
						<span class="card-icon">📬</span>
						<h3>Stay in the Loop</h3>
					</div>
					{#if isSubscribed}
						<div class="success-message success-journey">
							<div class="checkmark-circle">
								<svg class="checkmark" viewBox="0 0 52 52">
									<circle class="checkmark-bg" cx="26" cy="26" r="25" fill="none"/>
									<path class="checkmark-check" fill="none" d="M14.1 27.2l7.1 7.2 16.7-16.8"/>
								</svg>
							</div>
							<p>You're in! Thanks for subscribing.</p>
						</div>
					{:else}
						<p class="journey-newsletter-desc">Subscribe to my newsletter and never miss a new post or update.</p>
						<form class="journey-newsletter-form" on:submit={handleSubscribe}>
							<input
								type="email"
								class="journey-newsletter-input"
								placeholder="Enter your email"
								bind:value={email}
								required
								disabled={isSubmitting}
							/>
							<button type="submit" class="journey-subscribe-btn" disabled={isSubmitting}>
								{#if isSubmitting}
									<span class="spinner"></span>
								{:else}
									Subscribe
								{/if}
							</button>
						</form>
					{/if}
				</div>

				<div class="journey-card current-card">
					<div class="card-header">
						<span class="card-icon">🚀</span>
						<h3>Currently Working on...</h3>
					</div>
					<div class="card-body">
						<div class="project-item with-logo">
							<img src="/Lintel_Logo copy.png" alt="Lintel" class="item-logo logo-white-bg" />
							<div class="item-text">
								<h4>Lintel</h4>
								<p>AI-powered risk management platform for the construction industry</p>
							</div>
						</div>
						<div class="project-item">
							<h4>Personal Investment Portfolio Agents</h4>
							<p>Using AI agents to research, analyze, and make smarter investment decisions</p>
						</div>
					</div>
				</div>

				<div class="journey-card projects-card">
					<div class="card-header">
						<span class="card-icon">⭐</span>
						<h3>Notable Projects</h3>
					</div>
					<div class="card-body">
						<div class="project-item with-logo">
							<img src="/workly.jpeg" alt="Workly" class="item-logo" />
							<div class="item-text">
								<h4>Workly</h4>
								<p>Mobile gig-marketplace connecting college students with local homeowners</p>
							</div>
						</div>
						<div class="project-item with-logo">
							<img src="/sky_nav.png" alt="SkyNav" class="item-logo logo-white-bg" />
							<div class="item-text">
								<h4>SkyNav — LOS Regional Council</h4>
								<p>AI platform increasing accessibility and information availability for elderly populations</p>
							</div>
						</div>
						<div class="project-item">
							<h4>AceGlass</h4>
							<p>AI-powered poker glasses with real-time hand analysis</p>
						</div>
						<div class="project-item">
							<h4>Independent Research: Wealth Inequality</h4>
							<p>
								180+ page dueling-historian paper on wealth inequality in the US &mdash;
								<a
									href="https://www.youtube.com/watch?v=Drk4YNltrIg&t=3590s"
									class="project-link"
									target="_blank"
									rel="noopener noreferrer"
								>
									watch the debate
								</a>
							</p>
						</div>
						<div class="project-item with-logo">
							<img src="/vex_robotics.png" alt="Vex Robotics" class="item-logo" />
							<div class="item-text">
								<h4>Vex Robotics</h4>
								<p>Programmed and designed robots to play frisbee golf, stack cubes, and more</p>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- Contact Section -->
<section id="contact" class="contact-section" data-section="contact">
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
	<div class="contact-container" class:visible={contactVisible}>
		<div class="contact-content">
			<div class="contact-left">
				<div class="contact-image-wrapper">
					<img src="/contact_headshot.jpg" alt="Ibrahim" class="contact-image" />
				</div>
			</div>
			<div class="contact-right">
				<span class="section-label">Get in Touch</span>
				<h2 class="contact-title">{contactTitleText}<span class="typing-cursor" class:visible={contactTitleVisible}>|</span></h2>
				<p class="contact-description">
					I'm always open to discussing new opportunities, collaborations, or just having a conversation about tech, startups, or anything interesting. Feel free to reach out!
				</p>
				<div class="contact-info">
					<a href="mailto:imohsin@unc.edu" class="contact-item">
						<div class="contact-icon-wrapper">
							<svg class="contact-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
								<path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
								<polyline points="22,6 12,13 2,6"/>
							</svg>
						</div>
						<span>imohsin@unc.edu</span>
					</a>
					<div class="contact-item">
						<div class="contact-icon-wrapper">
							<svg class="contact-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
								<path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/>
								<circle cx="12" cy="10" r="3"/>
							</svg>
						</div>
						<span>Singapore</span>
					</div>
				</div>
				<div class="social-links">
					<a href="https://www.linkedin.com/in/ibrahim-mohsin-16a1b8261/" target="_blank" rel="noopener noreferrer" class="social-link" aria-label="LinkedIn">
						<svg viewBox="0 0 24 24" fill="currentColor">
							<path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
						</svg>
					</a>
					<a href="https://github.com/imohsin3797" target="_blank" rel="noopener noreferrer" class="social-link" aria-label="GitHub">
						<svg viewBox="0 0 24 24" fill="currentColor">
							<path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
						</svg>
					</a>
					<a href="https://x.com/IbrahimMohsin_" target="_blank" rel="noopener noreferrer" class="social-link" aria-label="X (Twitter)">
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

	/* ===== HERO ===== */
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

	.container {
		position: relative;
		width: 100%;
		max-width: 1400px;
		height: 100vh;
		margin: 0 auto;
		padding: 0 60px;
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

	/* ===== SHARED ===== */
	.section-label {
		display: inline-block;
		font-size: 0.8rem;
		font-weight: 600;
		letter-spacing: 2.5px;
		text-transform: uppercase;
		color: #4a8aa8;
		margin-bottom: 12px;
		position: relative;
		padding-left: 28px;
	}

	.section-label::before {
		content: '';
		position: absolute;
		left: 0;
		top: 50%;
		transform: translateY(-50%);
		width: 20px;
		height: 2px;
		background: #4a8aa8;
		border-radius: 2px;
	}

	.section-label.center {
		display: block;
		text-align: center;
		padding-left: 0;
	}

	.section-label.center::before {
		display: none;
	}

	.section-label.light {
		color: rgba(255, 255, 255, 0.8);
	}

	/* ===== IMAGE GALLERY ===== */
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

	/* ===== ABOUT SECTION ===== */
	.about-section {
		background: #e8f4f8;
		padding: 80px 40px 60px 40px;
	}

	.about-container {
		max-width: 1100px;
		margin: 0 auto;
		opacity: 0;
		transform: translateY(30px);
		transition: opacity 0.7s ease, transform 0.7s ease;
	}

	.about-container.visible {
		opacity: 1;
		transform: translateY(0);
	}

	.about-content {
		display: flex;
		align-items: center;
		gap: 64px;
	}

	.about-text {
		flex: 1;
	}

	.about-title {
		font-size: 3rem;
		font-weight: 700;
		color: #1a365d;
		margin: 0 0 24px 0;
		line-height: 1.1;
	}

	.about-body {
		font-size: 1.1rem;
		line-height: 1.8;
		color: #374a5e;
		margin: 0 0 18px 0;
	}

	.about-body:last-child {
		margin-bottom: 0;
	}

	.about-image-wrapper {
		flex-shrink: 0;
		width: 300px;
		height: 380px;
		border-radius: 24px;
		overflow: hidden;
		box-shadow:
			0 20px 50px rgba(61, 122, 150, 0.25),
			0 8px 20px rgba(0, 0, 0, 0.12);
		border: 3px solid rgba(255, 255, 255, 0.9);
		transition: transform 0.4s ease;
	}

	.about-image-wrapper:hover {
		transform: translateY(-6px) rotate(1deg);
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
		font-size: 1.35rem;
		font-weight: 600;
		color: #4a5e73;
		margin: 0 0 24px 0;
		letter-spacing: 0.3px;
	}

	.carousel-container {
		width: 100%;
		overflow: hidden;
		mask-image: linear-gradient(to right, transparent 0%, black 10%, black 90%, transparent 100%);
		-webkit-mask-image: linear-gradient(to right, transparent 0%, black 10%, black 90%, transparent 100%);
		padding: 16px 0;
	}

	.carousel-track {
		display: flex;
		gap: 32px;
		animation: scroll 45s linear infinite;
		width: max-content;
	}

	.carousel-item {
		flex-shrink: 0;
		padding: 10px 24px;
		background: rgba(255, 255, 255, 0.7);
		border: 1px solid rgba(74, 138, 168, 0.15);
		border-radius: 50px;
		font-size: 0.95rem;
		font-weight: 500;
		color: #2d4a5e;
		white-space: nowrap;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
		transition: transform 0.2s ease, box-shadow 0.2s ease;
	}

	.carousel-item:hover {
		transform: translateY(-2px);
		box-shadow: 0 4px 14px rgba(0, 0, 0, 0.1);
	}

	@keyframes scroll {
		0% {
			transform: translateX(0);
		}
		100% {
			transform: translateX(-50%);
		}
	}

	/* ===== BLOG / CONTENT SECTION ===== */
	.content-section {
		background: linear-gradient(180deg, #e8f4f8 0%, #daeaf3 50%, #c8dde9 100%);
		min-height: 50vh;
		padding: 0 40px 80px 40px;
	}

	.blog-section {
		max-width: 1100px;
		margin: 0 auto;
		opacity: 0;
		transform: translateY(30px);
		transition: opacity 0.7s ease, transform 0.7s ease;
	}

	.blog-section.visible {
		opacity: 1;
		transform: translateY(0);
	}

	.blog-title {
		text-align: center;
		font-size: 3rem;
		font-weight: 700;
		color: #1a365d;
		margin: 0 0 14px 0;
		line-height: 1.15;
	}

	.blog-subtitle {
		text-align: center;
		font-size: 1.1rem;
		color: #4a5e73;
		margin: 0 0 10px 0;
		line-height: 1.6;
	}

	.see-all-link {
		display: block;
		text-align: center;
		font-size: 0.95rem;
		font-weight: 600;
		color: #4a8aa8;
		text-decoration: none;
		margin: 0 0 44px 0;
		transition: color 0.3s ease;
	}

	.see-all-link:hover {
		color: #3d7a96;
	}

	.see-all-link .arrow,
	.read-more-link .arrow {
		display: inline-block;
		transition: transform 0.3s ease;
	}

	.see-all-link:hover .arrow,
	.read-more-link:hover .arrow {
		transform: translateX(4px);
	}

	.blog-cards {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 28px;
	}

	.blog-card {
		border-radius: 20px;
		overflow: hidden;
		background: rgba(255, 255, 255, 0.55);
		backdrop-filter: blur(16px);
		-webkit-backdrop-filter: blur(16px);
		border: 1px solid rgba(255, 255, 255, 0.7);
		box-shadow: 0 4px 20px rgba(0, 0, 0, 0.06);
		transition: transform 0.35s ease, box-shadow 0.35s ease;
	}

	.blog-card:hover {
		transform: translateY(-8px);
		box-shadow: 0 16px 40px rgba(0, 0, 0, 0.1);
	}

	.card-image {
		width: 100%;
		height: 220px;
		overflow: hidden;
	}

	.card-image img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		transition: transform 0.5s ease;
	}

	.blog-card:hover .card-image img {
		transform: scale(1.06);
	}

	.card-content {
		padding: 24px 24px 28px;
	}

	.card-meta {
		display: flex;
		align-items: center;
		gap: 10px;
		margin-bottom: 12px;
	}

	.card-tag {
		display: inline-block;
		font-size: 0.75rem;
		font-weight: 600;
		letter-spacing: 1px;
		text-transform: uppercase;
		color: #4a8aa8;
		background: rgba(74, 138, 168, 0.1);
		padding: 4px 12px;
		border-radius: 50px;
	}

	.card-date {
		font-size: 0.78rem;
		color: #8a9bb0;
		font-weight: 500;
	}

	.card-title {
		font-size: 1.2rem;
		font-weight: 650;
		color: #1a365d;
		margin: 0 0 10px 0;
		line-height: 1.35;
	}

	.card-body {
		font-size: 0.92rem;
		line-height: 1.65;
		color: #4a5e73;
		margin: 0 0 18px 0;
	}

	.read-more-link {
		font-size: 0.9rem;
		font-weight: 600;
		color: #4a8aa8;
		text-decoration: none;
		transition: color 0.2s ease;
	}

	.read-more-link:hover {
		color: #3d7a96;
	}

	/* Journey Newsletter Card */
	.journey-newsletter-desc {
		font-size: 0.9rem;
		color: rgba(255, 255, 255, 0.8);
		line-height: 1.55;
		margin: 0 0 16px 0;
	}

	.journey-newsletter-form {
		display: flex;
		flex-direction: column;
		gap: 10px;
	}

	.journey-newsletter-input {
		width: 100%;
		padding: 11px 16px;
		font-size: 0.9rem;
		border: 1px solid rgba(255, 255, 255, 0.2);
		border-radius: 50px;
		background: rgba(255, 255, 255, 0.1);
		color: #ffffff;
		outline: none;
		box-sizing: border-box;
		transition: border-color 0.3s ease, box-shadow 0.3s ease;
	}

	.journey-newsletter-input::placeholder {
		color: rgba(255, 255, 255, 0.45);
	}

	.journey-newsletter-input:focus {
		border-color: rgba(255, 255, 255, 0.45);
		box-shadow: 0 0 0 3px rgba(255, 255, 255, 0.1);
	}

	.journey-newsletter-input:disabled {
		opacity: 0.6;
		cursor: not-allowed;
	}

	.journey-subscribe-btn {
		padding: 11px 0;
		font-size: 0.9rem;
		font-weight: 600;
		color: #3d7a96;
		background: #ffffff;
		border: none;
		border-radius: 50px;
		cursor: pointer;
		transition: all 0.3s ease;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
	}

	.journey-subscribe-btn:hover:not(:disabled) {
		background: rgba(255, 255, 255, 0.9);
		transform: translateY(-2px);
	}

	.journey-subscribe-btn:disabled {
		opacity: 0.7;
		cursor: not-allowed;
	}

	.success-journey {
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
		gap: 8px;
	}

	.success-journey p {
		color: rgba(255, 255, 255, 0.9);
	}

	.spinner {
		width: 18px;
		height: 18px;
		border: 2px solid rgba(255, 255, 255, 0.3);
		border-top-color: white;
		border-radius: 50%;
		animation: spin 0.8s linear infinite;
	}

	@keyframes spin {
		to { transform: rotate(360deg); }
	}

	.success-message {
		text-align: center;
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
		color: #4a5e73;
		margin: 0;
	}

	@keyframes fadeInUp {
		from { opacity: 0; transform: translateY(20px); }
		to { opacity: 1; transform: translateY(0); }
	}

	.checkmark-circle {
		width: 72px;
		height: 72px;
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
		to { stroke-dashoffset: 0; }
	}

	@keyframes strokeCheck {
		to { stroke-dashoffset: 0; }
	}

	/* ===== JOURNEY / FOOTER SECTION ===== */
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
		fill: #c8dde9;
	}

	.journey-container {
		width: 100%;
		max-width: 1100px;
		padding: 50px 40px 80px 40px;
		box-sizing: border-box;
		opacity: 0;
		transform: translateY(30px);
		transition: opacity 0.7s ease, transform 0.7s ease;
	}

	.journey-container.visible {
		opacity: 1;
		transform: translateY(0);
	}

	.journey-title {
		text-align: center;
		font-size: 3rem;
		font-weight: 700;
		color: #ffffff;
		margin: 0 0 14px 0;
		line-height: 1.15;
	}

	.journey-subtitle {
		text-align: center;
		font-size: 1.1rem;
		color: rgba(255, 255, 255, 0.85);
		margin: 0 0 48px 0;
		line-height: 1.6;
	}

	.journey-grid {
		display: flex;
		gap: 24px;
		align-items: stretch;
	}

	.journey-column {
		flex: 1;
		display: flex;
		flex-direction: column;
	}

	/* Left: 3 cards — fixed gap, stack from top */
	.left-column {
		gap: 20px;
		justify-content: flex-start;
	}

	/* Right: 3 cards — gaps grow to match left column height */
	.right-column {
		justify-content: space-between;
	}

	.journey-card {
		padding: 22px 24px;
		border-radius: 20px;
		background: rgba(255, 255, 255, 0.1);
		backdrop-filter: blur(20px);
		-webkit-backdrop-filter: blur(20px);
		border: 1px solid rgba(255, 255, 255, 0.18);
		box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
		transition: transform 0.35s ease, box-shadow 0.35s ease;
		display: flex;
		flex-direction: column;
	}

	.journey-card:hover {
		transform: translateY(-5px);
		box-shadow: 0 12px 36px rgba(0, 0, 0, 0.22);
	}

	/* card-body: natural spacing, no stretching */
	.card-body {
		display: flex;
		flex-direction: column;
		gap: 18px;
	}

	.card-header {
		display: flex;
		align-items: center;
		gap: 12px;
		margin-bottom: 16px;
	}

	.journey-card .card-icon {
		font-size: 1.6rem;
		line-height: 1;
	}

	.journey-card h3 {
		font-size: 1.25rem;
		font-weight: 700;
		color: #ffffff;
		margin: 0;
	}

	.journey-card h4 {
		font-size: 1rem;
		font-weight: 600;
		color: #ffffff;
		margin: 0 0 4px 0;
	}

	.journey-card p {
		font-size: 0.9rem;
		line-height: 1.55;
		color: rgba(255, 255, 255, 0.85);
		margin: 0;
	}

	/* Logo items — shared across experience, education, project */
	.with-logo {
		display: flex;
		align-items: center;
		gap: 12px;
		border-left: none !important;
		padding-left: 0 !important;
	}

	.item-logo {
		width: 38px;
		height: 38px;
		border-radius: 50%;
		object-fit: cover;
		flex-shrink: 0;
		border: 1.5px solid rgba(255, 255, 255, 0.25);
		background: rgba(255, 255, 255, 0.08);
	}

	.item-logo.logo-white-bg {
		background: #ffffff;
	}

	.item-text {
		flex: 1;
		min-width: 0;
	}

	/* Experience */
	.experience-item {
		padding-left: 12px;
		border-left: 2px solid rgba(255, 255, 255, 0.2);
	}

	.experience-item .company {
		font-size: 0.82rem;
		color: rgba(255, 255, 255, 0.6);
		font-weight: 500;
	}

	.experience-item .description {
		font-size: 0.86rem;
		color: rgba(255, 255, 255, 0.8);
	}

	.cv-actions {
		margin-top: 16px;
		display: flex;
		flex-wrap: wrap;
		gap: 10px;
	}

	.cv-btn {
		padding: 9px 22px;
		font-size: 0.88rem;
		font-weight: 600;
		color: #ffffff;
		background: rgba(255, 255, 255, 0.12);
		border: 1px solid rgba(255, 255, 255, 0.25);
		border-radius: 50px;
		cursor: pointer;
		transition: all 0.3s ease;
		display: inline-flex;
		align-items: center;
		gap: 8px;
	}

	.cv-btn:hover {
		background: rgba(255, 255, 255, 0.2);
		transform: translateY(-2px);
	}

	.linkedin-glass-btn {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		width: 38px;
		height: 38px;
		border-radius: 999px;
		background: rgba(255, 255, 255, 0.16);
		backdrop-filter: blur(18px);
		-webkit-backdrop-filter: blur(18px);
		border: 1px solid rgba(255, 255, 255, 0.35);
		color: #ffffff;
		cursor: pointer;
		transition: all 0.3s ease;
		text-decoration: none;
	}

	.linkedin-glass-btn:hover {
		background: rgba(255, 255, 255, 0.26);
		transform: translateY(-2px) scale(1.03);
		box-shadow: 0 10px 28px rgba(0, 0, 0, 0.25);
	}

	.linkedin-glass-btn svg {
		width: 18px;
		height: 18px;
	}

	/* Education */
	.education-item {
		padding-left: 12px;
		border-left: 2px solid rgba(255, 255, 255, 0.2);
	}

	.education-item .degree {
		font-size: 0.82rem;
		color: rgba(255, 255, 255, 0.6);
		margin-bottom: 3px;
		font-weight: 500;
	}

	.education-item .honor {
		font-size: 0.82rem;
		color: rgba(255, 255, 255, 0.8);
		font-style: italic;
	}

	/* Projects */
	.project-item {
		padding-left: 12px;
		border-left: 2px solid rgba(255, 255, 255, 0.2);
	}

	.project-item h4 {
		margin-bottom: 4px;
	}

	.project-item p {
		font-size: 0.86rem;
		color: rgba(255, 255, 255, 0.8);
	}

	/* Skills */
	.skills-section {
		display: flex;
		flex-direction: column;
		gap: 18px;
	}

	.skill-group h4 {
		margin-bottom: 10px;
		font-size: 0.92rem;
	}

	.skill-tags {
		display: flex;
		flex-wrap: wrap;
		gap: 8px;
	}

	.skill-tag {
		display: inline-block;
		padding: 5px 14px;
		background: rgba(255, 255, 255, 0.12);
		border: 1px solid rgba(255, 255, 255, 0.2);
		border-radius: 50px;
		font-size: 0.82rem;
		color: #ffffff;
		font-weight: 500;
		transition: all 0.25s ease;
	}

	.skill-tag:hover {
		background: rgba(255, 255, 255, 0.22);
		transform: translateY(-2px);
	}

	.skill-tag.interest {
		background: rgba(255, 255, 255, 0.08);
		border-color: rgba(255, 255, 255, 0.15);
	}

	.project-link {
		color: rgba(255, 255, 255, 0.85);
		text-decoration: underline;
		text-underline-offset: 3px;
		text-decoration-color: rgba(255, 255, 255, 0.35);
		transition: color 0.2s ease, text-decoration-color 0.2s ease;
	}

	.project-link:hover {
		color: #ffffff;
		text-decoration-color: rgba(255, 255, 255, 0.8);
	}

	/* ===== CONTACT SECTION ===== */
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
		stroke: rgba(0, 0, 0, 0.08);
		stroke-width: 3;
		filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.1));
		transform: translateY(2px);
	}

	.wave-fill-contact {
		fill: #e8f4f8;
	}

	.contact-container {
		width: 100%;
		max-width: 1100px;
		margin: 0 auto;
		padding: 0 40px 40px 40px;
		box-sizing: border-box;
		opacity: 0;
		transform: translateY(30px);
		transition: opacity 0.7s ease, transform 0.7s ease;
	}

	.contact-container.visible {
		opacity: 1;
		transform: translateY(0);
	}

	.contact-content {
		display: flex;
		align-items: center;
		gap: 64px;
	}

	.contact-left {
		flex-shrink: 0;
	}

	.contact-image-wrapper {
		width: 320px;
		height: 380px;
		border-radius: 24px;
		overflow: hidden;
		box-shadow:
			0 20px 50px rgba(61, 122, 150, 0.2),
			0 8px 20px rgba(0, 0, 0, 0.1);
		border: 3px solid rgba(255, 255, 255, 0.9);
		transition: transform 0.4s ease;
	}

	.contact-image-wrapper:hover {
		transform: translateY(-6px) rotate(-1deg);
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
		font-size: 2.75rem;
		font-weight: 700;
		color: #1a365d;
		margin: 0 0 16px 0;
		line-height: 1.15;
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
		50% { opacity: 0; }
	}

	.contact-description {
		font-size: 1.05rem;
		line-height: 1.8;
		color: #4a5e73;
		margin: 0 0 28px 0;
	}

	.contact-info {
		display: flex;
		flex-direction: column;
		gap: 14px;
		margin-bottom: 28px;
	}

	.contact-item {
		display: flex;
		align-items: center;
		gap: 12px;
		font-size: 1rem;
		color: #374a5e;
		text-decoration: none;
		transition: color 0.2s ease;
	}

	a.contact-item:hover {
		color: #4a8aa8;
	}

	.contact-icon-wrapper {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 38px;
		height: 38px;
		border-radius: 10px;
		background: rgba(74, 138, 168, 0.1);
		flex-shrink: 0;
	}

	.contact-icon {
		width: 18px;
		height: 18px;
		color: #4a8aa8;
		flex-shrink: 0;
	}

	.social-links {
		display: flex;
		gap: 12px;
	}

	.social-link {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 44px;
		height: 44px;
		border-radius: 12px;
		background: rgba(74, 138, 168, 0.08);
		border: 1px solid rgba(74, 138, 168, 0.12);
		color: #4a8aa8;
		transition: all 0.3s ease;
	}

	.social-link:hover {
		background: linear-gradient(135deg, #4a8aa8 0%, #3d7a96 100%);
		color: white;
		transform: translateY(-3px);
		box-shadow: 0 6px 16px rgba(74, 138, 168, 0.3);
		border-color: transparent;
	}

	.social-link svg {
		width: 20px;
		height: 20px;
	}

	.contact-footer {
		margin-top: 48px;
		padding-top: 20px;
		border-top: 1px solid rgba(74, 138, 168, 0.15);
		text-align: center;
	}

	.contact-footer p {
		font-size: 0.85rem;
		color: #8a9bb0;
		margin: 0;
	}

	/* ===== RESPONSIVE ===== */
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

		.about-content {
			gap: 40px;
		}

		.about-image-wrapper {
			width: 260px;
			height: 340px;
		}

		.about-title, .blog-title, .journey-title, .contact-title {
			font-size: 2.5rem;
		}

		.journey-grid {
			flex-direction: column;
		}

		.journey-column {
			flex: none;
		}

		/* When stacked, both columns revert to a normal fixed gap */
		.left-column,
		.right-column {
			justify-content: flex-start;
			gap: 20px;
		}

		.contact-content {
			gap: 40px;
		}

		.contact-image-wrapper {
			width: 260px;
			height: 320px;
		}

		.blog-cards {
			grid-template-columns: repeat(2, 1fr);
		}

	}

	@media (max-width: 768px) {
		.container {
			padding: 0 20px;
			height: auto;
			min-height: auto;
			display: flex;
			flex-direction: column;
			align-items: center;
			padding-top: 100px;
			padding-bottom: 40px;
			gap: 32px;
		}

		.image-gallery {
			flex-wrap: wrap;
			justify-content: center;
			gap: 16px;
			min-height: auto;
			padding: 30px 20px 100px;
		}

		.image-wrapper {
			max-width: 140px;
			margin: 0;
			border-radius: 14px;
		}

		.image-wrapper img {
			height: 190px;
			border-radius: 14px;
		}

		.about-section {
			padding: 60px 24px 50px 24px;
		}

		.about-content {
			flex-direction: column-reverse;
			text-align: center;
		}

		.section-label {
			padding-left: 0;
		}

		.section-label::before {
			display: none;
		}

		.about-image-wrapper {
			width: 220px;
			height: 280px;
		}

		.about-title, .blog-title, .journey-title {
			font-size: 2.25rem;
		}

		.about-body {
			font-size: 1rem;
		}

		.content-section {
			padding: 0 24px 60px;
		}

		.blog-cards {
			grid-template-columns: 1fr;
			gap: 20px;
		}

		.blog-subtitle {
			font-size: 1rem;
		}

		.journey-title {
			font-size: 2.25rem;
		}

		.journey-subtitle {
			font-size: 1rem;
			margin-bottom: 32px;
		}

		.journey-container {
			padding: 40px 24px 60px;
		}

		.journey-card {
			padding: 22px;
		}

		.journey-card h3 {
			font-size: 1.15rem;
		}

		.journey-card h4 {
			font-size: 0.95rem;
		}

		.contact-container {
			padding: 0 24px 30px 24px;
		}

		.contact-content {
			flex-direction: column;
			text-align: center;
		}

		.contact-image-wrapper {
			width: 220px;
			height: 280px;
		}

		.contact-title {
			font-size: 2rem;
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

		.random-things {
			margin-top: 40px;
		}

		.random-things-title {
			font-size: 1.2rem;
		}

		.carousel-item {
			padding: 8px 18px;
			font-size: 0.88rem;
		}

		.carousel-track {
			gap: 20px;
		}

		.wave-divider svg,
		.wave-divider-bottom svg,
		.wave-divider-contact svg {
			height: 60px;
		}

		.cv-actions {
			flex-direction: column;
			align-items: flex-start;
		}
	}

	@media (max-width: 480px) {
		.container {
			padding-top: 80px;
			gap: 24px;
		}

		.image-gallery {
			gap: 10px;
			min-height: auto;
			padding: 20px 12px 80px;
		}

		.image-wrapper {
			max-width: 100px;
			border-radius: 10px;
		}

		.image-wrapper img {
			height: 130px;
			border-radius: 10px;
		}

		.image-wrapper.tilt-left {
			transform: rotate(-2deg);
		}

		.image-wrapper.tilt-right {
			transform: rotate(2deg);
		}

		.about-section {
			padding: 40px 16px 36px 16px;
		}

		.about-image-wrapper {
			width: 180px;
			height: 230px;
		}

		.about-title, .blog-title {
			font-size: 1.875rem;
		}

		.about-body {
			font-size: 0.95rem;
			line-height: 1.7;
		}

		.content-section {
			padding: 0 16px 50px;
		}

		.blog-subtitle {
			font-size: 0.9rem;
		}

		.journey-container {
			padding: 32px 16px 50px 16px;
		}

		.journey-title {
			font-size: 1.875rem;
		}

		.journey-card {
			padding: 18px;
		}

		.journey-card .card-icon {
			font-size: 1.4rem;
		}

		.journey-card h3 {
			font-size: 1.1rem;
		}

		.journey-card h4 {
			font-size: 0.9rem;
		}

		.item-logo {
			width: 32px;
			height: 32px;
		}

		.skill-tags {
			gap: 6px;
		}

		.skill-tag {
			padding: 4px 11px;
			font-size: 0.78rem;
		}

		.contact-container {
			padding: 0 16px 24px 16px;
		}

		.contact-image-wrapper {
			width: 180px;
			height: 230px;
		}

		.contact-title {
			font-size: 1.75rem;
		}

		.contact-description {
			font-size: 0.95rem;
			line-height: 1.7;
		}

		.social-link {
			width: 40px;
			height: 40px;
		}

		.social-link svg {
			width: 18px;
			height: 18px;
		}

		.contact-footer {
			margin-top: 28px;
		}

		.carousel-item {
			padding: 7px 14px;
			font-size: 0.82rem;
		}

		.carousel-track {
			gap: 14px;
			animation-duration: 30s;
		}

		.wave-divider svg,
		.wave-divider-bottom svg,
		.wave-divider-contact svg {
			height: 40px;
		}
	}
</style>
