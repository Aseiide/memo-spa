<template>
  <div>
    <div class="text-end">
      <button v-if="!addFlg" @click="registerMemo" type="button" class="btn btn-warning btn-lg">＋</button>
    </div>

    <div v-if="addFlg" class="d-flex flex-row align-items-center">
      <textarea v-model="newMemo" type="text" class="form-control me-3" id="exampleFormControlInput1" placeholder="Add new memo"></textarea>
      <button @click="addMemo" type="button" class="btn btn-primary">Add</button>
    </div>
    <hr class="my-4">
  </div>
</template>

<script>
export default {
  data() {
    return {
      addFlg: false,
    }
  },
  methods: {
    registerMemo() {
      this.addFlg = !this.addFlg
    },
    addMemo() {
      this.$emit('add', this.newMemo)
      this.addFlg = false
      this.newMemo = '新規メモ'
    }
  }
}
</script>

<style scoped>
.text-end {
  margin: 20px;
}
</style>
