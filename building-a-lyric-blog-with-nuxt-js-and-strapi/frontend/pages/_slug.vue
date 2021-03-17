<template>
  <div class="home">
    <h1 class="headline center">
      {{ article.title }}
    </h1>
    <p class="center">
      {{ article.description }}
    </p>
    <div class="sections center">
      <div class="group center">
        <p>{{ article.body }}</p>
      </div>

      <nuxt-link to="/" class="back">
        back
      </nuxt-link>
    </div>
    <div class="sections">
      <div class="group">
        <div v-for="article in articles" :key="article.id" class="section">
          <div class="entry">
            <NuxtLink :to="{path: article.slug, query: { id: article.id }}">
              <h3>
                {{ article.title }}
                <span class="subtitle"> {{ article.date }}</span>
              </h3>
            </NuxtLink>
          </div>
          <p>{{ article.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { singleArticleQuery } from '../graphql/queries'

export default {
  data () {
    return {
      article: []
    }
  },
  apollo: {
    article: {
      prefetch: true,
      query: singleArticleQuery,
      variables () {
        return {
          id: this.$route.query.id
        }
      }
    }
  }
}
</script>

<style>

.center {
  text-align: center;
}

.headline {
  text-transform: uppercase;
  margin: 4rem auto;
  font-size: 4rem;
}

.back {
  color: #42b883;
  text-decoration: underline;
}
.img {
  display: block;
  margin: 0 auto;
  width: 150px;
}

.h2 {
  color: #35495e;
  text-transform: capitalize;
}

.h3 {
  color: #42b883;
  margin-bottom: 0;
  cursor: pointer;
}

.h3 > subtitle {
  color: grey;
  font-site: 0.98rem;
  float: right;
  font-weight: normal;
}

.h3:hover {
  text-decoration: underline;
}

p {
  margin-top: 0.4rem;
}

.sections {
  max-width: 40vw;
  margin: 0 auto;
  margin-top: 4rem;
}

.section {
  margin-bottom: 3rem;
}

.group {
  margin-bottom: 4rem;
}
</style>
