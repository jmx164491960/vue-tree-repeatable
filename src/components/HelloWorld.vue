<template>
  <section>
    <el-tree
      ref="tree"
      :data="data"
      :usual-keys="usualKeys"
      show-checkbox
      node-key="id"
      @check="checkHandler"
    >
    </el-tree>

    <button @click="addUsual">添加常用</button>
  </section>
</template>

<script>
import ElTree from './tree/tree';
const USUAL_KEY = 'USUAL';
export default {
  name: 'HelloWorld',
  components: {
    ElTree
  },
  methods: {
    usualTreeSetChecked(key, val) {
      this.$refs['tree'].usualTreeStore.setChecked(key, val);
    },
    checkHandler(node, obj) {
      console.log('checkHandler:', node, obj);
      this.checkedNodes = obj.checkedNodes;
      this.checkedKeys = obj.checkedKeys;

      // 为update把常用选择里的parent
      if (node.id === USUAL_KEY) {
        this.usualKeys.forEach(key => {
          this.$refs['tree'].setChecked(key, obj.checked);
        })
      }

      if (this.checkedKeys.length > 0 && this.usualKeys.length > 0) {
        // 如果常用选择里的选项都选择了
        if (this.usualKeys.every(id => {
          return this.checkedKeys.includes(id);
        })) {
          this.$refs['tree'].usualTreeStore.setChecked(USUAL_KEY, true);
        } else {
          this.$refs['tree'].usualTreeStore.setChecked(USUAL_KEY, false);
        }
      } else {
        this.$refs['tree'].usualTreeStore.setChecked(USUAL_KEY, false);
      }
    },
    addUsual() {
      const checkedChildrenId = this.checkedNodes.filter(item => !item.children).map(item => item.id);
      this.usualKeys = [...new Set([...this.usualKeys, ...checkedChildrenId])];
    }
  },
  data () {
    return {
      usualKeys: ['c1-1', 'c1-2', 'c1-3', 'c1-4', 'c1-5'],
      checkedNodes: [],
      checkedKeys: [],
      data: [
        {
          id: 'p1',
          label: 'parent1',
          children: [
            {
              id: 'c1-1',
              label: 'c1-1'
            },
            {
              id: 'c1-2',
              label: 'c1-2'
            },
            {
              id: 'c1-3',
              label: 'c1-3'
            },
            {
              id: 'c1-4',
              label: 'c1-4'
            },
            {
              id: 'c1-5',
              label: 'c1-5'
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