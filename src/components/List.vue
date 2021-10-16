<template>
  <div>
    <ul class="memo-list-group">
      <li class="memo-list" v-for="(memo, i) in memos" :key="i">
        <a class="memo-link" @click="edit(i, memo)">
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
    edit(id, memo) {
      this.$emit('edit', id, memo)
    },
    splitOneLine(memo) {
      return memo.split('\n')[0]
    }
  }
}
</script>

<style scoped>
.memo-list-group {
  padding: 1rem;
}

.memo-list {
  list-style: none;
  margin: 0.2rem 0 0 0;
  border-bottom: 1px solid;
}

.memo-link {
  cursor: pointer;
  text-decoration:none;
}
</style>
