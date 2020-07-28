<template>
    <div>
        <el-tree
            :data="data"
            node-key="id"
            default-expand-all
            @node-drag-start="handleDragStart"
            @node-drag-enter="handleDragEnter"
            @node-drag-leave="handleDragLeave"
            @node-drag-over="handleDragOver"
            @node-drag-end="handleDragEnd"
            @node-drop="handleDrop"
            :expand-on-click-node='false'
            draggable
            :allow-drop="allowDrop"
            :allow-drag="allowDrag">
        <div class="custom-tree-node" slot-scope="{ node, data }">
            <span> <i class="el-icon-document" v-if="data.level === 2"></i> {{ node.label }}</span>
            <span>
                <el-button type="text" size="mini" v-if="data.level === 1">新建</el-button>
                <el-button type="text" size="mini" @click.native="() => remove(node, data)">
                    Delete
                </el-button>
            </span>
      </div>
        </el-tree>
    </div>
</template>

<script>
export default {
  data () {
    return {
      data: [{
        id: 1,
        label: '一级 1',
        level: 1,
        pid: 0,
        children: [{
          id: 4,
          label: '二级 1-1',
          level: 2,
          pid: 1
        }, {
          id: 5,
          label: '二级 1-2',
          level: 2,
          pid: 1
        }]
      }, {
        id: 2,
        label: '一级 2',
        level: 1,
        pid: 0,
        children: [{
          id: 5,
          label: '二级 2-1',
          level: 2,
          pid: 2
        }, {
          id: 6,
          label: '二级 2-2',
          level: 2,
          pid: 2
        }]
      }, {
        id: 3,
        label: '一级 3',
        level: 1,
        children: [{
          id: 7,
          label: '二级 3-1',
          level: 2
        }, {
          id: 8,
          label: '二级 3-2',
          level: 2
        },
        {
          id: 9,
          label: '二级 3-3',
          level: 2
        }
        ]
      }],
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    }
  },
  methods: {
    remove (node, data) {
      console.log('remove', node)
    },
    handleDragStart (node, ev) {
      console.log('drag start', node)
    },
    handleDragEnter (draggingNode, dropNode, ev) {
      console.log('tree drag enter: ', dropNode.label)
    },
    handleDragLeave (draggingNode, dropNode, ev) {
      console.log('tree drag leave: ', dropNode.label)
    },
    handleDragOver (draggingNode, dropNode, ev) {
      console.log('tree drag over: ', dropNode.label)
    },
    handleDragEnd (draggingNode, dropNode, dropType, ev) {
      console.log('tree drag end: ', dropNode && dropNode.label, dropType)
    },
    handleDrop (draggingNode, dropNode, dropType, ev) {
      console.log('tree drop: ', draggingNode, dropNode.label, dropType)
    },
    allowDrop (draggingNode, dropNode, type) {
    //   console.log('allowDrop-draggingNode', draggingNode)
      console.log('allowDrop-dropNode', draggingNode.data.pid)
      //   console.log('allowDrop-type', type)
      if (draggingNode.level === 1) {
        return false
      }
      if (draggingNode.level !== dropNode.level) {
        return false
      }
      if (draggingNode.data.pid !== dropNode.data.pid) {
        return false
      }
      if (type !== 'inner') {
        return true
      } else {
        return false
      }
    },
    allowDrag (draggingNode) {
      console.log('allowDrag', draggingNode)
      console.log('allowDrag-index', draggingNode.data.label.indexOf('三级 3-2-2') === -1)
      //   return draggingNode.data.label.indexOf('三级 3-2-2') === -1
      return true
    }
  }
}
</script>
<style >
</style>
