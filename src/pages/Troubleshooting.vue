<template>
  <Page>
    <template v-slot:header>
      <h1>
        Troubleshooting issues
      </h1>
      <p>
        Stuck? Get help solving a problem or the error message.
      </p>
    </template>
    <Section>
      <div
        v-for="article in articles"
        :key="article.node.title">
        <g-link :to="article.node.path">
          <Card
            class="article-list-item">
            <h4>{{ article.node.title }}</h4>
            <p>{{ article.node.excerpt | truncate(180) }}</p>
          </Card>
        </g-link>
      </div>
    </Section>
  </Page>
</template>
<page-query>
query TroubleshootingArticle {
  article: allTroubleshootingArticle {
    edges{
      node{
        title
				excerpt
        path
        timeToRead
        fileInfo{
          directory
        }
        sort
      }
    }
  }
}
</page-query>

<script>
import Vue2Filters from 'vue2-filters';

export default {
  name: 'GettingStarted',
  mixins: [Vue2Filters.mixin],
  computed: {
    articles() {
      console.log(this.$page.article.edges);
      return this.orderBy(this.$page.article.edges, 'node.sort', 1);
    }
  }
};
</script>

<style lang="scss" scoped>
.article-list-item {
  margin-bottom: 1rem;
  padding: 1.5rem 2rem;
  cursor: pointer;
  p {
    margin-bottom: 0;
  }
}
</style>
