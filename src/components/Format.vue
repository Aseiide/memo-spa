<template>
  <div>
    <Add @add="addMemo"/>
    <List :memos="this.memos" @transition="transitionToEdit"/>

    <Form v-if="editingId !== null"
    :id="editingId"
    :memo="memos[this.editingId]"
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
      editingId: null,
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
    transitionToEdit(index) {
      this.editingId = index
    },
    editMemo(index, memo) {
      this.memos.splice(index, 1, memo)
      this.saveMemo()
      this.undo()
    },
    removeMemo(index) {
      this.memos.splice(index, 1)
      this.saveMemo()
      this.undo()
    },
    saveMemo() {
      localStorage.setItem('memos', JSON.stringify(this.memos))
    },
    undo() {
      this.editingId = null
    }
  }
}
</script>
