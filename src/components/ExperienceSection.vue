<script setup lang="ts">
import { nextTick, onBeforeUnmount, onMounted, ref } from 'vue'
import SectionHeading from '@/components/SectionHeading.vue'

interface ExperienceItem {
  id: number
  company: string
  position: string
  period: string
  description: string
  highlights: string[]
  technologies: string[]
}

defineProps<{
  experiences: ExperienceItem[]
}>()

const section = ref<HTMLElement | null>(null)
const pathSvg = ref<SVGSVGElement | null>(null)
const bgPath = ref<SVGPathElement | null>(null)
const fgPath = ref<SVGPathElement | null>(null)
const traveler = ref<SVGCircleElement | null>(null)
const travelerHalo = ref<SVGCircleElement | null>(null)

const nodes = ref<{ x: number; y: number; length: number }[]>([])
const activeNodeIndex = ref(-1)
const isInitialized = ref(false)

let milestoneEls: HTMLElement[] = []
let pathLength = 0

function lengthAtY(targetY: number, totalLen: number) {
  let lo = 0
  let hi = totalLen

  for (let i = 0; i < 25; i += 1) {
    const mid = (lo + hi) / 2
    const point = fgPath.value?.getPointAtLength(mid)
    if (!point) break

    if (point.y < targetY) lo = mid
    else hi = mid
  }

  return (lo + hi) / 2
}

function buildPath() {
  if (!section.value || !pathSvg.value || !bgPath.value || !fgPath.value) return 0

  const height = Math.max(section.value.offsetHeight, 400)
  pathSvg.value.setAttribute('viewBox', `0 0 120 ${height}`)

  const segmentCount = Math.max(1, milestoneEls.length)
  const segmentHeight = height / segmentCount
  let d = 'M60,0'
  const midpoints: number[] = []

  for (let i = 0; i < segmentCount; i += 1) {
    const midpoint = segmentHeight * i + segmentHeight * 0.5
    const endY = segmentHeight * (i + 1)
    const swing = i % 2 === 0 ? 40 : 80
    d += ` C ${swing},${midpoint} ${120 - swing},${midpoint} 60,${endY}`
    midpoints.push(midpoint)
  }

  bgPath.value.setAttribute('d', d)
  fgPath.value.setAttribute('d', d)

  const total = fgPath.value.getTotalLength()
  
  const newNodes: { x: number; y: number; length: number }[] = []
  midpoints.forEach((y) => {
    const len = lengthAtY(y, total)
    const point = fgPath.value?.getPointAtLength(len)
    if (point) {
      newNodes.push({ x: point.x, y: point.y, length: len })
    }
  })
  nodes.value = newNodes

  return total
}

function updateMilestones() {
  if (!section.value) return

  const viewportHeight = window.innerHeight
  const documentHeight = document.documentElement.scrollHeight
  const sectionTop = section.value.offsetTop
  const sectionHeight = section.value.offsetHeight
  const sectionBottom = sectionTop + sectionHeight
  const scrollY = window.scrollY || window.pageYOffset
  const maxScroll = documentHeight - viewportHeight
  const startScroll = sectionTop - viewportHeight * 0.9
  const endScroll = Math.min(sectionBottom - viewportHeight * 0.1, maxScroll)

  let progress = (scrollY - startScroll) / (endScroll - startScroll)
  progress = Math.max(0, Math.min(1, progress))

  // Set path length to 0 until page initialization is complete or user scrolls
  if (!isInitialized.value) {
    progress = 0
  }

  if (fgPath.value) {
    const drawLength = Math.min(pathLength * progress, pathLength - 0.01)
    fgPath.value.style.strokeDashoffset = String(Math.max(pathLength - drawLength, 0))

    const point = fgPath.value.getPointAtLength(Math.max(drawLength, 0))
    if (traveler.value) {
      traveler.value.setAttribute('cx', String(point.x))
      traveler.value.setAttribute('cy', String(point.y))
    }
    if (travelerHalo.value) {
      travelerHalo.value.setAttribute('cx', String(point.x))
      travelerHalo.value.setAttribute('cy', String(point.y))
    }

    const mergeRange = (pathLength / Math.max(nodes.value.length, 1)) * 0.3
    let travelerRadius = 8
    let currentActiveIdx = -1

    nodes.value.forEach((node, index) => {
      const distance = Math.abs(drawLength - node.length)
      const visited = drawLength >= node.length - 1

      if (visited) {
        currentActiveIdx = index
      }

      const milestoneEl = milestoneEls[index]
      if (milestoneEl) {
        milestoneEl.classList.toggle('active', visited)
      }

      if (distance < mergeRange) {
        const t = 1 - distance / mergeRange
        const eased = t * t * (3 - 2 * t)
        travelerRadius = Math.max(travelerRadius, 8 + (13 - 8) * eased)
      }
    })

    activeNodeIndex.value = currentActiveIdx

    if (traveler.value) {
      traveler.value.setAttribute('r', String(travelerRadius))
    }
    if (travelerHalo.value) {
      travelerHalo.value.setAttribute('r', String(travelerRadius * 1.8))
    }
  }

  milestoneEls.forEach((milestone) => {
    const rect = milestone.getBoundingClientRect()
    if (rect.top < viewportHeight * 0.8) {
      milestone.classList.add('visible')
    }
  })
}

