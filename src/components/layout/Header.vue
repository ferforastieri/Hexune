<template>
  <header class="header" :class="{ 'scrolled': isScrolled }">
    <nav class="nav">
      <div class="logo" @click="scrollToTop">
        <div class="logo-content">
          <img src="../../assets/logo.png" alt="Logo" class="logo-img" />
          <div class="logo-text">
            <div class="text-container">
              <span class="text-line">Fer</span>
              <span class="text-line highlight">Tech</span>
            </div>
            <div class="logo-line"></div>
          </div>
        </div>
      </div>
      <div class="nav-toggle" @click="toggleMenu">
        <span class="bar" :class="{ 'active': isMenuOpen }"></span>
        <span class="bar" :class="{ 'active': isMenuOpen }"></span>
      </div>
      <ul class="nav-links" :class="{ 'active': isMenuOpen }">
        <li v-for="(link, index) in navLinks" :key="index">
          <a :href="link.href" 
             @click="closeMenu"
             :class="{ 'active': activeSection === link.href }">
            {{ link.text }}
            <span class="link-underline"></span>
          </a>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isMenuOpen = ref(false)
const isScrolled = ref(false)
const activeSection = ref('#home')

const navLinks = [
  { text: 'Artigos', href: '#articles' },
  { text: 'Sobre', href: '#about' },
  { text: 'Habilidades', href: '#skills' },
  { text: 'Curriculo', href: '#curriculo' },
  { text: 'Projetos', href: '#projects' },
  { text: 'Contato', href: '#contact' }
]

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
  
  // Atualiza a seção ativa
  const sections = document.querySelectorAll('section')
  for (const section of sections) {
    const sectionTop = section.offsetTop
    const sectionHeight = section.clientHeight
    if (window.scrollY >= sectionTop - 200 && window.scrollY < sectionTop + sectionHeight - 200) {
      activeSection.value = `#${section.id}`
    }
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  transition: all 0.3s ease;
}

.header.scrolled {
  background: rgba(255, 255, 255, 0.98);
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
}

.nav {
  max-width: 1400px;
  margin: 0 auto;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  align-items: center;
  gap: 1rem;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.logo:hover {
  transform: scale(1.05);
}

.logo-content {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.logo-text {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 0.5rem;
  line-height: 1;
}

.text-container {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.text-line {
  display: inline;
  font-size: 1.8rem;
  font-weight: 700;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  transition: all 0.3s ease;
}

.text-line.highlight {
  background: var(--gradient-secondary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.logo-img {
  height: 40px;
  width: auto;
  object-fit: contain;
  filter: none;
  background: linear-gradient(45deg, var(--secondary-color), var(--primary-color));
  -webkit-mask: url("../../assets/logo.png") center/contain no-repeat;
  mask: url("../../assets/logo.png") center/contain no-repeat;
  transition: all 0.3s ease;
}

.logo:hover .logo-img {
  transform: scale(1.1);
  background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
}

.logo-line {
  width: 100%;
  height: 2px;
  background: linear-gradient(45deg, var(--secondary-color), var(--primary-color));
  transform-origin: left;
  transition: transform 0.3s ease;
}

.logo:hover .logo-line {
  transform: scaleX(1.2);
  background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
}

.nav-toggle {
  display: none;
  cursor: pointer;
  z-index: 1001;
}

.bar {
  display: block;
  width: 25px;
  height: 3px;
  margin: 5px auto;
  background-color: var(--secondary-color);
  transition: all 0.3s ease;
}

.bar.active:nth-child(1) {
  transform: translateY(8px) rotate(45deg);
}

.bar.active:nth-child(2) {
  transform: translateY(-8px) rotate(-45deg);
}

.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
}

.nav-links a {
  text-decoration: none;
  color: var(--secondary-color);
  font-weight: 500;
  font-size: 1rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  position: relative;
  padding: 0.5rem 0;
  transition: all 0.3s ease;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.nav-links a::before {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--gradient-primary);
  transition: width 0.3s ease;
}

.nav-links a:hover,
.nav-links a.active {
  background: var(--gradient-secondary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.nav-links a:hover::before,
.nav-links a.active::before {
  width: 100%;
  background: var(--gradient-secondary);
}

@media (max-width: 768px) {
  .nav-toggle {
    display: block;
  }

  .nav-links {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: white;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 2rem;
    gap: 2rem;
    transform: translateX(100%);
    opacity: 0;
    transition: all 0.3s ease;
  }

  .nav-links.active {
    transform: translateX(0);
    opacity: 1;
  }

  .nav-links a {
    font-size: 1.2rem;
  }
}
</style> 