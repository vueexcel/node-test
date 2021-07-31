<template>
  <div>
    <h1 class="heading">Nested Nodes</h1>
    <Tree
      :value="treeData"
      :eachDraggable="eachDraggable"
      :ondragend="ondragend"
    >
      <span slot-scope="{ node, path }">
        <div class="node-wrapper">
          {{ node.text }}-<i>{{ path.join("-") }}</i>
        </div>
      </span>
    </Tree>
  </div>
</template>
<script>
import "he-tree-vue/dist/he-tree-vue.css";
import { Tree, Draggable } from "he-tree-vue";

export default {
  components: { Tree: Tree.mixPlugins([Draggable]) },
  data() {
    return {
      treeData: [
        {
          text: "node",
          children: [
            {
              text: "node",
              children: [{ text: "node" }, { text: "node" }],
            },
            {
              text: "node",
              children: [{ text: "node" }, { text: "node" }],
            },
            { text: "node" },
            { text: "node" },
          ],
        },
      ],
    };
  },
  methods: {
    eachDraggable(path, tree) {
      if (path.length === 1 && tree.rootNode.children.length === 1) {
        return false;
      } else {
        return true;
      }
    },
    ondragend(tree , store) {
      const parent = tree.getNodeParentByPath(store.targetPath)
      if(parent.children && parent.children.length > 1){
        return false
      } else {
         return true
      }
    }
  },
};
</script>

<style >
.he-tree {
  width: 300px;
  cursor: pointer;
}
.he-tree .tree-node {
  text-align: center;
  width: 150px;
}
.tree-branch {
  display: flex;
}
.draggable-placeholder {
}
.draggable-placeholder-inner {
  border: 1px dashed #0088f8;
  box-sizing: border-box;
  background: rgba(0, 136, 249, 0.09);
  color: #0088f9;
  text-align: center;
  padding: 0;
  display: flex;
  align-items: center;
}

.heading {
  text-align: center;
}

.node-wrapper {
  /* border: 1px solid #ccc; */
  padding: 20px;
}

.tree-node-back {
  padding-left: 40px !important;
  display: flex;
  align-items: center;
}
.tree-node {
  position: relative;
   cursor: pointer;
}

.tree-children.tree-root:before {
  width: 0px;
}
.tree-root > .tree-branch > .tree-node-back > .tree-node:before {
  width: 0px;
}
.tree-node:before {
  content: "";
  position: absolute;
  top: 53%;
  left: -20px;
  transform: translateY(-50%);
  height: 2px;
  width: 20px;
  background-color: #ccc;
}
.tree-node:after {
  content: "";
  position: absolute;
  top: 53%;
  right: -22px;
  transform: translateY(-50%);
  height: 2px;
  width: 22px;
  background-color: #ccc;
}

.tree-children {
  position: relative;
}
.tree-children:before {
  content: "";
  position: absolute;
  top: 50%;
  left: 20px;
  transform: translateY(-50%);
  height: 96%;
  width: 2px;
  background-color: #ccc;
}
</style>