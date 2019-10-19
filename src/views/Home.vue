<template>
  <div id="mountNode"></div>
</template>

<script>
import G6 from "@antv/g6";
import G6Plugins from "@antv/g6/build/plugins";
export default {
  data() {
    return {
      data: {
        nodes: [
          {
            id: "还是新增的3"
          },
          {
            id: "收集日志"
          },
          {
            id: "入 es 集群"
          },
          {
            id: "新增的"
          },
          {
            id: "入 hdfs"
          },
          {
            id: "hive 计算"
          },
          {
            id: "report"
          }
        ],
        edges: [
          {
            source: "收集日志",
            target: "入 es 集群"
          },
          {
            source: "收集日志",
            target: "入 hdfs"
          },
          {
            source: "入 hdfs",
            target: "hive 计算"
          },
          {
            source: "入 es 集群",
            target: "hive 计算"
          },
          {
            source: "hive 计算",
            target: "report"
          }
        ]
      }
    };
  },
  mounted() {
    G6.registerNode("rect", {
      getPath: function getPath(item) {
        var width = 100; // 一半宽
        var height = 40; // 一半高
        return G6.Util.getRectPath(-width / 2, -height / 2, width, height, 10);
      }
    });
    var graph = new G6.Graph({
      container: "mountNode",
      fitView: "fitView", //自适应
      height: window.innerHeight, // 画布高
      width: "500",
      plugins: [new G6.Plugins["layout.dagre"]()],
      defaultIntersectBox: "rect" // 使用矩形包围盒
    });

    graph.node({
      shape: "rect",
      label: function label(model) {
        // return model.id;
        return {
          text: model.id,
          fill: "#f00" //更改文字颜色
        };
      },

      style: {
        stroke: "#00C0A5",
        fill: "#92949F",
        fillOpacity: 0.45,
        lineWidth: 2
      }
    });
    graph.edge({
      style: {
        endArrow: true
      }
    });
    graph.read(this.data);
  }
};
</script>
