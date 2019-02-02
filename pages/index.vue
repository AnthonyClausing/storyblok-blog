<template>
  <section id="posts">
    <PostPreview
      v-for="post in posts"
      :id="post.id"
      :key="post.id"
      :title="post.title"
      :excerpt="post.previewText"
      :thumbnail-image="post.thumbnailUrl"
    />
  </section>
</template>

<script>
import PostPreview from '@/components/Blog/PostPreview'

export default {
  components: {
    PostPreview
  },
  data() {
    return {
      posts: [
        {
          title: 'A new beginning',
          previewText: 'This will be awesome, don\'t miss it!',
          thumbnailUrl: 'https://cdn.pixabay.com/photo/2014/05/02/21/49/home-office-336373_960_720.jpg',
          id: 'a-new-beginning'
        },
        {
          title: 'A second beginning',
          previewText: 'This will be awesome, don\'t miss it!',
          thumbnailUrl: 'https://cdn.pixabay.com/photo/2014/05/02/21/49/home-office-336373_960_720.jpg',
          id: 'a-second-beginning'
        }
      ]
    }
  }
}
</script>

<style scoped>
  #posts {
    padding-top: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  @media (min-width: 35rem) {
    #posts {
      flex-direction: row;
    }
  }
</style>
