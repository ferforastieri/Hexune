<template>
  <section id="home" class="hero">
    <div class="hero-content">
      <div class="hero-text">
        <h1 class="hero-title">
          <span class="title-line">Olá, eu sou</span>
          <span class="title-line highlight">Fernando</span>
        </h1>
        <div class="hero-roles">
          <span class="role">Desenvolvedor</span>
          <span class="role">Designer</span>
          <span class="role">Criativo</span>
        </div>
        <p class="hero-description">
          Transformando ideias em experiências digitais memoráveis. 
          Combinando desenvolvimento, design e criatividade para criar 
          soluções únicas e impactantes.
        </p>
        <div class="hero-buttons">
          <a href="#projects" class="btn btn-primary">Ver Projetos</a>
          <a href="#contact" class="btn btn-secondary">Contato</a>
        </div>
      </div>
      <div class="hero-visual">
        <div class="visual-container">
          <div class="visual-element" v-for="(element, index) in visualElements" 
               :key="index" 
               :style="element.style">
            <span class="element-text">{{ element.text }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const visualElements = ref([
  { text: 'Code', style: { top: '10%', left: '20%', transform: 'rotate(-15deg)' } },
  { text: 'Design', style: { top: '30%', right: '15%', transform: 'rotate(10deg)' } },
  { text: 'Create', style: { bottom: '20%', left: '25%', transform: 'rotate(-5deg)' } },
  { text: 'Innovate', style: { bottom: '40%', right: '20%', transform: 'rotate(15deg)' } }
])

onMounted(() => {
  // Adiciona animação aos elementos visuais
  const elements = document.querySelectorAll('.visual-element')
  elements.forEach((element, index) => {
    element.style.animation = `fadeIn 0.5s ease forwards ${index * 0.2}s`
  })
})
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 0 2rem;
  position: relative;
  overflow: hidden;
}

.hero-content {
  max-width: 1400px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.hero-text {
  position: relative;
  z-index: 2;
}

.hero-title {
  display: flex;
  flex-direction: column;
  margin-bottom: 2rem;
}

.title-line {
  display: block;
  font-size: clamp(2.5rem, 5vw, 4rem);
  line-height: 1.1;
}

.highlight {
  color: var(--primary-color);
}

.hero-roles {
  display: flex;
  gap: 1rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.role {
  background-color: var(--background-alt);
  padding: 0.5rem 1rem;
  border-radius: 2rem;
  font-size: 0.9rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.3s ease;
}

.role:hover {
  background-color: var(--primary-color);
  color: white;
  transform: translateY(-2px);
}

.hero-description {
  max-width: 600px;
  margin-bottom: 3rem;
  font-size: clamp(1rem, 2vw, 1.1rem);
  line-height: 1.8;
}

.hero-visual {
  position: relative;
  height: 500px;
}

.visual-container {
  position: relative;
  width: 100%;
  height: 100%;
}

.visual-element {
  position: absolute;
  background-color: white;
  padding: 1rem 2rem;
  border-radius: 0.5rem;
  box-shadow: var(--shadow-lg);
  opacity: 0;
  transform-origin: center;
  transition: all 0.3s ease;
}

.visual-element:hover {
  transform: scale(1.1) rotate(0deg) !important;
  background-color: var(--primary-color);
  color: white;
}

.element-text {
  font-weight: 600;
  font-size: 1.2rem;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.hero-buttons {
  display: flex;
  gap: 1.5rem;
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
  background: linear-gradient(45deg, var(--secondary-color), var(--primary-color));
  color: white;
  border: none;
}

.btn-primary::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
  opacity: 0;
  transition: opacity 0.3s ease;
  z-index: -1;
}

.btn-primary:hover {
  transform: translateY(-2px);
}

.btn-primary:hover::before {
  opacity: 1;
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
  background: linear-gradient(45deg, var(--secondary-color), var(--primary-color));
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

@media (max-width: 1024px) {
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 2rem;
  }

  .hero-description {
    margin: 0 auto 3rem;
  }

  .hero-buttons {
    justify-content: center;
  }

  .hero-visual {
    height: 400px;
    margin-top: 2rem;
  }
}

@media (max-width: 768px) {
  .hero {
    padding-top: 6rem;
  }

  .hero-roles {
    justify-content: center;
  }

  .visual-element {
    padding: 0.8rem 1.5rem;
  }

  .element-text {
    font-size: 1rem;
  }
}
</style> 