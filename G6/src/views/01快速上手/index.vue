<template>
  <main>
    <div ref="mountNodeRef" class="mountNode"></div>
  </main>
</template>

<script setup>
import { ref,onMounted } from 'vue';
import G6 from '@antv/g6';


let mountNodeRef = ref()

/*
  1,创建关系图的 HTML 容器；
  2,数据准备；
  3,创建关系图；
  4,配置数据源，渲染。
*/

const data = {
  // 点集
  nodes: [
    {
      id: 'node1', // String，该节点存在则必须，节点的唯一标识
      x: 100, // Number，可选，节点位置的 x 值
      y: 200, // Number，可选，节点位置的 y 值
    },
    {
      id: 'node2', // String，该节点存在则必须，节点的唯一标识
      x: 300, // Number，可选，节点位置的 x 值
      y: 200, // Number，可选，节点位置的 y 值
    },
  ],
  // 边集
  edges: [
    {
      source: 'node1', // String，必须，起始点 id
      target: 'node2', // String，必须，目标点 id
    },
  ],
};



const inti = () => {
  const graph = new G6.Graph({
    container: mountNodeRef.value, // String | HTMLElement，必须，在 Step 1 中创建的容器 id 或容器本身
    width: 800, // Number，必须，图的宽度
    height: 500, // Number，必须，图的高度
  });

  graph.data(data); // 读取 Step 2 中的数据源到图上
  graph.render(); // 渲染图

}


onMounted(() => {
  inti()
})


</script>


<style>
.mountNode {
  /* height: 600px;
  border: 1px solid red; */
}

</style>
