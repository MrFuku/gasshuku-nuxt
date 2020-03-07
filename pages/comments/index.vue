<template>
  <section class="container">
    <h1>Tweet App</h1>
    <p><input
        type="text"
        name="content"
      /></p>
    <div>
      <button>save</button>
    </div>
    <ul>
      <li
        v-for="comment in comments"
        :key="comment.id"
      >
        <p>
          <span>{{ comment.Content }} user by: {{ comment.UserId }}</span>
        </p>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  data() {
    return {
      comments: []
    };
  },
  methods: {
    async getComments() {
      const url = "/comment";
      const response = await this.$axios.$get(url);
      this.comments = response;
    }
  },
  mounted: function() {
    this.getComments();
  }
};
</script>
