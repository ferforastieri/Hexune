<template>
  <div class="skill-interaction" :class="skillType">
    <!-- Frontend Interaction -->
    <div v-if="skillType === 'frontend'" class="frontend-demo">
      <div class="code-editor">
        <div class="editor-header">
          <span class="dot red"></span>
          <span class="dot yellow"></span>
          <span class="dot green"></span>
          <span class="file-name">App.vue</span>
        </div>
        <div class="editor-content">
          <pre><code>{{ frontendCode }}</code></pre>
        </div>
      </div>
      <div class="preview-window">
        <div class="preview-header">
          <span>Preview</span>
        </div>
        <div class="preview-content">
          <div class="demo-button" @click="animateButton">
            <span>Hover Me!</span>
          </div>
        </div>
      </div>
    </div>

    <!-- DevOps Interaction -->
    <div v-if="skillType === 'devops'" class="devops-demo">
      <div class="terminal">
        <div class="terminal-header">
          <span>Terminal</span>
        </div>
        <div class="terminal-content">
          <div class="command-line" v-for="(cmd, index) in devopsCommands" :key="index">
            <span class="prompt">$</span>
            <span class="command">{{ cmd.command }}</span>
            <div class="output" v-if="cmd.output">{{ cmd.output }}</div>
          </div>
        </div>
      </div>
      <div class="container-status">
        <div class="container" v-for="(container, index) in containers" :key="index">
          <div class="container-icon" :class="{ 'running': container.status === 'running' }">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" alt="Docker" />
          </div>
          <span class="container-name">{{ container.name }}</span>
        </div>
      </div>
    </div>

    <!-- Hardware Interaction -->
    <div v-if="skillType === 'hardware'" class="hardware-demo">
      <div class="circuit-board">
        <div class="led" :class="{ 'active': ledActive }" @click="toggleLed"></div>
        <div class="sensor" :class="{ 'active': sensorActive }">
          <span class="sensor-value">{{ sensorValue }}°C</span>
        </div>
        <div class="connections">
          <div class="connection" v-for="n in 3" :key="n" :class="{ 'active': ledActive }"></div>
        </div>
      </div>
      <div class="hardware-controls">
        <button @click="toggleLed" class="control-btn">
          {{ ledActive ? 'Desligar LED' : 'Ligar LED' }}
        </button>
        <button @click="readSensor" class="control-btn">
          Ler Sensor
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const props = defineProps({
  skillType: {
    type: String,
    required: true
  }
})

// Frontend Demo
const frontendCode = `// Componente Vue.js
<template>
  <button class="animated-btn">
    Clique em mim!
  </button>
</template>

<style scoped>
.animated-btn {
  background: var(--gradient-primary);
  color: white;
  padding: 1rem 2rem;
  border-radius: 0.5rem;
  transition: transform 0.3s;
}

.animated-btn:hover {
  transform: scale(1.1);
}
</style>`

// DevOps Demo
const devopsCommands = ref([
  { command: 'docker ps', output: 'CONTAINER ID   IMAGE     STATUS    PORTS' },
  { command: 'docker-compose up -d', output: 'Starting services...' },
  { command: 'kubectl get pods', output: 'NAME    READY   STATUS    RESTARTS' }
])

const containers = ref([
  { name: 'web-app', status: 'running' },
  { name: 'database', status: 'running' },
  { name: 'cache', status: 'stopped' }
])

// Hardware Demo
const ledActive = ref(false)
const sensorActive = ref(false)
const sensorValue = ref(25)

const toggleLed = () => {
  ledActive.value = !ledActive.value
}

const readSensor = () => {
  sensorActive.value = true
  sensorValue.value = Math.floor(Math.random() * 10) + 20
  setTimeout(() => {
    sensorActive.value = false
  }, 1000)
}

const animateButton = () => {
  // Animation logic for frontend demo
}
</script>

