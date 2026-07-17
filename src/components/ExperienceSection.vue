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
let milestoneEls: HTMLElement[] = []
let nodeLengths: number[] = []
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

function renderNodeHalos() {
  const svg = pathSvg.value
  if (!svg) return

  svg.querySelectorAll('.node-dot').forEach((el) => el.remove())

  nodeLengths.forEach((len, index) => {
    const point = fgPath.value?.getPointAtLength(len)
    if (!point) return

    const dot = document.createElementNS('http://www.w3.org/2000/svg', 'circle')
    dot.setAttribute('class', 'node-dot')
    dot.setAttribute('data-index', index.toString())
    dot.setAttribute('cx', String(point.x))
    dot.setAttribute('cy', String(point.y))
    dot.setAttribute('r', '12')
    dot.setAttribute('fill', 'rgba(234, 234, 255, 0.98)')
    dot.setAttribute('stroke', 'rgba(96,165,250,0.9)')
    dot.setAttribute('stroke-width', '2')
    dot.setAttribute('pointer-events', 'none')

    const travelerNode = traveler.value
    if (travelerNode) {
      svg.insertBefore(dot, travelerNode)
    } else {
      svg.appendChild(dot)
    }
  })
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
  nodeLengths = midpoints.map((y) => lengthAtY(y, total))
  renderNodeHalos()

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

  if (fgPath.value) {
    const drawLength = Math.min(pathLength * progress, pathLength - 0.01)
    fgPath.value.style.strokeDashoffset = String(Math.max(pathLength - drawLength, 0))

    const point = fgPath.value.getPointAtLength(Math.max(drawLength, 0))
    if (traveler.value) {
      traveler.value.setAttribute('cx', String(point.x))
      traveler.value.setAttribute('cy', String(point.y))
    }

    const mergeRange = (pathLength / Math.max(nodeLengths.length, 1)) * 0.3
    let travelerRadius = 10

    nodeLengths.forEach((length, index) => {
      const dot = pathSvg.value?.querySelector(`.node-dot[data-index="${index}"]`)

      const distance = Math.abs(drawLength - length)
      const visited = drawLength >= length - 1

      if (dot instanceof SVGElement) dot.classList.toggle('visited', visited)

      const milestoneEl = milestoneEls[index]
      if (milestoneEl) milestoneEl.classList.toggle('active', visited)

      if (distance < mergeRange) {
        const t = 1 - distance / mergeRange
        const eased = t * t * (3 - 2 * t)
        travelerRadius = Math.max(travelerRadius, 10 + (16 - 10) * eased)
      }
    })

    if (traveler.value) {
      traveler.value.setAttribute('r', String(travelerRadius))
    }
  }

  milestoneEls.forEach((milestone) => {
    const rect = milestone.getBoundingClientRect()
    if (rect.top < viewportHeight * 0.8) {
      milestone.classList.add('visible')
    }
  })
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

    handleScroll = () => updateMilestones()
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
            <linearGradient id="pathGradient" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="rgba(96, 165, 250, 0.9)" />
              <stop offset="100%" stop-color="rgba(168, 85, 247, 0.9)" />
            </linearGradient>
            <filter id="glow" x="-30%" y="-30%" width="160%" height="160%">
              <feGaussianBlur stdDeviation="3.5" result="blur" />
              <feMerge>
                <feMergeNode in="blur" />
                <feMergeNode in="SourceGraphic" />
              </feMerge>
            </filter>
          </defs>
          <path ref="bgPath" class="path-bg" d="" />
          <path ref="fgPath" class="path-fg" d="" filter="url(#glow)" />
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
  stroke: rgba(96, 165, 250, 0.85);
  stroke-width: 2;
  filter: drop-shadow(0 0 18px rgba(96, 165, 250, 0.55));
}

.node-dot {
  transition: transform 0.28s ease, filter 0.28s ease, stroke 0.28s ease;
  transform-origin: center;
}

.node-dot.visited {
  transform: scale(1.14);
  filter: drop-shadow(0 0 20px rgba(96,165,250,0.28));
}

.milestone.active .card {
  background: linear-gradient(180deg, rgba(96,165,250,0.06), rgba(168,85,247,0.04));
  border-color: rgba(96,165,250,0.28);
  box-shadow: 0 54px 140px rgba(96,165,250,0.06), 0 8px 30px rgba(0,0,0,0.25);
  transform: translateY(-6px);
}

.milestone.active .card h3 {
  color: #eaf2ff;
}

.milestones {
  display: grid;
  gap: 4rem;
  position: relative;
  z-index: 2;
}

.milestone {
  display: grid;
  grid-template-columns: 1fr 160px 1fr;
  align-items: start;
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.7s ease, transform 0.7s ease;
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
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.16);
  border-radius: 1.75rem;
  padding: 2rem 2.2rem;
  max-width: 100%;
  min-height: 260px;
  box-shadow: 0 42px 110px rgba(0, 0, 0, 0.22);
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
    grid-template-columns: 1fr;
    width: min(100vw - 2rem, 760px);
    left: 50%;
    transform: translateX(-50%);
  }

  .milestone {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .milestone.left .card,
  .milestone.right .card {
    grid-column: 1;
    justify-self: stretch;
    max-width: 100%;
  }

  .path-svg {
    left: 1.25rem;
    transform: none;
    width: 72px;
  }

  .milestone.left .card,
  .milestone.right .card {
    padding: 1.8rem;
  }
}

@media (max-width: 760px) {
  .path-svg {
    left: 1rem;
    width: 56px;
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
