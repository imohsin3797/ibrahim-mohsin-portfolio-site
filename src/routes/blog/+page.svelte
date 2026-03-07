<script>
	import { onMount } from 'svelte';
	import Header from '$lib/components/Header.svelte';

	const posts = [
		{
			slug: 'building-the-plane',
			title: 'Building the Plane as it Flies',
			subtitle: "Lessons learned launching my first venture: the chaos, the pivots, and what I'd do differently.",
			tag: 'Startup',
			date: 'December 2025',
			image: '/workly_blog_cover.jpg'
		},
		{
			slug: 'skynav',
			title: 'SkyNav: Building AI for the Elderly',
			subtitle: 'How our team designed and built an AI platform to improve accessibility and information access for aging populations in Western NC.',
			tag: 'Professional',
			date: 'July 2025',
			image: '/skynav_blog.JPG'
		},
		{
			slug: 'lake-superior',
			title: '22 Days Away',
			subtitle: 'Stories from 90 miles of open water and 22 days away having never camped a night before in my life.',
			tag: 'Travel',
			date: 'July 2024',
			image: '/22_days_away.jpg'
		}
	];

	const tagColors = {
		Startup:      { bg: 'rgba(167, 139, 250, 0.15)', text: '#a78bfa' },
		Professional: { bg: 'rgba(74, 138, 168, 0.15)',  text: '#4a8aa8' },
		Travel:       { bg: 'rgba(52, 211, 153, 0.15)',  text: '#34d399' }
	};

	const allTags = ['All', ...Object.keys(tagColors)];

	let expanded = false;
	let activeTag = 'All';
	let visible = false;

	function toggleNav() {
		expanded = !expanded;
	}

	$: filteredPosts = activeTag === 'All'
		? posts
		: posts.filter(p => p.tag === activeTag);

	onMount(() => {
		setTimeout(() => { visible = true; }, 80);
	});
</script>

<svelte:head>
	<title>Blog — Ibrahim Mohsin</title>
</svelte:head>

<Header {expanded} {toggleNav} />

