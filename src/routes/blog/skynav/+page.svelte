<script>
	import { onMount } from 'svelte';
	import Header from '$lib/components/Header.svelte';

	let expanded = false;
	let heroVisible = false;
	let contentVisible = false;

	function toggleNav() {
		expanded = !expanded;
	}

	onMount(() => {
		setTimeout(() => { heroVisible = true; }, 100);
		setTimeout(() => { contentVisible = true; }, 400);
	});
</script>

<svelte:head>
	<title>SkyNav: Building AI for the Elderly — Ibrahim Mohsin</title>
	<link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600&display=swap" rel="stylesheet" />
</svelte:head>

<Header {expanded} {toggleNav} />

<article class="post">

	<!-- ===== BANNER ===== -->
	<div class="banner" class:visible={heroVisible}>
		<img src="/skynav_blog.JPG" alt="The SkyNav team in Asheville, North Carolina" class="banner-img" />
		<div class="banner-overlay"></div>
		<div class="banner-content">
			<span class="post-tag professional">Professional</span>
			<h1 class="banner-title">SkyNav: Building AI for the Elderly</h1>
			<p class="banner-sub">How our team designed and built an AI platform to improve accessibility and information access for aging populations in Western NC.</p>
			<div class="banner-meta">
				<span>July 2025</span>
				<span class="dot">&middot;</span>
				<span>Ibrahim Mohsin</span>
			</div>
		</div>
	</div>

	<!-- ===== BODY ===== -->
	<div class="body-wrap" class:visible={contentVisible}>

		<!-- Intro -->
		<section class="prose-section">
			<p class="lead">Last week I came back from spending two months in Asheville, North Carolina where I, alongside three other Morehead-Cain peers, were tasked with building AI that could best serve the needs of the aging population. Initially, when I read the problem statement for the summer, I certainly had my questions and reservations. Aging populations? Government agencies? Western North Carolina? It felt so far removed from the startup and tech world I was used to.</p>

			<blockquote class="pull-quote">In the end, that distance proved to be a truly amazing experience.</blockquote>

			<p>The Morehead-Cain Civic Collaboration program sends rising sophomores and juniors into regional communities for eight weeks to work alongside local partners on real-world problems. My team — Sofia, Harsehaj, and Walter — was paired with the Land of Sky Regional Council and their Area Agency on Aging (AAA). These were communities that had just been hit hard by Hurricane Helene, and the agency was already stretched thin, facing staffing shortages and a surge in service demand at the same time.</p>

			<p>The problem we were asked to solve was straightforward on the surface but deeply complex as we interviewed over 30 specialists, caregivers, and other stakeholders alike: older adults and their caregivers often had no idea what resources were available to them, and when they did go looking, they'd spend hours bouncing between phone calls, departments, and dead ends. Meanwhile, agency staff were so overwhelmed fielding basic inquiries that they had little bandwidth for anything else.</p>
		</section>

		<div class="media-full">
			<img src="/landofsky_photo.jpg" alt="The SkyNav team at the Land of Sky Regional Council" />
			<p class="caption">Our team at the Land of Sky Regional Council offices in Asheville.</p>
		</div>

		<!-- The First Eight Weeks -->
		<section class="prose-section">
			<h2 class="section-heading"><span class="heading-accent"></span> The First Eight Weeks</h2>

			<p>We spent the first two weeks almost entirely away from our laptops. Instead of jumping into building, we focused on customer discovery — conducting interviews with caregivers, AAA staff, and community members to understand the problem and what our target audience was really looking for. This was humbling. None of us were caregivers. None of us knew the problems these individuals faced every single day.</p>

			<p>What we heard was consistent: caregivers didn't need another app or password to remember. They needed something simple, immediate, and human. Many of the people we were trying to serve weren't going to download anything or create an account. They just needed answers.</p>

			<p>By week three, we had a clear direction and brought our proposed solution to the government administration for feedback. What we built over the following four weeks was <strong>SkyNav</strong>, an SMS-first, AI-powered care navigation service. The concept was simple: a caregiver or older adult sends a text message, and the system connects them directly to the state and regional resources best suited for their specific situation, routing them to the right specialists without the endless back-and-forth of navigating the system manually. No app, no login, no learning curve. Just a text message.</p>

			<p>On the backend, we also used AI to automate much of the agency's internal organization — conversation tracking, resource referral logging, and interdepartmental communication about calls and client needs. Work that had previously taken up hours of staff time each week was suddenly running on its own.</p>
		</section>

		<div class="media-full">
			<img src="/landofsky_nathan.JPG" alt="Working with the Land of Sky team" />
			<p class="caption">Our team with Nathan, the Director of the Land of Sky Regional Council.</p>
		</div>

		<section class="prose-section">
			<p>The final week was spent polishing the product and presenting to the Land of Sky Regional Council. Standing in front of regional leaders and watching them engage seriously with something we had built from scratch in under two months was one of the more surreal and rewarding moments I've had.</p>
		</section>

		<div class="media-full">
			<img src="/landofsky_presenting.jpg" alt="Presenting SkyNav to the Land of Sky Regional Council" />
			<p class="caption">Presenting SkyNav to the Land of Sky Regional Council and Area Agency on Aging leadership.</p>
		</div>

		<!-- What I Didn't Expect -->
		<section class="prose-section">
			<h2 class="section-heading"><span class="heading-accent"></span> What I Didn't Expect</h2>

			<p>Asheville gave me the best work-life balance I have ever experienced. There is something clarifying about working on a problem that is concrete, local, and urgent — where you can truly see the impact and desire to help within the local community. The problem was real and the people affected by it were sitting across from us. I left the office each day feeling like the work actually mattered, which is not something I have always been able to say.</p>
		</section>

		<div class="media-full">
			<img src="/asheville_cookout.JPG" alt="Team cookout in Asheville" />
			<p class="caption">Team cookout in Asheville.</p>
		</div>

		<section class="prose-section">
			<p>The moment that has stuck with me most came during our very first week of interviews. We sat down with a 95+-year-old woman to understand her experience navigating care resources and her experience living in Western North Carolina. I went in with low expectations, honestly — I assumed the conversation would likely confirm what I already believed, that technology and this demographic simply didn't mix.</p>

			<p>Instead, she told us that she uses AI every single day. <em>Every day.</em> She told us stories about how she uses Photoshop to edit her photos of local birds she finds — her favorite pastime — and how she uses AI to help plan out her daily errands. It was truly amazing to see in this interaction, and through the summer, how technology can genuinely make a real impact in the lives of every single person.</p>

			<blockquote class="pull-quote">It simply has to be built in the right way.</blockquote>
		</section>

		<div class="media-full">
			<img src="/landofsky_aging.jpg" alt="Meeting with aging population stakeholders" />
			<p class="caption">Meeting with caregivers and community stakeholders during the discovery phase.</p>
		</div>

		<!-- What I'm Taking Away -->
		<section class="prose-section">
			<h2 class="section-heading"><span class="heading-accent"></span> What I'm Taking Away</h2>

			<p>A few things from this summer will stick with me for a long time.</p>

			<p><strong>First, civic technology is something I want more experience in.</strong> There is an enormous amount of meaningful, technically interesting work to be done in spaces that the private sector tends to ignore. Government agencies, nonprofits, and under-resourced communities are not problems too old or too analog for good technology — they are just waiting for people willing to show up, be patient, and build for them.</p>

			<p><strong>Second, learning the user is crucial.</strong> We could have spent eight weeks building our initial idea of a web app we thought was useful that nobody used. The two weeks we invested upfront in actually talking to caregivers and agency staff shaped every decision we made after that, and I genuinely believe SkyNav is a better and more sustainable product because of it.</p>

			<p><strong>Third, an efficient team is everything.</strong> Four people, eight weeks, a tight scope, and clear trust in each other made this project work. We were able to efficiently delegate tasks to each other, have trust we would get our work done, and were able to move really fast, truly accomplishing a lot within the eight weeks.</p>
		</section>

		<!-- Closing -->
		<section class="prose-section closing">
			<blockquote class="pull-quote closing-quote">This summer reminded me that technology doesn't have limits on who it can help. I came to Asheville with reservations and left with one of the most meaningful experiences I've had building.</blockquote>

			<p>I'm grateful to the Land of Sky Regional Council, to LeeAnne Tucker and her team at the AAA, and to the community members who trusted four college students enough to let us try.</p>

			<div class="signature">
				<span class="signature-text">Ibrahim Mohsin</span>
			</div>
		</section>

		<!-- Back link -->
		<div class="back-bar">
			<a href="/blog" class="back-link">
				<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
					<path d="M19 12H5M5 12l7-7M5 12l7 7"/>
				</svg>
				Back to Blog
			</a>
		</div>

	</div><!-- /body-wrap -->

	<footer class="post-footer">
		<p>&copy; 2026 Ibrahim Mohsin. All rights reserved.</p>
	</footer>

