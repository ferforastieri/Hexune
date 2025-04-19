<template>
  <section id="home" class="hero">
    <div class="hero-content">
      <div class="hero-text">
        <h1 class="hero-title">
          <span class="title-line">Olá, eu sou</span>
          <span class="title-line highlight">Fernando</span>
        </h1>
        <div class="hero-roles">
          <span class="role">Frontend Developer</span>
          <span class="role">DevOps Engineer</span>
          <span class="role">Hardware Enthusiast</span>
        </div>
        <p class="hero-description">
          Transformando ideias em experiências digitais memoráveis. 
          Combinando desenvolvimento, infraestrutura e hardware para criar 
          soluções completas e impactantes.
        </p>
        <div class="hero-buttons">
          <a href="#projects" class="btn btn-primary">Ver Projetos</a>
          <a href="#contact" class="btn btn-secondary">Contato</a>
        </div>
      </div>
      <div class="hero-visual">
        <div class="skills-showcase">
          <div class="flip-card" 
               v-for="(skill, index) in skills" 
               :key="index"
               @click="flipCard(index)"
               :class="{ 'is-flipped': flippedCards[index] }">
            <div class="flip-card-inner">
              <div class="flip-card-front">
                <div class="skill-icon">
                  <img :src="skill.icon" :alt="skill.name" />
                </div>
                <h3 class="skill-name">{{ skill.name }}</h3>
                <p class="skill-preview">{{ skill.preview }}</p>
                <div class="flip-hint">Clique para ver mais</div>
              </div>
              <div class="flip-card-back">
                <SkillInteractions :skill-type="skill.type" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import SkillInteractions from '../interactions/SkillInteractions.vue'

const flippedCards = ref([false, false, false])

const skills = [
  {
    name: 'Frontend',
    type: 'frontend',
    icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg',
    preview: 'Interfaces modernas e reativas'
  },
  {
    name: 'DevOps',
    type: 'devops',
    icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg',
    preview: 'Infraestrutura e automação'
  },
  {
    name: 'Hardware',
    type: 'hardware',
    icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/raspberrypi/raspberrypi-original.svg',
    preview: 'Projetos de automação'
  }
]

const flipCard = (index) => {
  flippedCards.value[index] = !flippedCards.value[index]
}
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  padding: 2rem;
  padding-top: 6rem;
  position: relative;
  overflow: hidden;
}

.hero-content {
  max-width: 1400px;
  margin: 0 auto;
  width: 100%;
}

.hero-text {
  position: relative;
  z-index: 2;
  text-align: center;
  margin-bottom: 4rem;
}

.hero-title {
  display: flex;
  flex-direction: column;
  margin-bottom: 2rem;
  align-items: center;
}

.title-line {
  display: block;
  font-size: clamp(2.5rem, 5vw, 4rem);
  line-height: 1.1;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.title-line.highlight {
  background: var(--gradient-secondary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero-roles {
  display: flex;
  gap: 1rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
  justify-content: center;
}

.role {
  background: rgba(255, 255, 255, 0.1);
  padding: 0.5rem 1rem;
  border-radius: 2rem;
  font-size: 0.9rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  color: var(--text-color);
}

.role:hover {
  background: var(--gradient-primary);
  color: white;
  transform: translateY(-2px);
}

.hero-description {
  max-width: 600px;
  margin: 0 auto 3rem;
  font-size: clamp(1rem, 2vw, 1.1rem);
  line-height: 1.8;
  color: var(--text-color);
}

.hero-buttons {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
}

.btn {
  padding: 1rem 2rem;
  border-radius: 0.5rem;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
  z-index: 1;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.btn-primary {
  background: var(--gradient-primary);
  color: white;
  border: none;
}

.btn-primary:hover {
  transform: translateY(-2px);
}

.btn-secondary {
  background: transparent;
  border: 2px solid transparent;
  background-clip: padding-box;
  position: relative;
}

.btn-secondary::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: var(--gradient-primary);
  border-radius: 0.5rem;
  z-index: -2;
}

.btn-secondary::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: white;
  border-radius: 0.5rem;
  z-index: -1;
  transition: opacity 0.3s ease;
}

.btn-secondary:hover {
  color: white;
  transform: translateY(-2px);
}

.btn-secondary:hover::after {
  opacity: 0;
}

.hero-visual {
  position: relative;
  width: 100%;
  margin-top: 4rem;
  padding: 0 1rem;
}

.skills-showcase {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

.flip-card {
  background-color: transparent;
  height: 400px;
  perspective: 1000px;
  cursor: pointer;
  width: 100%;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.flip-card.is-flipped .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 1.5rem;
  border-radius: 1rem;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.flip-card-front {
  background-color: white;
  color: var(--text-color);
}

.flip-card-back {
  background-color: white;
  color: var(--text-color);
  transform: rotateY(180deg);
}

.skill-icon {
  width: 60px;
  height: 60px;
  margin-bottom: 1rem;
  transition: transform 0.3s ease;
}

.flip-card:hover .skill-icon {
  transform: scale(1.1);
}

.skill-name {
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--secondary-color);
  margin-bottom: 0.5rem;
}

.skill-preview {
  color: var(--text-color);
  font-size: 0.9rem;
  margin-bottom: 1rem;
}

.flip-hint {
  font-size: 0.8rem;
  color: var(--primary-color);
  opacity: 0.7;
  margin-top: auto;
}

@media (max-width: 1024px) {
  .skills-showcase {
    grid-template-columns: repeat(3, 1fr);
    gap: 1.5rem;
  }

  .flip-card {
    height: 350px;
  }
}

@media (max-width: 768px) {
  .hero {
    padding: 1rem;
    padding-top: 6rem;
  }

  .hero-visual {
    margin-top: 2rem;
    padding: 0;
  }

  .skills-showcase {
    grid-template-columns: 1fr;
    gap: 1rem;
    padding: 0 1rem;
  }

  .flip-card {
    height: 300px;
    max-width: 400px;
    margin: 0 auto;
  }

  .flip-card-front,
  .flip-card-back {
    padding: 1rem;
  }
}

@media (max-width: 480px) {
  .flip-card {
    height: 250px;
  }
}
</style> 