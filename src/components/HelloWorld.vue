<template>
  <v-container>
    <PageHeader>
      Home Page
      <template v-slot:description>
        This is the landing page of our project
      </template>
    </PageHeader>

    <v-btn @click="getPosts()" color="primary">Get posts</v-btn>
    <v-select
      :items="posts"
      v-model="selectedPost"
      @change="getPost($event)"
    ></v-select>

    {{ numberOfPosts }}
  </v-container>
</template>

<script>
import PageHeader from "@/components/PageHeader.vue";

const url = "http://localhost:8080/posts/";

export default {
  name: "HelloWorld",

  components: {
    PageHeader,
  },

  data: () => ({
    posts: [],
    post: "",
    selectedPost: "",
  }),

  methods: {
    async getPosts() {
      const response = await fetch(url + "list.txt");
      const data = await response.text();
      this.posts = data.split("\n");
      this.selectedPost = this.posts[0];
    },

    getPost(value) {
      console.log(value);
      // fetch(...)
    },
  },

  watch: {
    selectedPost(value) {
      console.log("selected post has changed " + value);
    },
    numberOfPosts() {
      // await fetch(someUrl...)
      console.log("number of posts changed");
    },
  },

  computed: {
    numberOfPosts() {
      return this.posts.length;
    },
  },
};
</script>
