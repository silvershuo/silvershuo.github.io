<script lang="ts">
import { fly, scale } from "svelte/transition";

type Palette = {
	name: string;
	surface: string;
	surfaceStrong: string;
	accent: string;
	accentSoft: string;
	text: string;
	muted: string;
	border: string;
	glow: string;
};

const defaultLine = "给有点疲惫的下午，一次很小的打断。";
const defaultMood = "状态：还有一点提不起劲。";

const lines = [
	"先从很小的一步开始。点一下也算进展。",
	"如果今天有点吵，就把这里当作一秒安静。",
	"你的注意力没有坏掉，它只是需要被轻轻推一下。",
	"先去喝口水，再点一下，这很公平。",
	"小小的仪式感，比看起来更有用。",
	"简单一点也完全没问题。",
	"这种温柔的势头，也是真的势头。",
	"一点颜色会有帮助，再试一下也会。",
];

const moods = [
	defaultMood,
	"状态：无聊感稍微退了一格。",
	"状态：有点重新热起来了。",
	"状态：注意力慢慢回来了。",
	"状态：电量微微回升。",
];

const palettes: Palette[] = [
	{
		name: "钴蓝漂流",
		surface: "#10213f",
		surfaceStrong: "#081326",
		accent: "#7dc4ff",
		accentSoft: "#d7eeff",
		text: "#f5f9ff",
		muted: "#bed2ee",
		border: "rgba(169, 210, 255, 0.26)",
		glow: "rgba(80, 154, 255, 0.38)",
	},
	{
		name: "玫瑰讯号",
		surface: "#30142d",
		surfaceStrong: "#170a17",
		accent: "#ff9fb9",
		accentSoft: "#ffe2ea",
		text: "#fff7fb",
		muted: "#efc7d7",
		border: "rgba(255, 182, 208, 0.22)",
		glow: "rgba(255, 114, 171, 0.35)",
	},
	{
		name: "静谧薄荷",
		surface: "#122b29",
		surfaceStrong: "#081614",
		accent: "#8de3c7",
		accentSoft: "#dbfff2",
		text: "#f2fffa",
		muted: "#b9e7da",
		border: "rgba(152, 229, 205, 0.24)",
		glow: "rgba(94, 220, 185, 0.34)",
	},
	{
		name: "琥珀静电",
		surface: "#342112",
		surfaceStrong: "#171006",
		accent: "#ffd27a",
		accentSoft: "#fff1d1",
		text: "#fffaf0",
		muted: "#ecd7ae",
		border: "rgba(255, 221, 161, 0.22)",
		glow: "rgba(255, 186, 74, 0.32)",
	},
];

let count = 0;
let paletteIndex = 0;
let line = defaultLine;
let mood = defaultMood;
let lineKey = 0;
let countKey = 0;

const pickLine = (previous: string) => {
	if (lines.length === 1) return lines[0];

	let next = previous;
	while (next === previous) {
		next = lines[Math.floor(Math.random() * lines.length)];
	}
	return next;
};

function handleClick() {
	count += 1;
	line = pickLine(line);
	mood = moods[Math.min(count, moods.length - 1)];
	lineKey += 1;
	countKey += 1;
}

function cyclePalette() {
	paletteIndex = (paletteIndex + 1) % palettes.length;
}

function resetPanel() {
	count = 0;
	paletteIndex = 0;
	line = defaultLine;
	mood = defaultMood;
	lineKey += 1;
	countKey += 1;
}

$: palette = palettes[paletteIndex];
$: ctaLabel =
	count === 0 ? "先点一下" : count > 6 ? "继续点" : "再来一次";
$: resetDisabled = count === 0 && paletteIndex === 0;
$: panelStyle = [
	`--break-surface:${palette.surface}`,
	`--break-surface-strong:${palette.surfaceStrong}`,
	`--break-accent:${palette.accent}`,
	`--break-accent-soft:${palette.accentSoft}`,
	`--break-text:${palette.text}`,
	`--break-muted:${palette.muted}`,
	`--break-border:${palette.border}`,
	`--break-glow:${palette.glow}`,
].join(";");
</script>

