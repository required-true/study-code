<template>
  <div v-if="data.length">
    <ul class="list">
      <li v-for="(item, index) in data" :key="item.keyword" @click="onClickList(item.keyword)">
        <span v-if="keywordType" class="number">{{ index + 1 }}</span>
        {{ item.keyword }}
        <span v-if="historyType" class="date">{{ item.date }}</span>
        <button v-if="historyType" class="btn-remove" @click.stop="onRemoveList(item.keyword)"></button>
      </li>
    </ul>
  </div>
  <div v-else>
    추천 검색어가 없습니다.
  </div>
</template>

<script>
export default {
  props: ['data', 'type'],
  computed: {
    keywordType() {
      return this.type === 'keywords'
    },
    historyType() {
      return this.type === 'history'
    }
  },
  methods: {
    onClickList(keyword) {
      this.$emit('@click', keyword)
    },
    onRemoveList(keyword) {
      this.$emit('@remove', keyword)
    },
  }
}
</script>