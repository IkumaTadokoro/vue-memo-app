<template>
  <div>
    <div class="d-flex memo-area">
      <textarea class="textarea" v-model="editingMemo" type="text"></textarea>
      <button type="button" @click="update">編集</button>
      <button type="button" @click="destroy">削除</button>
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
    update() {
      this.$emit('update', this.editingId, this.editingMemo)
      this.reset()
    },
    destroy() {
      this.$emit('destroy', this.editingId)
      this.reset()
    },
    reset() {
      this.editingId = null
      this.editingMemo = null
    }
  },
  watch: {
    id: function(newId) {
      this.editingId = newId
    },
    memo: function(newMemo) {
      this.editingMemo = newMemo
    }
  }
}
</script>

<style scoped>
.d-flex {
  display: flex;
}

.memo-area {
  padding: 1rem;
}

.textarea {
  flex: 1 1 auto;
  margin-right: 2rem;
}
</style>
