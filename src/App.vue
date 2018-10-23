<template>
  <condition-relation
    :conditions="conditions"
    :options="{ keyOptions, relationOptions, valueInputs }"
    style="width: 800px;"
  />
</template>

<script>
import ConditionRelation from './components/ConditionRelation/index'

export default {
  name: 'App',
  components: {
    ConditionRelation
  },
  data () {
    return {
      keyOptions: [{
        label: '性别',
        value: 'gender'
      }, {
        label: '年龄',
        value: 'age'
      }],
      relationOptions: {
        gender: [{
          label: '是',
          value: '='
        }, {
          label: '不是',
          value: '!='
        }],
        age: [{
          label: '等于',
          value: '='
        }, {
          label: '大于',
          value: '>'
        }, {
          label: '小于',
          value: '<'
        }]
      },
      valueInputs: {
        gender: {
          type: 1,
          options: [{
            label: '男',
            value: '0'
          }, {
            label: '女',
            value: '1'
          }]
        },
        age: {
          type: 3
        }
      },

      conditions: {
        group: [{
          group: [{
            describe: '',
            relation: '',
            value: ''
          }],
          relation: 'and'
        }],
        relation: 'and'
      }
    }
  }
}
</script>