<section class="break-card" style={panelStyle} aria-label="歇一会互动卡片">
	<div class="mesh"></div>
	<div class="glow-orb"></div>

	<div class="content">
		<div class="copy">
			<p class="eyebrow">互动角落</p>
			<h2>休息一下</h2>
			<p class="mood">{mood}</p>

			{#key lineKey}
				<p class="line" in:fly={{ y: 10, duration: 180 }}>
					{line}
				</p>
			{/key}

			<div class="actions">
				<button type="button" class="primary-btn" on:click={handleClick}>
					{ctaLabel}
				</button>
				<button type="button" class="ghost-btn" on:click={cyclePalette}>
					切换配色
				</button>
				<button
					type="button"
					class="ghost-btn"
					on:click={resetPanel}
					disabled={resetDisabled}
				>
					重置
				</button>
			</div>
		</div>

		<aside class="meta">
			<div class="stat-card">
				<span class="meta-label">点击次数</span>

				{#key countKey}
					<strong class="stat-value" in:scale={{ start: 0.85, duration: 170 }}>
						{count}
					</strong>
				{/key}

				<span class="meta-copy">
					{count === 0
						? "第一次点击后，计数器就会醒过来。"
						: "一个很小、但看得见的进展。"}
				</span>
			</div>

			<div class="palette-card">
				<span class="meta-label">当前配色</span>
				<strong class="palette-name">{palette.name}</strong>
				<div class="swatches" aria-hidden="true">
					{#each [palette.accent, palette.accentSoft, palette.surfaceStrong] as swatch}
						<span class="swatch" style={`background:${swatch}`}></span>
					{/each}
				</div>
			</div>
		</aside>
	</div>
</section>

<style>
	.break-card {
		position: relative;
		overflow: hidden;
		border-radius: calc(var(--radius-large) + 0.5rem);
		border: 1px solid var(--break-border);
		background:
			radial-gradient(circle at top right, var(--break-glow), transparent 28%),
			linear-gradient(135deg, var(--break-surface), var(--break-surface-strong) 62%);
		color: var(--break-text);
		box-shadow: 0 24px 70px rgba(15, 23, 42, 0.18);
	}

	.mesh,
	.glow-orb {
		pointer-events: none;
		position: absolute;
	}

	.mesh {
		inset: 0;
		background:
			linear-gradient(125deg, transparent 15%, rgba(255, 255, 255, 0.12) 48%, transparent 68%),
			radial-gradient(circle at 20% 20%, rgba(255, 255, 255, 0.08), transparent 32%);
		opacity: 0.45;
	}

	.glow-orb {
		right: -5rem;
		bottom: -6rem;
		width: 18rem;
		height: 18rem;
		border-radius: 999px;
		background: radial-gradient(circle, var(--break-accent-soft), transparent 62%);
		filter: blur(16px);
		opacity: 0.28;
	}

	.content {
		position: relative;
		display: grid;
		gap: 1.5rem;
		padding: 1.5rem;
	}

	.copy {
		max-width: 42rem;
	}

	.eyebrow,
	.meta-label {
		display: block;
		font-size: 0.78rem;
		font-weight: 700;
		letter-spacing: 0.18em;
		text-transform: uppercase;
		color: var(--break-muted);
	}

	h2 {
		margin: 0.45rem 0 0;
		font-size: clamp(2.15rem, 4vw, 3.4rem);
		line-height: 0.96;
	}

	.mood {
		margin: 1rem 0 0;
		color: var(--break-muted);
		font-size: 1rem;
		line-height: 1.7;
	}

	.line {
		margin: 1.2rem 0 0;
		max-width: 38rem;
		padding: 1rem 1.1rem;
		border-radius: 1rem;
		border: 1px solid rgba(255, 255, 255, 0.14);
		background: rgba(7, 10, 18, 0.18);
		backdrop-filter: blur(12px);
		font-size: 1rem;
		line-height: 1.75;
	}

	.actions {
		display: flex;
		flex-wrap: wrap;
		gap: 0.75rem;
		margin-top: 1.35rem;
	}

	.primary-btn,
	.ghost-btn {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		min-height: 3.15rem;
		padding: 0.9rem 1.2rem;
		border: 0;
		border-radius: 999px;
		font: inherit;
		font-weight: 700;
		cursor: pointer;
		transition:
			transform 160ms ease,
			background 160ms ease,
			opacity 160ms ease,
			box-shadow 160ms ease;
	}

	.primary-btn:hover,
	.ghost-btn:hover {
		transform: translateY(-1px);
	}

	.primary-btn:focus-visible,
	.ghost-btn:focus-visible {
		outline: 2px solid var(--break-accent-soft);
		outline-offset: 3px;
	}

	.primary-btn {
		background: var(--break-accent);
		color: #08111f;
		box-shadow: 0 12px 30px rgba(0, 0, 0, 0.18);
	}

	.ghost-btn {
		background: rgba(255, 255, 255, 0.1);
		color: var(--break-text);
		border: 1px solid rgba(255, 255, 255, 0.14);
		backdrop-filter: blur(12px);
	}

	.ghost-btn:disabled {
		opacity: 0.45;
		cursor: default;
		transform: none;
	}

	.meta {
		display: grid;
		gap: 0.85rem;
		align-self: end;
	}

	.stat-card,
	.palette-card {
		padding: 1rem;
		border-radius: 1.2rem;
		border: 1px solid rgba(255, 255, 255, 0.12);
		background: rgba(7, 10, 18, 0.22);
		backdrop-filter: blur(12px);
	}

	.stat-value,
	.palette-name {
		display: block;
		font-weight: 800;
	}

	.stat-value {
		margin-top: 0.55rem;
		font-size: clamp(2.8rem, 7vw, 4.2rem);
		line-height: 1;
	}

	.palette-name {
		margin-top: 0.4rem;
		font-size: 1.25rem;
	}

	.meta-copy {
		display: block;
		margin-top: 0.55rem;
		color: var(--break-muted);
		line-height: 1.6;
	}

	.swatches {
		display: flex;
		gap: 0.55rem;
		margin-top: 0.95rem;
	}

	.swatch {
		display: inline-block;
		width: 2rem;
		height: 2rem;
		border-radius: 999px;
		border: 1px solid rgba(255, 255, 255, 0.28);
		box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.08);
	}

	@media (min-width: 900px) {
		.content {
			grid-template-columns: minmax(0, 1.2fr) 15rem;
			padding: 2rem;
		}
	}

	@media (max-width: 640px) {
		.content {
			padding: 1.25rem;
		}

		.line {
			font-size: 0.95rem;
		}

		.actions > button {
			flex: 1 1 100%;
		}
	}
</style>
