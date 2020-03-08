<template>
  <v-list-item-content>
    <v-col cols="6">
      <span v-if="!isEdit">
        {{ comment.Content }}
        <v-icon @click="edit">mdi-square-edit-outline</v-icon>
      </span>
      <span v-else>
        <v-text-field
          v-model="editContent"
          append-icon="mdi-close-circle"
          append-outer-icon="mdi-check-outline"
          @click:append="isEdit=false"
          @click:append-outer="commit()"
        >
        </v-text-field>
      </span>
    </v-col>
  </v-list-item-content>
</template>

<script>
export default {
  props: {
    comment: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      isEdit: false,
      editContent: ""
    };
  },
  methods: {
    async updateComment(comment) {
      const url = `/comment/${comment.Id}`;
      comment = await this.$axios.$post(url, `content=${comment.Content}`);
    },
    edit() {
      if (this.editContent === "") {
        this.editContent = this.comment.Content;
      }
      this.isEdit = true;
    },
    commit() {
      if (this.editContent === "") return
      this.comment.Content = this.editContent
      this.updateComment(this.comment)
      this.isEdit = false;
    }
  }
};
</script>
