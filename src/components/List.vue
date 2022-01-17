<template>
  <div>
    <ul class="list-group">
      <li v-for="(memo, index) in memos" :key="memo.id" class="list-group-item">
        <a class="memo-list" @click="transitionToEdit(index, memo)">
          {{ splitOneLine(memo) }}
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['memos'],
  methods: {
    transitionToEdit (index, memo) {
      this.$emit('transition', index, memo)
    },
    splitOneLine (memo) {
      return memo.content.split('\n')[0]
    } 
  }
  
}
</script>

<style scoped>
.memo-list {
  cursor: pointer;
  text-decoration:none;
}
</style>
