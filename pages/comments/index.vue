<template>
  <v-app>
    <section class="container">
      <h1>Tweet App</h1>
      <v-col cols="6">
        <v-text-field
          v-model="editContent"
          append-outer-icon="mdi-send"
          outlined
          label="tweetを投稿"
          type="text"
          @click:append-outer="sendComment"
        />
      </v-col>
      <v-list>
        <v-list-item
          v-for="comment in comments"
          :key="comment.id"
        >
          <Comment :comment="comment" />
        </v-list-item>
      </v-list>
    </section>
  </v-app>
</template>

<script>
import Comment from "~/components/Comment";

export default {
  components: {
    Comment
  },
  data() {
    return {
      comments: [],
      editContent: ""
    };
  },
  methods: {
    async getComments() {
      const url = "/comment";
      const response = await this.$axios.$get(url);
      this.comments = response.reverse();
    },
    async postComment(content) {
      const url = "/comment";
      const comment = await this.$axios.$post(url, `content=${content}`);
      this.comments.unshift(comment);
    },
    sendComment() {
      if (this.editContent === "") return;
      this.postComment(this.editContent);
      this.editContent = "";
    }
  },
  mounted: function() {
    this.getComments();
  }
};
</script>
