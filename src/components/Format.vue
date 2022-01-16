<template>
  <div>
    <Add @add="addMemo"/>
    <List :memos="this.memos" @transition="transitionToEdit"/>

    <Form v-if="editFlg"
    :id="editingId"
    :memo="editingMemo"
    @editMemo="editMemo"
    @removeMemo="removeMemo"/>
  </div> 
</template>

<script>
import List from './List.vue'
import Form from './Form.vue'
import Add from './Add.vue'
export default {
  data() {
    return {
      memos: [],
      editFlg: false,
      editingId: null,
      editingMemo: null
    }
  },
  
  components: {
    List,
    Form,
    Add
  },
  mounted() {
    if (localStorage.getItem('memos')) {
      try {
        this.memos = JSON.parse(localStorage.getItem('memos'))
      } catch(e) {
        localStorage.removeItem('memos')
      }
    }
  },
  methods: {
    addMemo(text) {
      if (!text) {
        return
      }
      const content = {id:this.$uuid.v4(), content: text}
      this.memos.push(content)
      this.saveMemo()
    },
    transitionToEdit(id, memo) {
      this.editFlg = true
      this.editingId = id
      this.editingMemo = memo
    },
    editMemo(id, memo) {
      this.memos.splice(id, 1, memo)
      this.saveMemo()
      this.undo()
    },
    removeMemo(id) {
      this.memos.splice(id, 1)
      this.saveMemo()
      this.undo()
    },
    saveMemo() {
      localStorage.setItem('memos', JSON.stringify(this.memos))
    },
    undo() {
      this.editFlg = false
      this.editingId = null
      this.editingMemo = null
    }
  }
}
</script>
