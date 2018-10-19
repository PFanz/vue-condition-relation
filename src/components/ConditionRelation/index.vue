<template>
  <!-- 一级条件 -->
  <div style="display: flex;">
    <!-- 条件关系 -->
    <relation-side
      :relation="conditions.relation"
      @change="switchRelation"
    />
    <!-- /条件关系 -->

    <!-- 二级条件 -->
    <div style="flex-grow: 1;">
      <div
        v-for="(group, i) in conditions.group"
        :key="'group-' + i"
        class="conditions-group"
      >
        <relation-side
          :relation="group.relation"
          @change="relation => switchSubRelation(i, relation)"
        />
        <div style="flex-grow: 1;">
          <condition-item
            v-for="(condition, j) in group.group"
            :key="'condition' + j"
            :describe="condition.describe"
            :relation="condition.relation"
            :value="condition.value"
            :options="options"
            class="condition-item"
            @change="({key, value}) => changeItem(i, j, key, value)"
            @deleteItem="deleteItem(i, j)"
          />
          <div class="condition-item">
            <el-button @click="addSubCondition(i)">添加条件</el-button>
          </div>
        </div>
      </div>
      <div class="conditio-item">
        <el-button @click="addCondition">添加条件</el-button>
      </div>
    </div>
    <!-- /二级条件 -->
  </div>
  <!-- /一级条件 -->
</template>

<script>
import 'element-ui/lib/theme-chalk/index.css'

import RelationSide from './RelationSide'
import ConditionItem from './ConditionItem'
import { Button } from 'element-ui'

export default {
  components: {
    ConditionItem,
    RelationSide,
    [Button.name]: Button
  },
  props: {
    options: {
      type: Object,
      required: true
    },
    conditions: {
      type: Object,
      default: () => ({
        group: [{
          group: [{
            describe: '',
            relation: '',
            value: ''
          }],
          relation: 'and'
        }],
        relation: 'and'
      })
    }
  },
  data () {
    return {
    }
  },
  methods: {
    switchRelation (relation) {
      this.conditions.relation = relation
    },
    switchSubRelation (index, relation) {
      this.conditions.group[index].relation = relation
    },
    addCondition () {
      this.conditions.group.push({
        group: [{
          describe: '',
          relation: '',
          value: ''
        }],
        relation: 'and'
      })
    },
    addSubCondition (index) {
      this.conditions.group[index].group.push({
        describe: '',
        relation: '',
        value: ''
      })
    },
    changeItem (i, j, key, value) {
      this.conditions.group[i].group[j][key] = value
    },
    deleteItem (i, j) {
      this.conditions.group[i].group.splice(j, 1)
      this.checkClearGroup(i)
    },
    checkClearGroup (i) {
      if (this.conditions.group[i].group.length === 0) {
        this.conditions.group.splice(i, 1)
      }
    }
  }
}
</script>

<style lang="css" scoped>
.conditions-group {
  display: flex;
  margin: 10px 0;
}

.condition-item {
  margin: 10px 0;
}
</style>
