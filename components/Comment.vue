<template>
  <v-list-item-content>
    <v-col cols="6">
      <span v-if="!isEdit">
        {{ comment.Content }}
        <v-icon @click="edit">mdi-square-edit-outline</v-icon>
        <v-icon @click="dialog = true">mdi-trash-can-outline</v-icon>
      </span>
      <span v-else>
        <v-text-field
          autofocus
          v-model="editContent"
          append-icon="mdi-check-outline"
          @click:append="commit"
          @keydown.enter="commit"
          @blur="isEdit=false"
        >
        </v-text-field>
      </span>
    </v-col>
    <v-dialog
      v-model="dialog"
      width="500"
    >
      <v-card>
        <v-card-title
          class="headline grey lighten-2"
          primary-title
        >
          投稿を削除しますか？
        </v-card-title>
        <v-card-text class="mt5">
          投稿：　{{ comment.Content }}
        </v-card-text>
        <v-card-text>
          削除した投稿は元に戻せません。本当に消しますか？
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="error"
            dark
            @click="remove"
          >
            削除
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
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
      editContent: "",
      dialog: false
    };
  },
  methods: {
    async updateComment(comment) {
      const url = `/comment/${comment.Id}`;
      comment = await this.$axios.$post(url, `content=${comment.Content}`);
    },
    async removeComment(comment) {
      const url = `/comment/${comment.Id}`;
      comment = await this.$axios.$delete(url);
    },
    edit() {
      if (this.editContent === "") {
        this.editContent = this.comment.Content;
      }
      this.isEdit = true;
    },
    remove() {
      this.removeComment(this.comment)
      this.dialog = false;
      this.$destroy();
      this.$el.parentNode.remove()
    },
    commit() {
      if (event.keyCode !== undefined && event.keyCode !== 13) return;
      if (this.editContent === "") return;
      this.comment.Content = this.editContent;
      this.updateComment(this.comment);
      this.isEdit = false;
    }
  }
};
</script>
