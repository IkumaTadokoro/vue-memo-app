<template>
  <div>
    <div
      class="d-flex flex-end memo-area"
      v-if="!addFlg"
    >
      <button
        @click="register"
        type="button"
      >
        ＋
      </button>
    </div>
    <div
      v-else
      class="d-flex memo-area"
    >
      <textarea
        v-model="newMemo"
        type="text"
        class="textarea"
      />
      <button
        @click="add"
        type="button"
        class="btn"
      >
        追加
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      addFlg: false,
      newMemo: '新規メモ'
    }
  },
  emits: ['add'],
  methods: {
    register() {
      this.addFlg = !this.addFlg
    },
    add() {
      this.$emit('add', this.newMemo)
      this.addFlg = false
      this.newMemo = '新規メモ'
    }
  }
}
</script>

<style scoped>
.d-flex {
  display: flex;
}

.flex-end {
  justify-content: flex-end;
}

.memo-area {
  padding: 1rem;
}

.textarea {
  flex: 1 1 auto;
  margin-right: 2rem;
}

</style>
