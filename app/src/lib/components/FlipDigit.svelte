<script lang="ts">
	interface Props {
		digit: number;
	}

	const { digit }: Props = $props();

	$effect(() => {
		if (digit < 0 || digit > 9) {
			throw new Error('Digit must be between 0 and 9');
		}
	});
</script>

<div class="flip-digit">
	<div class="card">
		<p class="digit">{digit}</p>
	</div>
</div>

<style>
	.flip-digit {
		width: 120px;
		height: 190px;
	}

	.card {
		width: 100%;
		height: 100%;
		background: var(--fg);
		border-radius: 15px;
		display: flex;
		align-items: center;
		justify-content: center;
		position: relative;
		overflow: hidden;
	}

	.card::before {
		content: '';
		position: absolute;
		left: 0;
		right: 0;
		top: 50%;
		height: 5px;
		background: var(--bg);
		transform: translateY(-50%);
	}

	.digit {
		font-size: 120px;
		font-weight: bold;
		color: var(--bg);
		position: relative;
		z-index: 2;
	}
</style>
