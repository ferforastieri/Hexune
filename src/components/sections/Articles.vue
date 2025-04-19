<template>
  <section id="articles" class="articles">
    <div class="container">
      <h2 class="section-title">Artigos</h2>
      <div class="articles-grid">
        <article v-for="(article, index) in articles" :key="index" class="article-card">
          <div class="article-image">
            <img :src="article.image" :alt="article.title" />
          </div>
          <div class="article-content">
            <h3 class="article-title">{{ article.title }}</h3>
            <p class="article-excerpt">{{ article.excerpt }}</p>
            <div class="article-meta">
              <span class="article-date">{{ article.date }}</span>
              <span class="article-category">{{ article.category }}</span>
            </div>
            <a :href="article.link" class="article-link">Ler mais</a>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
const articles = [
  {
    title: 'Título do Artigo 1',
    excerpt: 'Breve descrição do artigo...',
    date: '19/04/2024',
    category: 'Desenvolvimento',
    image: 'https://via.placeholder.com/300x200',
    link: '#'
  },
  {
    title: 'Título do Artigo 2',
    excerpt: 'Breve descrição do artigo...',
    date: '18/04/2024',
    category: 'Design',
    image: 'https://via.placeholder.com/300x200',
    link: '#'
  }
]
</script>

<style scoped>
.articles {
  padding: 5rem 0;
  background-color: var(--background-color);
}

.section-title {
  font-size: 2.5rem;
  margin-bottom: 3rem;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.articles-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.article-card {
  background: white;
  border-radius: 1rem;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.article-card:hover {
  transform: translateY(-5px);
}

.article-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
}

.article-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.article-card:hover .article-image img {
  transform: scale(1.1);
}

.article-content {
  padding: 1.5rem;
}

.article-title {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: var(--secondary-color);
}

.article-excerpt {
  color: var(--text-color);
  margin-bottom: 1rem;
  line-height: 1.6;
}

.article-meta {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
  font-size: 0.9rem;
  color: var(--text-color);
}

.article-link {
  display: inline-block;
  padding: 0.5rem 1rem;
  background: var(--gradient-primary);
  color: white;
  border-radius: 0.5rem;
  transition: all 0.3s ease;
}

.article-link:hover {
  background: var(--gradient-secondary);
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .articles-grid {
    grid-template-columns: 1fr;
  }
}
</style> 