function scrollToMilestone(index: number) {
  const milestoneEl = milestoneEls[index]
  if (milestoneEl) {
    const yOffset = -120 // Space for floating navbar
    const y = milestoneEl.getBoundingClientRect().top + window.scrollY + yOffset
    window.scrollTo({ top: y, behavior: 'smooth' })
  }
}

let resizeObserver: ResizeObserver | null = null

onMounted(() => {
  let handleScroll: () => void

  nextTick(() => {
    if (!section.value) return
    milestoneEls = Array.from(section.value.querySelectorAll('.milestone')) as HTMLElement[]
    pathLength = buildPath()
    if (fgPath.value) {
      fgPath.value.style.strokeDasharray = String(pathLength)
      fgPath.value.style.strokeDashoffset = String(pathLength)
    }
    updateMilestones()

    handleScroll = () => {
      if (!isInitialized.value) {
        isInitialized.value = true
      }
      updateMilestones()
    }
    window.addEventListener('scroll', handleScroll, { passive: true })
    window.addEventListener('resize', handleScroll)

    resizeObserver = new ResizeObserver(() => {
      pathLength = buildPath()
      if (fgPath.value) {
        fgPath.value.style.strokeDasharray = String(pathLength)
        fgPath.value.style.strokeDashoffset = String(pathLength)
      }
      updateMilestones()
    })

    if (section.value) {
      resizeObserver.observe(section.value)
    }

    // Force animation from 0 after a small delay on initial page load
    setTimeout(() => {
      if (!isInitialized.value) {
        isInitialized.value = true
        updateMilestones()
      }
    }, 450)
  })

  onBeforeUnmount(() => {
    if (handleScroll) {
      window.removeEventListener('scroll', handleScroll)
      window.removeEventListener('resize', handleScroll)
    }
    resizeObserver?.disconnect()
    resizeObserver = null
  })
})
</script>

