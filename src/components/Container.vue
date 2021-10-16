<template>
  <div >
    <Add @add="add"/>
    <List :memos="this.memos" @edit="edit"/>

    <Form v-if="editFlg"
          :id="editingId"
          :memo="editingMemo"
          @update="update"
          @destroy="destroy"/>
  </div>
</template>

<script>
import List from './List.vue'
import Add from './Add.vue'
import Form from './Form'

export default {
  data() {
    return {
      memos: [],
      editFlg: false,
      editingId: null,
      editngMemo: null
    }
  },
  components: {
    List,
    Form,
    Add
  },
  mounted() {
    this.memos = JSON.parse(localStorage.getItem('memos'))
  },
  methods: {
    add(memo) {
      if (!memo) return
      this.memos.push(memo)
      this.save()
    },
    edit(...data) {
      const [id, memo] = data
      this.editFlg = true
      this.editingId = id
      this.editingMemo = memo
    },
    update(...data) {
      const [id, memo] = data
      this.memos.splice(id, 1, memo)
      this.save()
      this.reset()
    },
    destroy(id) {
      this.memos.splice(id, 1)
      this.save()
      this.reset()
    },
    save() {
      localStorage.setItem('memos', JSON.stringify(this.memos))
    },
    reset() {
      this.editFlg = false
      this.editingId = null
      this.editingMemo = null
    }
  }
}
</script>
