<template>
  <div class="condition-relation">
    <el-button
      class="condition-btn"
      size="mini"
      type="info"
      @click="switchRelation"
    >{{ relation === 'and' ? '且' : '或' }}</el-button>
  </div>
</template>

<script>
export default {
  props: {
    relation: {
      type: String,
      required: true
    }
  },
  methods: {
    switchRelation: function () {
      this.relation === 'and' ? this.$emit('change', 'or') : this.$emit('change', 'and')
    }
  }
}
</script>

<style lang="css" scoped>
.condition-relation {
  margin-right: 5px;
  background:linear-gradient(0deg,#d2d4d4 100%,#d2d4d4 100%);
  background-size: 3px;
  background-repeat: no-repeat;
  background-position: center;

  display: flex;
  flex-direction: column;
  justify-content: center;
}

.condition-btn {
  color: #409eff;
  padding: 7px;
}
</style>