<template>
  <section id="experience" class="section path-section" ref="section">
    <div class="container">
      <SectionHeading
        eyebrow="Career path"
        title="Experience shaping thoughtful product interfaces."
        description="My work has centered on turning complex product needs into elegant, reliable user experiences that feel calm and effortless."
      />

      <div class="path-layout">
        <svg ref="pathSvg" class="path-svg" viewBox="0 0 120 3000" preserveAspectRatio="none">
          <defs>
            <linearGradient id="pathGradient" x1="0%" y1="0%" x2="0%" y2="100%">
              <stop offset="0%" stop-color="#3b82f6" />
              <stop offset="50%" stop-color="#8b5cf6" />
              <stop offset="100%" stop-color="#ec4899" />
            </linearGradient>
            <filter id="glow" x="-35%" y="-35%" width="170%" height="170%">
              <feGaussianBlur stdDeviation="5" result="blur" />
              <feMerge>
                <feMergeNode in="blur" />
                <feMergeNode in="SourceGraphic" />
              </feMerge>
            </filter>
          </defs>
          <path ref="bgPath" class="path-bg" d="" />
          <path ref="fgPath" class="path-fg" d="" filter="url(#glow)" />
          
          <!-- Node Dots rendered reactively -->
          <g class="nodes-group">
            <g
              v-for="(node, idx) in nodes"
              :key="idx"
              class="node-group"
              :class="{ 'visited': activeNodeIndex >= idx, 'active-current': activeNodeIndex === idx }"
              @click="scrollToMilestone(idx)"
            >
              <!-- Interactive hover zone -->
              <circle
                :cx="node.x"
                :cy="node.y"
                r="24"
                fill="transparent"
                style="cursor: pointer; pointer-events: all;"
              />
              <!-- Glowing ring -->
              <circle
                class="node-ring"
                :cx="node.x"
                :cy="node.y"
                r="10"
              />
              <!-- Inner dot -->
              <circle
                class="node-dot"
                :cx="node.x"
                :cy="node.y"
                r="5"
              />
            </g>
          </g>

          <!-- Double pulsing traveler -->
          <circle ref="travelerHalo" class="traveler-halo" r="14" />
          <circle ref="traveler" class="traveler" r="8" />
        </svg>

        <div class="milestones">
          <article v-for="(exp, index) in experiences" :key="exp.id" class="milestone" :class="{ left: index % 2 === 0, right: index % 2 === 1 }">
            <div class="card">
              <span class="date">{{ exp.period }}</span>
              <h3>{{ exp.position }}</h3>
              <p class="company">{{ exp.company }}</p>
              <p class="description">{{ exp.description }}</p>

              <ul v-if="exp.highlights.length > 0" class="highlights">
                <li v-for="(highlight, idx) in exp.highlights" :key="idx">{{ highlight }}</li>
              </ul>

              <div v-if="exp.technologies.length > 0" class="tech-tags">
                <span v-for="tech in exp.technologies" :key="tech">{{ tech }}</span>
              </div>
            </div>
          </article>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.path-section {
  min-height: calc(100vh - 5rem);
  padding: 5.5rem 0 6rem;
}

.path-layout {
  position: relative;
  display: block;
  width: min(100vw - 3rem, 1100px);
  margin: 0 auto;
  padding: 0 1.5rem;
}

.path-svg {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 160px;
  height: 100%;
  overflow: visible;
  pointer-events: none;
  z-index: 1;
}

.path-bg,
.path-fg {
  fill: none;
  stroke-width: 2.5;
}

.path-bg {
  stroke: rgba(255, 255, 255, 0.12);
}

