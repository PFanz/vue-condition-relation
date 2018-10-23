<template>
  <div class="condition-item">
    <el-select
      :value="describe"
      placeholder="请选择条件"
      filterable
      @change="value => change('describe', value)"
    >
      <el-option
        v-for="item in options.keyOptions"
        :key="item.value"
        :label="item.label"
        :value="item.value"
      />
    </el-select>

    <el-select
      :value="relation"
      placeholder="请选择关系"
      @change="value => change('relation', value)"
    >
      <el-option
        v-for="item in relationOptions"
        :key="item.value"
        :label="item.label"
        :value="item.value"
      />
    </el-select>

    <template>
      <el-input
        v-if="valueInput.type === 0"
        type="text"
        style="width: 180px;"
        placeholder="请输入文本"
      />

      <!-- 下拉 -->
      <el-select
        v-else-if="valueInput.type === 1"
        :value="value"
        placeholder="请选择"
        filterable
        @change="value => change('value', value)"
      >
        <el-option
          v-for="item in valueInput.options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        />
      </el-select>
      <!-- /下拉 -->

      <!-- 多选下拉 -->
      <el-select
        v-if="valueInput.type === 2"
        :value="value.length ? JSON.parse(value) : []"
        placeholder="请选择"
        filterable
        multiple
        style="width: 500px;"
        @change="value => change('value', JSON.stringify(value))"
      >
        <el-option
          v-for="item in valueInput.options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        />
      </el-select>
      <!-- /多选下拉 -->

      <!-- 数值比较 -->
      <el-input
        v-else-if="valueInput.type === 3"
        :value="value"
        type="number"
        style="width: 180px;"
        placeholder="请输入数值"
        @change="value => change('value', value.toString())"
      />
      <!-- /数值比较 -->

      <!-- 日期选择 -->
      <el-date-picker
        v-else-if="valueInput.type === 4"
        :value="value"
        type="date"
        placeholder="选择日期"
        value-format="yyyy-MM-dd"
        @input="value => change('value', value)"
      />
      <!-- /日期选择 -->

      <!-- 时间段 -->
      <el-date-picker
        v-else-if="valueInput.type === 5"
        :value="value.length ? JSON.parse(value) : []"
        type="daterange"
        value-format="yyyy-MM-dd"
        @input="value => change('value', JSON.stringify(value))"
      />
      <!-- /时间段 -->

      <!-- 级联 -->
      <el-cascader
        v-else-if="valueInput.type === 6"
        :options="valueInput.options"
        :value="value.length ? JSON.parse(value) : []"
        change-on-select
        @change="value => change('value', JSON.stringify(value))"
      />
      <!-- /级联 -->

    </template>

    <el-button
      type="danger"
      icon="el-icon-delete"
      style="float: right;"
      @click="deleteItem"
    />
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Object,
      required: true
    },
    describe: {
      type: String,
      default: ''
    },
    relation: {
      type: String,
      default: ''
    },
    value: {
      type: String,
      default: ''
    }
  },
  computed: {
    relationOptions () {
      const describe = this.describe
      return describe !== '' ? this.options.relationOptions[describe] : []
    },
    valueInput () {
      const describe = this.describe
      return describe !== '' && this.options.valueInputs[describe] !== undefined ? this.options.valueInputs[describe] : {
        type: 1,
        options: []
      }
    }
  },
  methods: {
    change (key, value) {
      if (key === 'describe') {
        this.$emit('change', { key: 'relation', value: '' })
        this.$emit('change', { key: 'value', value: '' })
      }
      this.$emit('change', { key, value })
    },
    deleteItem () {
      this.$emit('deleteItem')
    }
  }
}
</script>
