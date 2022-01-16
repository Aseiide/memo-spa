<template>
  <div class=form>
    <div class="d-flex flex-row align-items-center">
      <textarea v-model="editingMemo.content" type="text" class="form-control me-3" id="exampleFormControlInput1" placeholder="New change..."></textarea>
      <button type="button" class="btn btn-success ms-1" @click="editMemo">Update</button>
      <button type="button" class="btn btn-danger ms-1" @click="removeMemo">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      editingMemo: this.memo,
      editingId: this.id
    }
  },
  
  props: ['id', 'memo'],
  
  methods: {
    editMemo() {
      this.$emit('editMemo', this.editingId, this.editingMemo)
      this.undo()
    },
    removeMemo() {
      if (confirm('このメモを削除しますか？')) {
        this.$emit('removeMemo', this.editingId)
        this.undo()
      }
    },
    undo() {
      this.editingId = null
      this.editingMemo = null
    }
  },
}
</script>

<style scoped>
.form {
  margin-top: 20px;
}
</style>