.path-fg {
  stroke: url(#pathGradient);
  stroke-linecap: round;
  transition: stroke-dashoffset 0.2s ease;
}

.traveler {
  fill: #ffffff;
  stroke: var(--accent-strong);
  stroke-width: 2.5;
  filter: drop-shadow(0 0 10px rgba(217, 70, 239, 0.7));
  transition: r 0.25s cubic-bezier(0.16, 1, 0.3, 1), stroke 0.25s;
}

.traveler-halo {
  fill: rgba(96, 165, 250, 0.12);
  stroke: rgba(96, 165, 250, 0.3);
  animation: pulse-ring 2s infinite ease-in-out;
  pointer-events: none;
  transition: r 0.25s cubic-bezier(0.16, 1, 0.3, 1);
}

@keyframes pulse-ring {
  0% {
    stroke-width: 1px;
    opacity: 0.8;
  }
  50% {
    stroke-width: 3.5px;
    opacity: 0.3;
  }
  100% {
    stroke-width: 1px;
    opacity: 0.8;
  }
}

/* Node Dot Styling */
.node-group {
  cursor: pointer;
}

.node-ring {
  fill: #090e1d;
  stroke: rgba(255, 255, 255, 0.12);
  stroke-width: 2;
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  transform-origin: center;
}

.node-dot {
  fill: rgba(255, 255, 255, 0.3);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  transform-origin: center;
}

/* Visited node styling */
.node-group.visited .node-ring {
  stroke: var(--accent);
  fill: rgba(96, 165, 250, 0.1);
  filter: drop-shadow(0 0 8px rgba(96, 165, 250, 0.4));
}

.node-group.visited .node-dot {
  fill: var(--accent);
}

/* Current active node styling */
.node-group.active-current .node-ring {
  stroke: var(--accent-strong);
  fill: rgba(217, 70, 239, 0.15);
  filter: drop-shadow(0 0 12px rgba(217, 70, 239, 0.6));
  r: 12;
}

.node-group.active-current .node-dot {
  fill: var(--accent-strong);
  r: 6;
}

/* Hover effects */
.node-group:hover .node-ring {
  stroke: var(--success);
  fill: rgba(94, 234, 212, 0.15);
  filter: drop-shadow(0 0 10px rgba(94, 234, 212, 0.6));
  r: 13;
}

.node-group:hover .node-dot {
  fill: var(--success);
  r: 7.5;
}

.milestone.active .card {
  background: linear-gradient(180deg, rgba(96, 165, 250, 0.08), rgba(168, 85, 247, 0.05));
  border-color: rgba(96, 165, 250, 0.3);
  box-shadow: 0 45px 120px rgba(96, 165, 250, 0.08), 0 8px 30px rgba(0,0,0,0.35);
  transform: translateY(-8px) scale(1.01);
}

.milestone.active .card h3 {
  color: #eaf2ff;
}

.milestones {
  display: grid;
  gap: 5rem;
  position: relative;
  z-index: 2;
}

.milestone {
  display: grid;
  grid-template-columns: 1fr 160px 1fr;
  align-items: start;
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.milestone.visible {
  opacity: 1;
  transform: translateY(0);
}

.milestone.left .card {
  grid-column: 1;
  justify-self: end;
  width: 100%;
  max-width: 860px;
}

.milestone.right .card {
  grid-column: 3;
  justify-self: start;
  width: 100%;
  max-width: 860px;
}

.card {
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 1.75rem;
  padding: 2rem 2.2rem;
  max-width: 100%;
  min-height: 260px;
  box-shadow: 0 35px 90px rgba(0, 0, 0, 0.25);
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1), border-color 0.4s, background-color 0.4s, box-shadow 0.4s;
}

.date {
  display: block;
  margin-bottom: 0.75rem;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.82rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--success);
}

.card h3 {
  margin: 0;
  font-size: clamp(1.4rem, 2vw, 1.9rem);
  line-height: 1.1;
  color: var(--text);
}

.company {
  margin: 0.65rem 0 0;
  color: var(--text-soft);
  font-weight: 600;
  font-size: 1rem;
}

.description {
  margin: 1rem 0 0;
  line-height: 1.8;
  color: var(--text-soft);
  font-size: 0.98rem;
  max-width: 48rem;
}

.highlights {
  margin-top: 1.4rem;
  list-style: none;
  display: grid;
  gap: 0.8rem;
  padding: 0;
}

.highlights li {
  display: flex;
  gap: 0.8rem;
  align-items: flex-start;
  color: var(--text-soft);
  line-height: 1.7;
}

.highlights li::before {
  content: '';
  display: inline-block;
  width: 0.55rem;
  height: 0.55rem;
  margin-top: 0.35rem;
  border-radius: 999px;
  background: var(--success);
  flex-shrink: 0;
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
  margin-top: 1.2rem;
}

.tech-tags span {
  padding: 0.45rem 0.75rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.12);
  color: var(--text-soft);
  font-size: 0.86rem;
}

@media (max-width: 1024px) {
  .path-layout {
    display: block;
    width: 100%;
    padding-left: 5.5rem;
    padding-right: 1.5rem;
    margin: 0;
  }

  .milestone {
    grid-template-columns: 1fr;
    gap: 0;
  }

  .milestone.left .card,
  .milestone.right .card {
    grid-column: 1;
    justify-self: stretch;
    max-width: 100%;
  }

  .path-svg {
    left: 0.5rem;
    transform: none;
    width: 80px;
  }

  .milestone.left .card,
  .milestone.right .card {
    padding: 1.8rem;
  }
}

@media (max-width: 760px) {
  .path-layout {
    padding-left: 4.5rem;
    padding-right: 1rem;
  }

  .path-svg {
    left: 0.25rem;
    width: 70px;
  }

  .card {
    padding: 1.4rem;
  }

  .description {
    font-size: 0.98rem;
  }

  .milestones {
    gap: 3rem;
  }
}
</style>