</article>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
		font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
		background: #f0f6f9;
	}

	.post {
		min-height: 100vh;
	}

	/* ===== BANNER ===== */
	.banner {
		position: relative;
		width: 100%;
		height: 90vh;
		min-height: 560px;
		overflow: hidden;
		opacity: 0;
		transition: opacity 0.9s ease;
	}

	.banner.visible {
		opacity: 1;
	}

	.banner-img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		object-position: center 35%;
		transform: scale(1.04);
		transition: transform 6s ease;
	}

	.banner.visible .banner-img {
		transform: scale(1);
	}

	.banner-overlay {
		position: absolute;
		inset: 0;
		background: linear-gradient(
			to bottom,
			rgba(26, 54, 93, 0.25) 0%,
			rgba(26, 54, 93, 0.5) 60%,
			rgba(26, 54, 93, 0.75) 100%
		);
	}

	.banner-content {
		position: absolute;
		bottom: 80px;
		left: 0;
		right: 0;
		max-width: 860px;
		margin: 0 auto;
		padding: 0 48px;
		color: #ffffff;
	}

	.post-tag {
		display: inline-block;
		font-size: 0.72rem;
		font-weight: 700;
		letter-spacing: 1.5px;
		text-transform: uppercase;
		padding: 5px 14px;
		border-radius: 50px;
		margin-bottom: 18px;
	}

	.post-tag.professional {
		background: rgba(74, 138, 168, 0.2);
		color: #93c5e0;
		border: 1px solid rgba(74, 138, 168, 0.3);
	}

	.banner-title {
		font-size: clamp(3rem, 8vw, 5.5rem);
		font-weight: 800;
		margin: 0 0 12px 0;
		line-height: 1.0;
		letter-spacing: -0.02em;
		text-shadow: 0 2px 16px rgba(0, 0, 0, 0.4);
	}

	.banner-sub {
		font-size: 1.2rem;
		color: rgba(255, 255, 255, 0.82);
		margin: 0 0 16px 0;
		font-style: italic;
		max-width: 640px;
	}

	.banner-meta {
		display: flex;
		align-items: center;
		gap: 10px;
		font-size: 0.9rem;
		color: rgba(255, 255, 255, 0.65);
		font-weight: 500;
	}

	.dot {
		opacity: 0.5;
	}

	/* ===== BODY ===== */
	.body-wrap {
		background: #f0f6f9;
		opacity: 0;
		transform: translateY(20px);
		transition: opacity 0.7s ease, transform 0.7s ease;
	}

	.body-wrap.visible {
		opacity: 1;
		transform: translateY(0);
	}

	/* ===== PROSE ===== */
	.prose-section {
		max-width: 720px;
		margin: 0 auto;
		padding: 52px 24px 0;
	}

	.prose-section.closing {
		padding-bottom: 60px;
	}

	.lead {
		font-size: 1.2rem;
		line-height: 1.8;
		color: #1a365d;
		font-weight: 500;
		margin: 0 0 28px 0;
	}

	p {
		font-size: 1.05rem;
		line-height: 1.85;
		color: #2d4a5e;
		margin: 0 0 24px 0;
	}

	strong {
		color: #1a365d;
		font-weight: 700;
	}

	em {
		color: #3d7a96;
	}

	/* ===== PULL QUOTE ===== */
	.pull-quote {
		margin: 36px 0;
		padding: 24px 32px;
		border-left: 4px solid #4a8aa8;
		background: rgba(74, 138, 168, 0.06);
		border-radius: 0 12px 12px 0;
		font-size: 1.25rem;
		font-style: italic;
		line-height: 1.7;
		color: #1a365d;
		font-weight: 500;
	}

	.closing-quote {
		font-size: 1.3rem;
		border-left-color: #3d7a96;
		background: rgba(61, 122, 150, 0.07);
	}

	/* ===== SECTION HEADINGS ===== */
	.section-heading {
		display: flex;
		align-items: center;
		gap: 14px;
		font-size: 1.65rem;
		font-weight: 700;
		color: #1a365d;
		margin: 0 0 24px 0;
	}

	.heading-accent {
		display: inline-block;
		width: 28px;
		height: 3px;
		background: linear-gradient(90deg, #4a8aa8, #6ba3c0);
		border-radius: 2px;
		flex-shrink: 0;
	}

	/* ===== MEDIA — full bleed ===== */
	.media-full {
		max-width: 960px;
		margin: 52px auto 0;
		padding: 0 24px;
	}

	.media-full img {
		width: 100%;
		border-radius: 16px;
		display: block;
		object-fit: cover;
		max-height: 560px;
		box-shadow: 0 8px 32px rgba(0, 0, 0, 0.12);
	}

	/* ===== CAPTION ===== */
	.caption {
		font-size: 0.82rem !important;
		color: #8a9bb0 !important;
		text-align: center;
		margin: 10px 0 0 0 !important;
		font-style: italic;
		line-height: 1.5 !important;
	}

	/* ===== SIGNATURE ===== */
	.signature {
		margin-top: 48px;
		text-align: right;
	}

	.signature-text {
		font-family: 'Dancing Script', cursive;
		font-size: 2rem;
		font-weight: 600;
		color: #1a365d;
		opacity: 0.85;
	}

	/* ===== BACK BAR ===== */
	.back-bar {
		max-width: 720px;
		margin: 60px auto 0;
		padding: 0 24px 60px;
		border-top: 1px solid rgba(74, 138, 168, 0.15);
		padding-top: 32px;
	}

	.back-link {
		display: inline-flex;
		align-items: center;
		gap: 8px;
		font-size: 0.9rem;
		font-weight: 600;
		color: #4a8aa8;
		text-decoration: none;
		transition: color 0.2s ease;
	}

	.back-link:hover {
		color: #3d7a96;
	}

	.back-link svg {
		transition: transform 0.2s ease;
	}

	.back-link:hover svg {
		transform: translateX(-3px);
	}

	/* ===== FOOTER ===== */
	.post-footer {
		padding: 20px 48px;
		border-top: 1px solid rgba(74, 138, 168, 0.12);
		background: #f0f6f9;
		text-align: center;
	}

	.post-footer p {
		font-size: 0.85rem;
		color: #8a9bb0;
		margin: 0;
	}

	/* ===== RESPONSIVE ===== */
	@media (max-width: 768px) {
		.banner {
			height: 70vh;
		}

		.banner-content {
			bottom: 48px;
			padding: 0 24px;
		}

		.banner-title {
			font-size: 2.75rem;
		}

		.banner-sub {
			font-size: 1rem;
		}

		.prose-section {
			padding: 40px 20px 0;
		}

		.lead {
			font-size: 1.1rem;
		}

		p {
			font-size: 1rem;
		}

		.pull-quote {
			font-size: 1.1rem;
			padding: 20px 24px;
			margin: 28px 0;
		}

		.media-full {
			padding: 0 16px;
			margin-top: 40px;
		}

		.section-heading {
			font-size: 1.4rem;
		}

		.back-bar {
			padding: 28px 20px 48px;
		}

		.signature-text {
			font-size: 1.7rem;
		}
	}

	@media (max-width: 480px) {
		.banner {
			height: 55vh;
		}

		.banner-content {
			bottom: 32px;
			padding: 0 16px;
		}

		.banner-title {
			font-size: 2.2rem;
		}

		.banner-sub {
			font-size: 0.9rem;
		}

		.banner-meta {
			font-size: 0.8rem;
		}

		.prose-section {
			padding: 32px 16px 0;
		}

		.lead {
			font-size: 1rem;
		}

		p {
			font-size: 0.95rem;
		}

		.pull-quote {
			font-size: 1rem;
			padding: 16px 20px;
			margin: 24px 0;
		}

		.section-heading {
			font-size: 1.25rem;
		}

		.media-full {
			padding: 0 12px;
			margin-top: 32px;
		}

		.media-full img {
			border-radius: 12px;
			max-height: 400px;
		}

		.back-bar {
			padding: 24px 16px 40px;
		}

		.post-footer {
			padding: 16px 16px;
		}

		.signature-text {
			font-size: 1.5rem;
		}
	}
</style>
