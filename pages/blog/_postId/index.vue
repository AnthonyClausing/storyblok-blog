<template>
  <div id="post" v-editable="blok">
    <div class="post-thumbnail" :style="{backgroundImage: 'url(' + image + ')'}" />
    <section class="post-content">
      <h1>{{ title }}</h1>
      <p>{{ content }}</p>
    </section>
  </div>
</template>

<script>
export default {
  asyncData(context) {
    return context.app.$storyapi.get('cdn/stories/blog/' + context.params.postId, {
      version: process.env.NODE_ENV === 'production' ? 'published' : 'draft'
    })
      .then((res) => {
        return {
          blok: res.data.story.content,
          image: res.data.story.content.thumbnail,
          title: res.data.story.content.title,
          content: res.data.story.content.content
        }
      })
  },
  mounted() {
    this.$storybridge.on(['input', 'published', 'change'], (event) => {
      if (event.action === 'input') {
        // Inject content on the input event
        if (event.story.id === this.story.id) {
          this.story.content = event.story.content
        }
      } else if (!event.slugChanged) {
        // Reload the page on save events
        window.location.reload()
      }
      if (event.action === 'change') {
        location.reload(true)
      }
    })
  }
}
</script>

<style>
 .post-thumbnail {
   width: 100%;
   height: 300px;
   background-size: cover;
   background-position: center;
 }

 .post-content {
   width: 80%;
   max-width: 500px;
   margin: auto;
 }

 .post-content p {
   white-space: pre-line;
 }
</style>
