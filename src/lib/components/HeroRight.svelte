<div class="right-content">
	<p class="description">
		Hi! I'm Ibrahim Mohsin, a full stack<br />
		developer and designer passionate about<br />
		building innovative solutions and<br />
		impactful ventures. Check out my<br />
		work here and feel free to reach out<br />
		to chat!
	</p>
	<div class="nus-status">
		<span class="status-dot"></span>
		<img src="/NUS-logo.png" alt="NUS Logo" class="nus-logo" />
		<span class="status-text">Currently Studying CS @ NUS Singapore</span>
	</div>
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
	</div>
</div>

<style>
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

	.nus-status {
		display: flex;
		align-items: center;
		gap: 8px;
		margin-bottom: 20px;
		animation: slideUpFadeIn 0.8s ease-out 0.2s both;
	}

	.status-dot {
		width: 10px;
		height: 10px;
		border-radius: 50%;
		background-color: #10b981;
		box-shadow: 0 0 8px rgba(16, 185, 129, 0.6), 0 0 16px rgba(16, 185, 129, 0.4);
		animation: pulse 2s ease-in-out infinite;
		flex-shrink: 0;
	}

	@keyframes pulse {
		0%, 100% {
			box-shadow: 0 0 8px rgba(16, 185, 129, 0.6), 0 0 16px rgba(16, 185, 129, 0.4);
		}
		50% {
			box-shadow: 0 0 12px rgba(16, 185, 129, 0.8), 0 0 24px rgba(16, 185, 129, 0.6);
		}
	}

	.nus-logo {
		width: 24px;
		height: 24px;
		object-fit: contain;
		flex-shrink: 0;
	}

	.status-text {
		font-size: 14px;
		font-weight: 600;
		color: #ffffff;
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

	@media (max-width: 768px) {
		.right-content {
			right: 40px;
			top: auto;
			bottom: 150px;
			transform: translateY(0);
		}

		.description {
			font-size: 14px;
		}
	}

	@media (max-width: 480px) {
		.description {
			font-size: 13px;
		}
	}
</style>
