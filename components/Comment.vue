<template>
  <v-list-item-content>{{ comment.Content }}</v-list-item-content>
</template>

<script>
export default {
  props: {
    comment: {
      type: Object,
      required: true
    }
  }
}
</script>
