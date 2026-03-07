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
	<title>Building the Plane as it Flies — Ibrahim Mohsin</title>
	<link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600&display=swap" rel="stylesheet" />
</svelte:head>

<Header {expanded} {toggleNav} />

<article class="post">

	<!-- ===== BANNER ===== -->
	<div class="banner" class:visible={heroVisible}>
		<img src="/workly_blog_cover.jpg" alt="Workly — Building the Plane" class="banner-img" />
		<div class="banner-overlay"></div>
		<div class="banner-content">
			<span class="post-tag startup">Startup</span>
			<h1 class="banner-title">Building the Plane as it Flies</h1>
			<p class="banner-sub">Lessons learned launching my first venture: the chaos, the pivots, and what I'd do differently.</p>
			<div class="banner-meta">
				<span>December 2025</span>
				<span class="dot">&middot;</span>
				<span>Ibrahim Mohsin</span>
			</div>
		</div>
	</div>

	<!-- ===== BODY ===== -->
	<div class="body-wrap" class:visible={contentVisible}>

		<!-- Intro -->
		<section class="prose-section">
			<p class="lead">Over the past year, alongside my freshman year suitemate Blake Mechels, Torrey Lin as our creative director, and Charlie Ashcroft, our head of growth at CU Boulder, I had been working on Workly, a mobile platform dedicated to connecting local households to hardworking college students for everyday jobs and gig tasks.</p>

			<p>Two months into our launch, we had reached hundreds of households, students, and even businesses, helping users complete all kinds of tasks from cleaning gutters, babysitting pets, knitting quilts, lawn mowing, moving and building furniture, and so much more.</p>
		</section>

		<div class="media-full">
			<img src="/workly_founders.jpg" alt="The Workly founding team" />
			<p class="caption">The Original Workly Founders: Ibrahim and Blake</p>
		</div>

		<section class="prose-section">
			<h2 class="section-heading"><span class="heading-accent"></span> The Origin Story</h2>

			<p>The idea came about the September of my freshman year as I talked with Blake about drafting up our trademark "Dog Plan" — what we coined our pathway to gain real professional experience, startup traction, and the goals and dreams we collectively hoped to accomplish.</p>

			<p>It was in drafting this "Dog Plan" that I first learned about Blake's incredible high school experience of founding "High Schoolers 4 Hire," his hometown business that hired 40+ of his peers and did $35,000+ in revenue helping households around the neighborhood with whatever their odd job needs were, building community and getting things done.</p>

			<blockquote class="pull-quote">Coming from a computer science background, my immediate first thought was, "Why stop there?"</blockquote>

			<p>Manually scheduling jobs, coordinating contractors, and conducting outreach was, without saying, unscalable. With Blake's past experience managing the business and my experience building across robotics, e-commerce, and other user applications, we decided to co-found what we eventually named Workly.</p>

			<p>Ultimately, with some notable delays and setbacks, we followed through, built, and launched the platform ourselves from scratch, helping hundreds across the nation along the way. Being the first consumer venture I have officially launched in this way, I now take away some significant lessons about venture creation and growth that I will carry with me in all my future endeavors. Here are some of the most significant ones.</p>
		</section>

		<div class="media-video">
			<video autoplay muted loop playsinline preload="metadata">
				<source src="/workly_timelapse.MOV" type="video/mp4" />
			</video>
			<p class="caption">A timelapse of building our Workly slide deck.</p>
		</div>

		<!-- Lesson 1 -->
		<section class="prose-section">
			<h2 class="section-heading"><span class="heading-accent"></span> More is Not Always Better</h2>

			<p>In launching Workly, my co-founders and I quickly fell into the trap of thinking more was going to be better. More users, more active markets, more features, more platforms, more people on the team — more, more, more. From the very beginning, rather than deeply understanding the users we already had, we were focused on expanding. We launched simultaneously at CU Boulder and UNC Chapel Hill before we had even come close to perfecting the experience at our home market, spreading our attention thin before we had earned the right to grow.</p>

			<p>The pattern continued. We began developing an AI-powered phone line targeted at older users who lacked app experience — a genuinely interesting idea — but we built it almost entirely without conducting real user research on that demographic first. We were solving a problem we assumed existed rather than one we had validated. Meanwhile, our core app still had plenty of rough edges that our existing users were running into every day, and instead of stopping to fix them, we kept chasing new users to add to the top of a leaky bucket.</p>

			<blockquote class="pull-quote">The lesson we learned the hard way is a simple one: growth means nothing if the foundation isn't solid. More users won't save a product that isn't working for the users you already have.</blockquote>
		</section>

		<div class="media-full">
			<img src="/Workly_pitch_comp_1.jpg" alt="Ibrahim pitching Workly at a competition" />
			<p class="caption">Presenting Workly at UNC's annual Carolina Pitch Fest</p>
		</div>

		<!-- Lesson 2 -->
		<section class="prose-section">
			<h2 class="section-heading"><span class="heading-accent"></span> The Customer is Always Right</h2>

			<p>An adage as old as time. Stemming from Blake's high school experience connecting local households with students looking for work, we locked ourselves into college students as the foundation of our platform early on and never seriously questioned it. It felt like our identity. But even as we frequently ran into the same problems — students being unreliable, inflexible, or simply unavailable — we kept pushing forward with the same model. Some households waited days to hear back on a job request or struggled to get something scheduled at all, and rather than treating that as a signal worth addressing, we tried to brute force our way through it with more users and more volume.</p>

			<p>Looking back, we likely should have opened the worker side of our platform beyond students far sooner. Working several jobs ourselves and speaking directly with customers, the values they cared about most were clear: responsiveness, efficiency, and quality work. At times, students as workers simply couldn't consistently deliver on those things — not out of bad intent, but because of the natural realities of their schedules and commitments.</p>

			<blockquote class="pull-quote">A broader, more diverse worker base may have allowed us to actually meet the standard our customers expected, rather than asking them to work around the limitations of ours. We were so attached to the original vision that we failed to notice the original vision was holding us back.</blockquote>
		</section>

		<div class="media-split">
			<div class="split-item">
				<img src="/Workly_club_pitch.jpg" alt="Pitching Workly at a club event" />
				<p class="caption">Presenting Workly to 80+ entrepreneurship students at UNC.</p>
			</div>
			<div class="split-item">
				<img src="/Workly_video_film.jpg" alt="Filming a Workly promotional video" />
				<p class="caption">Filming our 2nd Workly promotional video.</p>
			</div>
		</div>

		<!-- Lesson 3 -->
		<section class="prose-section">
			<h2 class="section-heading"><span class="heading-accent"></span> There is Opportunity Quite Literally Everywhere</h2>

			<p>I'll be frank. I had some initial hesitation going into this venture. When Blake and I first talked about it, my thoughts immediately went to the platforms that are already available and have been around for years, generating billions of dollars in collective revenue. Taskrabbit, Thumbtack, Nextdoor, Craigslist, and much more. When talking about the idea with friends and mentors, I was met with similar skepticism.</p>

			<p>But upon beginning to build the platform and speaking with our users directly, I came to the realization that even in industries that seem to be fairly well developed, there is always opportunity to build and make users' lives better. We had countless conversations with our customers about their frustration using platforms like Thumbtack and Taskrabbit — whether it was pricing, last minute cancellations, lack of availability from the contractors, and lack of attention given to daily everyday tasks that take literally 30 minutes to an hour or less.</p>

			<p>We were building in that exact gap that existing platforms didn't match. A gap that, large enough as it was, without building in the space, I never would have seen or considered firsthand and likely would have written off as a problem that has a matured tech solution.</p>

			<blockquote class="pull-quote">With enough analysis, user obsession, and the courage to take the jump, there is opportunity to improve existing or new systems everywhere.</blockquote>
		</section>

		<div class="media-full">
			<img src="/first_workly_video_end.jpeg" alt="Wrapping up the first Workly promotional video shoot" />
			<p class="caption">Wrapping up the first Workly promotional video shoot.</p>
		</div>

		<!-- Closing -->
		<section class="prose-section closing">
			<p>Ultimately, I am incredibly grateful for Workly being my first experience launching a consumer venture. Though the project is being put on hold, the many lessons I have learned will stay with me in all my future endeavors. Now building in the AI and construction management space, I look forward to ensuring responsible growth, user obsession, and key consideration of opportunity anywhere and everywhere it can be seen.</p>

			<blockquote class="pull-quote closing-quote">Building the plane as it flies is never easy, but every turbulent moment taught me something I couldn't have learned on the ground.</blockquote>

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
		object-position: center 40%;
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

	.post-tag.startup {
		background: rgba(167, 139, 250, 0.2);
		color: #c4b5fd;
		border: 1px solid rgba(167, 139, 250, 0.3);
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

	/* ===== PULL QUOTE ===== */
	.pull-quote {
		margin: 36px 0;
		padding: 24px 32px;
		border-left: 4px solid #a78bfa;
		background: rgba(167, 139, 250, 0.06);
		border-radius: 0 12px 12px 0;
		font-size: 1.25rem;
		font-style: italic;
		line-height: 1.7;
		color: #1a365d;
		font-weight: 500;
	}

	.closing-quote {
		font-size: 1.3rem;
		border-left-color: #7c3aed;
		background: rgba(124, 58, 237, 0.07);
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
		background: linear-gradient(90deg, #a78bfa, #c4b5fd);
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

	/* ===== MEDIA — video ===== */
	.media-video {
		max-width: 960px;
		margin: 52px auto 0;
		padding: 0 24px;
	}

	.media-video video {
		width: 100%;
		border-radius: 16px;
		display: block;
		max-height: 520px;
		object-fit: cover;
		box-shadow: 0 8px 32px rgba(0, 0, 0, 0.12);
		background: #1a2e3a;
	}

	/* ===== MEDIA — split ===== */
	.media-split {
		max-width: 960px;
		margin: 52px auto 0;
		padding: 0 24px;
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 16px;
	}

	.split-item img {
		width: 100%;
		height: 320px;
		object-fit: cover;
		border-radius: 14px;
		display: block;
		box-shadow: 0 6px 24px rgba(0, 0, 0, 0.1);
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

		.media-full,
		.media-video {
			padding: 0 16px;
			margin-top: 40px;
		}

		.media-split {
			grid-template-columns: 1fr;
			padding: 0 16px;
			margin-top: 40px;
		}

		.split-item img {
			height: 260px;
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

		.media-full,
		.media-video {
			padding: 0 12px;
			margin-top: 32px;
		}

		.media-split {
			padding: 0 12px;
			margin-top: 32px;
		}

		.split-item img {
			height: 200px;
		}

		.media-full img {
			border-radius: 12px;
			max-height: 400px;
		}

		.media-video video {
			border-radius: 12px;
			max-height: 360px;
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
