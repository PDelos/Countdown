<script lang="ts">
	import { PUBLIC_TARGET_DATE } from '$env/static/public';
	import FlipDigit from '$lib/components/FlipDigit.svelte';

	// If the env var is missing/empty, treat it as "no date configured".
	const rawTarget = (PUBLIC_TARGET_DATE ?? '').trim();
	const targetDate = rawTarget ? new Date(rawTarget) : null;
	const hasTargetDate = targetDate instanceof Date && !isNaN(targetDate.getTime());

	let days = $state(0);
	let hours = $state(0);
	let isExpired = $state(false);

	function updateCountdown() {
		if (!hasTargetDate || !targetDate) return;

		const diff = targetDate.getTime() - Date.now();

		if (diff <= 0) {
			isExpired = true;
			days = 0;
			hours = 0;
			return;
		}

		const totalSeconds = Math.floor(diff / 1000);
		days = Math.floor(totalSeconds / 86400);
		hours = Math.floor((totalSeconds % 86400) / 3600);
	}

	$effect(() => {
		// Don't start the interval when there's no valid date configured.
		if (!hasTargetDate) return;

		updateCountdown();
		const interval = setInterval(updateCountdown, 60000);
		return () => clearInterval(interval);
	});
</script>

<section class="page">
	<h1 class="title">Countdown</h1>
	<h2 class="subtitle">Web Launching</h2>

	<div class="content">
		{#if !hasTargetDate}
			<p class="lead">No launch date set.</p>
		{:else if isExpired}
			<p class="lead">We're live!</p>
		{:else}
			<div class="countdown-grid">
				<!-- Top row -->
				<div class="digits">
					<FlipDigit digit={Math.floor(days / 10)} />
					<FlipDigit digit={days % 10} />
				</div>

				<span class="separator">:</span>

				<div class="digits">
					<FlipDigit digit={Math.floor(hours / 10)} />
					<FlipDigit digit={hours % 10} />
				</div>

				<!-- Bottom row -->
				<p class="label">Day{days === 1 ? '' : 's'}</p>

				<div></div>
				<!-- empty cell under the separator -->

				<p class="label">Hour{hours === 1 ? '' : 's'}</p>
			</div>
		{/if}
	</div>
</section>

<style>
	h1,
	h2,
	p {
		text-transform: uppercase;
	}
	.lead {
		font-size: 3rem;
		font-weight: 600;
		margin-top: 2rem;
		letter-spacing: -1px;
	}

	.page {
		height: 100vh;
		width: 100vw;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.title {
		font-size: 5rem;
		margin-top: 3rem;
		font-weight: 700;
		letter-spacing: -1px;
	}
	.subtitle {
		font-size: 2.2rem;
		font-weight: 300;
		margin-top: -0.5rem;
		margin-bottom: 1.2rem;
		letter-spacing: -1px;
	}

	.countdown-grid {
		display: grid;
		grid-template-columns: auto auto auto; /* days | : | hours */
		grid-template-rows: auto auto; /* digits | labels */
		align-items: center;
		justify-content: center;
		column-gap: 25px;
		row-gap: 20px;
		text-align: center;
	}

	.digits {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 10px;
	}

	.separator {
		font-size: 120px;
		font-weight: bold;
	}

	.label {
		font-size: 1.5rem;
	}
</style>
