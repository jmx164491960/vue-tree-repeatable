<template>
  <section>
    <el-tree
      :data="data"
      show-checkbox
      node-key="id"
    >
    </el-tree>
  </section>
</template>

<script>
import ElTree from './tree/tree';
export default {
  name: 'HelloWorld',
  components: {
    ElTree
  },
  data () {
    return {
      data: [
        {
          id: 'p1',
          label: 'parent1',
          children: [
            {
              id: 'c1',
              label: 'child2'
            }
          ]
        },
        {
          id: 'p2',
          label: 'parent2',
          children: [
            {
              id: 'c2',
              label: 'child2'
            }
          ]
        }
      ]
    }
  }
}
</script>