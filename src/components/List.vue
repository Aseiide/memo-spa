<template>
  <div>
    <ul class="list-group">
      <li v-for="(memo, i) in memos" :key="i" class="list-group-item">
        <a class="memo-list" @click="transitionToEdit(i, memo)">
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
    transitionToEdit (id, memo) {
      this.$emit('transition', id, memo)
    },
    splitOneLine (memo) {
      return memo.split('\n')[0]
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
