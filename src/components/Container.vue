<template>
  <div>
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
      editingMemo: null
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
      this.$_container_save()
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
      this.$_container_save()
      this.$_container_reset()
    },
    destroy(id) {
      this.memos.splice(id, 1)
      this.$_container_save()
      this.$_container_reset()
    },
    $_container_save() {
      localStorage.setItem('memos', JSON.stringify(this.memos))
    },
    $_container_reset() {
      this.editFlg = false
      this.editingId = null
      this.editingMemo = null
    }
  }
}
</script>