<div class="page">
	<!-- Hero -->
	<section class="hero">
		<div class="hero-inner" class:visible>
			<span class="section-label">Writing</span>
			<h1 class="hero-title">The Latest</h1>
			<p class="hero-sub">Stories, mistakes, and rants about my most meaningful experiences.</p>
		</div>
		<div class="wave">
			<svg viewBox="0 0 1440 100" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
				<path class="wave-fill" d="M0,50 C360,100 1080,0 1440,50 L1440,100 L0,100 Z"/>
			</svg>
		</div>
	</section>

	<!-- Posts -->
	<main class="posts-section">
		<div class="posts-inner">
			<!-- Filter bar -->
			<div class="filter-bar" class:visible>
				{#each allTags as tag}
					<button
						class="filter-btn"
						class:active={activeTag === tag}
						on:click={() => { activeTag = tag; }}
					>
						{tag}
					</button>
				{/each}
			</div>

			<!-- Grid -->
			<div class="posts-grid">
				{#each filteredPosts as post, i (post.slug)}
					<a
						href="/blog/{post.slug}"
						class="post-card"
						class:visible
						style="animation-delay: {i * 90}ms"
					>
						<div class="post-image">
							<img src={post.image} alt={post.title} />
						</div>
						<div class="post-content">
							<div class="post-meta">
								<span
									class="post-tag"
									style="background:{tagColors[post.tag].bg}; color:{tagColors[post.tag].text}"
								>{post.tag}</span>
								<span class="post-date">{post.date}</span>
							</div>
							<h2 class="post-title">{post.title}</h2>
							<p class="post-sub">{post.subtitle}</p>
							<span class="read-link">Read More <span class="arrow">&rarr;</span></span>
						</div>
					</a>
				{/each}
			</div>
		</div>
	</main>

	<footer class="page-footer">
		<p>&copy; 2026 Ibrahim Mohsin. All rights reserved.</p>
	</footer>
</div>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
		font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
	}

	.page {
		min-height: 100vh;
		background: #e8f4f8;
		display: flex;
		flex-direction: column;
	}

	/* ===== HERO ===== */
	.hero {
		background: linear-gradient(180deg, #e8f4f8 0%, #b8d8e8 30%, #6ba3c0 70%, #4a8aa8 100%);
		padding-top: 120px;
		position: relative;
	}

	.hero-inner {
		max-width: 900px;
		margin: 0 auto;
		padding: 40px 48px 80px;
		opacity: 0;
		transform: translateY(30px);
		transition: opacity 0.7s ease, transform 0.7s ease;
	}

	.hero-inner.visible {
		opacity: 1;
		transform: translateY(0);
	}

	.section-label {
		display: inline-block;
		font-size: 0.78rem;
		font-weight: 600;
		letter-spacing: 2.5px;
		text-transform: uppercase;
		color: rgba(255, 255, 255, 0.8);
		margin-bottom: 14px;
	}

	.hero-title {
		font-size: clamp(3rem, 8vw, 5.5rem);
		font-weight: 800;
		color: #ffffff;
		margin: 0 0 16px 0;
		line-height: 1.05;
		letter-spacing: -0.02em;
		text-shadow: 0 2px 12px rgba(26, 61, 82, 0.3);
	}

	.hero-sub {
		font-size: 1.15rem;
		color: rgba(255, 255, 255, 0.85);
		margin: 0;
		line-height: 1.65;
		max-width: 560px;
	}

	/* Wave — full bleed, no inherited padding */
	.wave {
		position: relative;
		width: 100%;
		line-height: 0;
		margin-top: -1px;
	}

	.wave svg {
		display: block;
		width: 100%;
		height: 100px;
	}

	.wave-fill {
		fill: #e8f4f8;
	}

	/* ===== POSTS SECTION ===== */
	.posts-section {
		flex: 1;
		background: #e8f4f8;
		padding: 0 48px 80px;
	}

	.posts-inner {
		max-width: 1100px;
		margin: 0 auto;
	}

	/* ===== FILTER BAR ===== */
	.filter-bar {
		display: flex;
		gap: 10px;
		flex-wrap: wrap;
		margin-bottom: 36px;
		padding-top: 48px;
		opacity: 0;
		transform: translateY(16px);
		transition: opacity 0.6s ease 0.15s, transform 0.6s ease 0.15s;
	}

	.filter-bar.visible {
		opacity: 1;
		transform: translateY(0);
	}

	.filter-btn {
		padding: 8px 20px;
		font-size: 0.85rem;
		font-weight: 600;
		border-radius: 50px;
		border: 1.5px solid rgba(74, 138, 168, 0.25);
		background: rgba(255, 255, 255, 0.55);
		color: #4a5e73;
		cursor: pointer;
		transition: all 0.2s ease;
		backdrop-filter: blur(8px);
		-webkit-backdrop-filter: blur(8px);
	}

	.filter-btn:hover {
		border-color: #4a8aa8;
		color: #4a8aa8;
		background: rgba(255, 255, 255, 0.75);
	}

	.filter-btn.active {
		background: #4a8aa8;
		border-color: #4a8aa8;
		color: #ffffff;
		box-shadow: 0 4px 12px rgba(74, 138, 168, 0.3);
	}

	/* ===== POSTS GRID ===== */
	.posts-grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 28px;
	}

	.post-card {
		display: flex;
		flex-direction: column;
		border-radius: 20px;
		overflow: hidden;
		background: rgba(255, 255, 255, 0.6);
		backdrop-filter: blur(16px);
		-webkit-backdrop-filter: blur(16px);
		border: 1px solid rgba(255, 255, 255, 0.75);
		box-shadow: 0 4px 20px rgba(0, 0, 0, 0.06);
		text-decoration: none;
		color: inherit;
		transition: transform 0.35s ease, box-shadow 0.35s ease;
		opacity: 0;
		transform: translateY(24px);
	}

	.post-card.visible {
		animation: cardIn 0.55s ease forwards;
	}

	@keyframes cardIn {
		to { opacity: 1; transform: translateY(0); }
	}

	.post-card:hover {
		transform: translateY(-8px) !important;
		box-shadow: 0 16px 40px rgba(0, 0, 0, 0.1);
	}

	.post-image {
		width: 100%;
		height: 220px;
		overflow: hidden;
	}

	.post-image img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		transition: transform 0.5s ease;
	}

	.post-card:hover .post-image img {
		transform: scale(1.06);
	}

	.post-content {
		padding: 24px 24px 28px;
		display: flex;
		flex-direction: column;
		flex: 1;
	}

	.post-meta {
		display: flex;
		align-items: center;
		gap: 10px;
		margin-bottom: 12px;
	}

	.post-tag {
		font-size: 0.72rem;
		font-weight: 600;
		letter-spacing: 1px;
		text-transform: uppercase;
		padding: 4px 11px;
		border-radius: 50px;
	}

	.post-date {
		font-size: 0.78rem;
		color: #8a9bb0;
		font-weight: 500;
	}

	.post-title {
		font-size: 1.2rem;
		font-weight: 700;
		color: #1a365d;
		margin: 0 0 10px 0;
		line-height: 1.35;
	}

	.post-sub {
		font-size: 0.92rem;
		line-height: 1.65;
		color: #4a5e73;
		margin: 0 0 20px 0;
		flex: 1;
	}

	.read-link {
		font-size: 0.9rem;
		font-weight: 600;
		color: #4a8aa8;
		display: inline-flex;
		align-items: center;
		gap: 4px;
	}

	.post-card:hover .read-link {
		color: #3d7a96;
	}

	.arrow {
		display: inline-block;
		transition: transform 0.25s ease;
	}

	.post-card:hover .arrow {
		transform: translateX(4px);
	}

	/* ===== FOOTER ===== */
	.page-footer {
		padding: 20px 48px;
		border-top: 1px solid rgba(74, 138, 168, 0.12);
		text-align: center;
	}

	.page-footer p {
		font-size: 0.85rem;
		color: #8a9bb0;
		margin: 0;
	}

	/* ===== RESPONSIVE ===== */
	@media (max-width: 900px) {
		.posts-grid {
			grid-template-columns: repeat(2, 1fr);
		}
	}

	@media (max-width: 600px) {
		.hero-inner {
			padding: 20px 24px 60px;
		}

		.hero-title {
			font-size: 2.75rem;
		}

		.hero-sub {
			font-size: 1rem;
		}

		.posts-section {
			padding: 0 24px 60px;
		}

		.filter-bar {
			padding-top: 36px;
			gap: 8px;
		}

		.filter-btn {
			padding: 7px 16px;
			font-size: 0.82rem;
		}

		.posts-grid {
			grid-template-columns: 1fr;
			gap: 20px;
		}

		.page-footer {
			padding: 18px 24px;
		}
	}

	@media (max-width: 480px) {
		.hero-inner {
			padding: 16px 16px 50px;
		}

		.hero-title {
			font-size: 2.2rem;
		}

		.hero-sub {
			font-size: 0.92rem;
		}

		.posts-section {
			padding: 0 16px 50px;
		}

		.filter-bar {
			padding-top: 28px;
			gap: 6px;
			margin-bottom: 28px;
		}

		.filter-btn {
			padding: 6px 14px;
			font-size: 0.78rem;
		}

		.post-content {
			padding: 18px 18px 22px;
		}

		.post-title {
			font-size: 1.1rem;
		}

		.post-sub {
			font-size: 0.88rem;
		}

		.post-image {
			height: 180px;
		}

		.wave svg {
			height: 60px;
		}

		.page-footer {
			padding: 14px 16px;
		}
	}
</style>
