<template>
  <div ref="container" class="marquee" @mouseenter="pause" @mouseleave="resume">
    <div ref="track" class="marquee-track">
      <!-- the original slot content (we clone this node in JS) -->
      <div ref="content" class="marquee-content"><slot /></div>
      <!-- clones will be appended here by JS -->
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick, watch } from "vue";

const props = defineProps({
  // speed in pixels per second (higher = faster). Default 100 px/s.
  speed: { type: Number, default: 100 },
  // maximum clone iterations to avoid runaway loops
  maxClones: { type: Number, default: 50 },
});

const container = ref(null);
const track = ref(null);
const content = ref(null);
let resizeObserver = null;

function buildMarquee() {
  if (!container.value || !track.value || !content.value) return;

  // Keep only the original content element and remove previous clones
  const children = Array.from(track.value.children);
  for (let i = children.length - 1; i >= 1; i--) {
    track.value.removeChild(children[i]);
  }

  // Wait a tick to ensure layout is stable
  nextTick(() => {
    const singleWidth = content.value.scrollWidth;
    const containerWidth = container.value.clientWidth;

    // If width is zero (no slot content) bail out
    if (singleWidth === 0) return;

    // Duplicate the content until the track is at least twice the container width
    // (so when we translate by half the track width we never see a gap).
    let totalWidth = singleWidth;
    let clones = 0;
    while (totalWidth < containerWidth * 2 && clones < props.maxClones) {
      const clone = content.value.cloneNode(true);
      track.value.appendChild(clone);
      totalWidth += singleWidth;
      clones++;
    }

    // Now compute exact translate distance and animation duration
    // track.scrollWidth should now be >= containerWidth*2
    const translatePx = track.value.scrollWidth / 2;
    // duration (seconds) = distance (px) / speed (px/sec)
    const durationSec = Math.max(0.1, translatePx / props.speed);

    // Set CSS custom property and inline animation (keeps it dynamic)
    track.value.style.setProperty("--marquee-translate", `${translatePx}px`);
    track.value.style.animation = `marqueeScroll ${durationSec}s linear infinite`;
    // ensure the animation-play-state is running after rebuild
    track.value.style.animationPlayState = "running";
  });
}

function pause() {
  if (track.value) track.value.style.animationPlayState = "paused";
}
function resume() {
  if (track.value) track.value.style.animationPlayState = "running";
}

onMounted(() => {
  // Build initially
  buildMarquee();

  // Rebuild on resize using ResizeObserver for better responsiveness
  resizeObserver = new ResizeObserver(() => buildMarquee());
  if (container.value) resizeObserver.observe(container.value);
  if (content.value) resizeObserver.observe(content.value);
});

// cleanup
onBeforeUnmount(() => {
  if (resizeObserver) resizeObserver.disconnect();
});

// Rebuild if speed prop changes
watch(
  () => props.speed,
  () => buildMarquee()
);
</script>

<style scoped>
.marquee {
  overflow: hidden;
  width: 100%;
  box-sizing: border-box;
}

/* track holds the original + clones in a row */
.marquee-track {
  display: inline-flex;
  align-items: center;
  gap: 1.5rem; /* spacing between items */
  /* animation will be set dynamically from JS, but keyframe uses --marquee-translate */
}

/* ensure each content block doesn't flex/shrink (keeps measured width stable) */
.marquee-content {
  display: inline-flex;
  flex: 0 0 auto;
}

/* keyframes animate exactly by the measured pixel distance */
@keyframes marqueeScroll {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(calc(-1 * var(--marquee-translate)));
  }
}

/* optional: pause on hover (JS pause already wired but keep this for extra compatibility) */
.marquee:hover .marquee-track {
  animation-play-state: paused;
}
</style>