<style scoped>
.skill-interaction {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  padding: 1rem;
  background: white;
  border-radius: 1rem;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

/* Frontend Demo Styles */
.frontend-demo {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  height: 100%;
  align-items: center;
}

.code-editor {
  background: #1e1e1e;
  border-radius: 0.5rem;
  overflow: hidden;
  height: 100%;
  display: flex;
  flex-direction: column;
}

.editor-header {
  background: #2d2d2d;
  padding: 0.5rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
}

.dot.red { background: #ff5f56; }
.dot.yellow { background: #ffbd2e; }
.dot.green { background: #27c93f; }

.file-name {
  color: #888;
  margin-left: 1rem;
}

.editor-content {
  padding: 1rem;
  font-family: 'Fira Code', monospace;
  color: #d4d4d4;
  flex: 1;
  overflow-y: auto;
}

.preview-window {
  background: white;
  border-radius: 0.5rem;
  overflow: hidden;
  height: 100%;
  display: flex;
  flex-direction: column;
}

.preview-header {
  background: #f5f5f5;
  padding: 0.5rem;
  border-bottom: 1px solid #ddd;
}

.preview-content {
  padding: 2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex: 1;
}

.demo-button {
  background: var(--gradient-primary);
  color: white;
  padding: 1rem 2rem;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: transform 0.3s;
}

.demo-button:hover {
  transform: scale(1.1);
}

/* DevOps Demo Styles */
.devops-demo {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 1rem;
  height: 100%;
  align-items: center;
}

.terminal {
  background: #1e1e1e;
  border-radius: 0.5rem;
  overflow: hidden;
  height: 100%;
  display: flex;
  flex-direction: column;
}

.terminal-header {
  background: #2d2d2d;
  padding: 0.5rem;
  color: #888;
}

.terminal-content {
  padding: 1rem;
  font-family: 'Fira Code', monospace;
  flex: 1;
  overflow-y: auto;
}

.command-line {
  margin-bottom: 0.5rem;
}

.prompt {
  color: #42b883;
  margin-right: 0.5rem;
}

.command {
  color: white;
}

.output {
  color: #888;
  margin-left: 1.5rem;
}

.container-status {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  height: 100%;
  justify-content: center;
}

.container {
  background: white;
  padding: 1rem;
  border-radius: 0.5rem;
  display: flex;
  align-items: center;
  gap: 1rem;
}

.container-icon {
  width: 40px;
  height: 40px;
  opacity: 0.5;
}

.container-icon.running {
  opacity: 1;
}

/* Hardware Demo Styles */
.hardware-demo {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  height: 100%;
  justify-content: center;
}

.circuit-board {
  background: #2d2d2d;
  border-radius: 0.5rem;
  padding: 2rem;
  position: relative;
  height: 200px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.led {
  width: 30px;
  height: 30px;
  background: #ccc;
  border-radius: 50%;
  position: absolute;
  top: 50%;
  left: 30%;
  cursor: pointer;
  transition: background 0.3s;
}

.led.active {
  background: #ff4444;
  box-shadow: 0 0 20px #ff4444;
}

.sensor {
  width: 40px;
  height: 40px;
  background: #444;
  border-radius: 50%;
  position: absolute;
  top: 50%;
  right: 30%;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: background 0.3s;
}

.sensor.active {
  background: #42b883;
}

.sensor-value {
  color: white;
  font-size: 0.8rem;
}

.connections {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  height: 2px;
  background: #444;
}

.connection {
  position: absolute;
  width: 20px;
  height: 2px;
  background: #444;
  transition: background 0.3s;
}

.connection.active {
  background: #42b883;
}

.hardware-controls {
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin-top: auto;
}

.control-btn {
  background: var(--gradient-primary);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  border: none;
  cursor: pointer;
  transition: transform 0.3s;
}

.control-btn:hover {
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .frontend-demo,
  .devops-demo {
    grid-template-columns: 1fr;
  }

  .code-editor,
  .terminal {
    height: 200px;
  }

  .preview-window {
    height: 200px;
  }
}
</style> 