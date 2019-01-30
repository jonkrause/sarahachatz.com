<template>
  <div class="inputContainer">
    <input v-model="newTitle">
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      newTitle: 'sarahachatzkkjj.com',
      newText: '',
    }
  },
  // props: ['newTitle', 'newText'],
  computed: {
    editText() {
      this.newText = this.newTitle
    }
  }

}
</script>

<style>

</style>
