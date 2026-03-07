<script>
	import { onMount } from 'svelte';
	import Header from '$lib/components/Header.svelte';

	let expanded = false;
	let heroVisible = false;
	let contentVisible = false;

	function toggleNav() {
		expanded = !expanded;
	}

	/** @param {Event} e */
	function loopRainDanceFirstSix(e) {
		const v = /** @type {HTMLVideoElement} */ (e.currentTarget);
		if (v && v.currentTime >= 6) v.currentTime = 0;
	}

	onMount(() => {
		setTimeout(() => { heroVisible = true; }, 100);
		setTimeout(() => { contentVisible = true; }, 400);
	});
</script>

<svelte:head>
	<title>22 Days Away — Ibrahim Mohsin</title>
	<link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600&display=swap" rel="stylesheet" />
</svelte:head>

<Header {expanded} {toggleNav} />

<article class="post">

	<!-- ===== BANNER ===== -->
	<div class="banner" class:visible={heroVisible}>
		<img src="/22_days_away.jpg" alt="Lake Superior wilderness" class="banner-img" />
		<div class="banner-overlay"></div>
		<div class="banner-content">
			<span class="post-tag travel">Travel</span>
			<h1 class="banner-title">22 Days Away</h1>
			<p class="banner-sub">Stories from the Wilderness of Lake Superior</p>
			<div class="banner-meta">
				<span>July 2024</span>
				<span class="dot">&middot;</span>
				<span>Ibrahim Mohsin</span>
			</div>
		</div>
	</div>

	<!-- ===== BODY ===== -->
	<div class="body-wrap" class:visible={contentVisible}>

		<!-- Intro -->
		<section class="prose-section">
			<p class="lead">On the second day of my Outward Bound experience, I reluctantly stood over the neoprene wetsuit I had been instructed to put on, feeling the freezing rain pelt my back as I got dressed, all the while cursing the decisions that had brought me here. As I began mile 1 of the journey of a lifetime ahead, I came to a simple conclusion:</p>

			<blockquote class="pull-quote">This was going to be the hardest thing I had ever done.</blockquote>

			<p>The June after my senior year of high school, I bid farewell to my friends and family for 22 days as I embarked on a trek through Canadian Lake Superior led by Outward Bound — a mandatory commitment I made when I accepted the Morehead-Cain Scholarship at UNC.</p>

			<section class="prose-section prose-with-float">
			<figure class="float-image">
				<img src="/airport_farewell.jpg" alt="Saying goodbye at Indianapolis International Airport" />
				<figcaption>June 22nd: Saying goodbye to my mom at the Indianapolis International Airport, heading to Duluth, Minnesota.</figcaption>
			</figure>

			<p>There was little that could have prepared me for what I had in store. Leaving the airport from my hometown in Indianapolis, I had a million questions racing through my mind:</p>

			<ul class="questions-list">
				<li>"How much am I going to miss in the lives of my friends and family while I'm gone?"</li>
				<li>"When will I feel comfortable and in routine on the trip?"</li>
				<li>"Will I be able to physically tolerate the swarms of mosquitoes I'll inevitably find?"</li>
			</ul>

			<p>The answers were simple: a lot, you won't, and no. More significantly, just a few days after these trivial questions had filled my mind, my physical and mental energy was consumed entirely by:</p>

			<ul class="survival-list">
				<li>Counting down the minutes to my next meal</li>
				<li>Holding the comfort of my new-found friends in my hands as I secured our tarp among the trees in midnight darkness</li>
				<li>Navigating our group with nothing but a compass, a map, and a dream of reaching camp before sunset</li>
				<li>And most importantly — telling myself every day that <em>better times are to come</em></li>
			</ul>
			<div class="float-clear"></div>
		</section>

		<!-- Scene-setting image + video -->
		<div class="media-full">
			<img src="/group_preparing.JPG" alt="The group resting and planning on the rocks of Lake Superior" />
			<p class="caption">Planning on the rocks, one of many shore breaks during the kayaking portion.</p>
		</div>

		<section class="prose-section">
			<p>It was truly remarkable how quickly my thoughts and energy boiled down to simple human tasks when I stepped away from the highly programmed, structured, and noisy lifestyle I'm accustomed to. What we were going to eat, where we were heading, when we were sleeping, and when we were waking up to start over again. Rinse, wash, repeat.</p>
		</section>

		<div class="media-video">
			<video autoplay muted loop playsinline preload="metadata">
				<source src="/waves_on_camp.MOV" type="video/mp4" />
			</video>
			<p class="caption">Waves rolling in after a long day on the water.</p>
		</div>

		<!-- Birthday Celebration -->
		<section class="prose-section">
			<h2 class="section-heading">
				<span class="heading-accent"></span>
				Birthday Celebration
			</h2>

			<p>In the 22 days away, we celebrated a few birthdays among our group. On the milestone 10th day of our trip, we arrived at shore after yet another 10-hour kayaking trek, ready to unpack, set up camp, and celebrate a group member's birthday. We went through our normal routines, unpacking our kayaks, tying up tarps, and beginning to prepare dinner.</p>

			<p>To our pleasant surprise, our instructors had baked a brownie in the fire for dessert.</p>
		</section>

		<div class="media-split">
			<div class="split-item">
				<img src="/sarah_birthday.png" alt="Fire-baked birthday brownie for Sarah" />
				<p class="caption">Happy birthday, Sarah, baked over an open fire on Day 10.</p>
			</div>
			<div class="split-item">
				<img src="/preparing_lunch.JPG" alt="Shore break and lunch prep between paddles" />
				<p class="caption">A shore break between paddles, every rest earned.</p>
			</div>
		</div>

		<section class="prose-section">
			<p>Eating that brownie reminded me of a very simple fact:</p>

			<blockquote class="pull-quote">There is so much that I take for granted.</blockquote>

			<p>The basic joy of eating a sugary treat reminded me how many little things make life enjoyable. Out on the water, stripped of the comforts I never think twice about at home, even the smallest things carried enormous weight. A warm, well-cooked meal. A dry pair of socks. A moment of laughter around a fire. Out there, these were everything.</p>

			<p>I realized that gratitude lives in the quiet appreciation of ordinary things, however trivial they may seem at first glance.</p>
		</section>

		<!-- 20 Miles of Doom -->
		<section class="prose-section">
			<h2 class="section-heading">
				<span class="heading-accent"></span>
				20 Miles of Doom
			</h2>

			<p>After several excruciating days paddling 14 hours through rainstorms and challenging waves, while shivering through the night in a sopping wet sleeping bag laid out on rocks, we were told by our instructors that we had our biggest day yet ahead of us: <strong>20 miles on the water.</strong> For reference, the longest day we had done before that was 11 miles, which took us about 8 hours.</p>

			<p>Upon hearing this, a clear sense of anxiety and dread swept over the group. Just a week in, we were all substantially weaker, hungrier, sleep-deprived, and desperate to reach the next vantage point, wherever it was.</p>
		</section>

		<div class="media-video">
			<video
				autoplay
				muted
				playsinline
				preload="metadata"
				on:timeupdate={loopRainDanceFirstSix}
			>
				<source src="/rain_dancing.MOV" type="video/mp4" />
			</video>
			<p class="caption"> Dancing in the rain for warmth.</p>
		</div>

		<section class="prose-section">
			<p>Despite these thoughts, when we woke up at 4:00 AM that morning to begin the day, our entire group worked in sync in a way we hadn't quite done before. We delegated tasks, got water boiling in record time, efficiently prepared the kayaks, and got dressed while ready members did jumping jacks on the shore to wake themselves up.</p>

			<p>We knew from the start that it was going to be a long and difficult day, yet despite less than four hours of sleep and nothing but granola, raisins, and rice to fuel us, we were filled with a newfound sense of motivation and purpose.</p>

			<blockquote class="pull-quote">It truly is a mindset thing. With the right energy and group effort behind a goal, no matter how far away it may seem, it is always closer than it appears.</blockquote>

			<p>That day showed me how crucial it is to set lofty, seemingly unattainable goals. In doing so, we gave ourselves a renewed sense of purpose, challenge, and curiosity. We were determined to find out what was possible.</p>

			<p>Suffice it to say, we reached our destination — completing the full 20 miles — and even managed to get dinner before sundown.</p>
		</section>

		<div class="media-full">
			<img src="/drinking_water.JPG" alt="Filtering water from the wilderness during the hiking portion" />
			<p class="caption">Filtering water in the backcountry, a daily ritual once the hiking portion began.</p>
		</div>

		<!-- Silver Islet -->
		<section class="prose-section">
			<h2 class="section-heading">
				<span class="heading-accent"></span>
				Silver I-Lit
			</h2>

			<p>After 2 weeks, we finally arrived at our final destination of the kayaking portion of our trip — Silver Islet, a small Canadian town off the coast of Lake Superior. As we paddled in, we began to hear the sound of bagpipes playing through the town, echoing across the water toward us.</p>

			<p>It was a surreal and unexpected welcome after two weeks of nothing but wind and waves. Locals gathered at the shore offering hot cups of coffee, cheering us in as we made our final approach. We stripped off our sweat-stained life jackets, pulled our kayaks from the water for the last time, and stepped onto solid ground — officially done with one of the longest and hardest things any of us had ever done.</p>
		</section>

		<div class="media-split">
			<div class="split-item">
				<img src="/silver_islet.JPG" alt="The group at Silver Islet Harbour sign" />
				<p class="caption">Arriving at Silver Islet Harbour, two weeks of water behind us.</p>
			</div>
			<div class="split-item">
				<img src="/Superior_sunset.JPG" alt="Pink and purple sunset over Lake Superior" />
				<p class="caption">A Lake Superior sunset — one of the many moments of pure stillness.</p>
			</div>
		</div>

		<!-- Reconnecting -->
		<section class="prose-section">
			<h2 class="section-heading">
				<span class="heading-accent"></span>
				Reconnecting
			</h2>

			<p>Upon completing the kayaking and hiking and reaching our long-awaited 22nd day, I could really feel the joy and triumph in the air. We sat down together as a group and had what felt like the first real meal in weeks — barbecue chicken, mashed potatoes, and a brownie sundae for dessert. We finally showered and got a real look at ourselves in the mirror, which was, to put it mildly, a frightening sight.</p>

			<p>Then came the moment we had (surprisingly) both dreaded and looked forward to: our phones. Thousands of messages, emails, and notifications came flooding in, the noise of the "real world" rushing back in all at once.</p>

			<p class="news-callout">Bronny got drafted to the Lakers. Spain won the Euro. Trump got shot.</p>

			<p>It was a strange feeling, holding that little screen again, getting reconnected. What struck me most was how little I had actually missed it.</p>
		</section>

		<div class="media-full">
			<img src="/reconnecting.JPG" alt="The group sharing their first real meal at a table after 22 days" />
			<p class="caption">The first real meal in weeks, the group at the dining table, finally back inside.</p>
		</div>

		<section class="prose-section">
			<p>Out on Lake Superior, life had been reduced to its simplest form — paddle, eat, sleep, repeat — and somewhere in that simplicity, I had found a kind of clarity. Enough time to think. Something I rarely feel I get in the buzz and distractions of my daily life.</p>

			<p>The lesson was plain: so much of what we treat as essential is really just noise, and it sometimes takes 22 days on a cold, unforgiving lake to figure that out.</p>
		</section>

		<div class="media-full">
			<img src="/final_descent.JPG" alt="Ibrahim on a rocky summit with a backpack, vast Canadian wilderness behind him" />
			<p class="caption">Final descent during the hiking portion, somewhere in the Canadian wilderness, pack on my back.</p>
		</div>

		<section class="prose-section closing">
			<blockquote class="pull-quote closing-quote">Weirdly, despite all the blood, sweat, and tears, I will genuinely miss Lake Superior. And I can confidently say — with some important changes — I hope to do it again someday, with newfound realizations of stillness, accomplishment, and mindset.</blockquote>

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
		object-position: center 30%;
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

	.post-tag.travel {
		background: rgba(52, 211, 153, 0.2);
		color: #6ee7b7;
		border: 1px solid rgba(52, 211, 153, 0.3);
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

	.questions-list,
	.survival-list {
		margin: 0 0 24px 0;
		padding-left: 0;
		list-style: none;
	}

	.questions-list li,
	.survival-list li {
		font-size: 1.05rem;
		line-height: 1.75;
		color: #2d4a5e;
		padding: 10px 16px 10px 20px;
		border-left: 2px solid rgba(74, 138, 168, 0.25);
		margin-bottom: 8px;
		font-style: italic;
	}

	.survival-list li {
		font-style: normal;
		border-left-color: rgba(74, 138, 168, 0.4);
	}

	strong {
		color: #1a365d;
		font-weight: 700;
	}

	em {
		color: #3d7a96;
	}

	/* ===== FLOAT IMAGE ===== */
	.prose-with-float {
		overflow: hidden;
	}

	.float-image {
		float: right;
		width: 260px;
		margin: 0 0 20px 32px;
	}

	.float-image img {
		width: 100%;
		aspect-ratio: 3 / 4;
		object-fit: cover;
		border-radius: 14px;
		display: block;
		box-shadow: 0 8px 28px rgba(0, 0, 0, 0.13);
	}

	.float-image figcaption {
		font-size: 0.8rem;
		color: #8a9bb0;
		text-align: center;
		margin-top: 8px;
		font-style: italic;
		line-height: 1.5;
	}

	.float-clear {
		clear: both;
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

	/* ===== NEWS CALLOUT ===== */
	.news-callout {
		font-size: 1rem;
		font-weight: 600;
		color: #4a5e73;
		background: rgba(255, 255, 255, 0.7);
		border: 1px solid rgba(74, 138, 168, 0.15);
		border-radius: 12px;
		padding: 14px 20px;
		margin: 24px 0;
		letter-spacing: 0.2px;
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
		.float-image {
			float: none;
			width: 100%;
			margin: 0 0 24px 0;
		}

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

		p, .questions-list li, .survival-list li {
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

		p, .questions-list li, .survival-list li {
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
