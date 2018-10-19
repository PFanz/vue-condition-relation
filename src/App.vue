<template>
  <condition-relation
    :conditions="conditions"
    :options="{ keyOptions, relationOptions, valueInputs }"
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
      keyOptions: [],
      relationOptions: {},
      valueInputs: {},

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
