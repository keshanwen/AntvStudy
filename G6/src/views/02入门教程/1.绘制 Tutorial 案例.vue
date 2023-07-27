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

/*
常用配置项

fitView  是否将图适配到画布大小，可以防止超出画布或留白太多。

fitViewPadding 画布上的四周留白宽度。

animate 是否启用图的动画。

modes 图上行为模式的集合。由于比较复杂，按需参见：G6 中的 Mode 教程。

defaultNode 节点默认的属性，包括节点的一般属性和样式属性.

defaultEdge 边的默认属性，包括边的一般属性和样式属性（style）

nodeStateStyles 节点在除默认状态外，其他状态下的样式属性（style）。例如鼠标放置（hover）， 选中（select） 等状态

edgeStateStyles 边在除默认状态外，其他状态下的样式属性（style）。例如鼠标放置(hover), 选中（select）等状态


*/

const inti = async () => {
  const graph = new G6.Graph({
    container: mountNodeRef.value, // String | HTMLElement，必须，在 Step 1 中创建的容器 id 或容器本身
    width: 800, // Number，必须，图的宽度
    height: 500, // Number，必须，图的高度
    fitView: true,
    fitViewPadding: [20,40,50,20]
  });

   const response = await fetch(
      'https://gw.alipayobjects.com/os/basement_prod/6cae02ab-4c29-44b2-b1fd-4005688febcb.json',
    );
  const remoteData = await response.json();
  console.log(remoteData)

  graph.data(remoteData); // 加载远程数据
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
