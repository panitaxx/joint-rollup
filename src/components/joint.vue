<template>
  <div ref="mydiv" />
</template>
<script>
import { dia, shapes } from "jointjs";
import { ref, onMounted } from "vue";



export default {
  setup() {
    const mydiv = ref(null);

    onMounted(() => {


        const graph = new dia.Graph({}, { cellNamespace: shapes });

        const paper = new dia.Paper({
            el: mydiv.value,
            model: graph,
            width: 600,
            height: 100,
            gridSize: 1,
            cellViewNamespace: shapes
        });

        const rect = new shapes.standard.Rectangle();
        rect.position(100, 30);
        rect.resize(100, 40);
        rect.attr({
            body: {
                fill: 'blue'
            },
            label: {
                text: 'Hello',
                fill: 'white'
            }
        });
        rect.addTo(graph);

        const rect2 = rect.clone();
        rect2.translate(300, 0);
        rect2.attr('label/text', 'World!');
        rect2.addTo(graph);

        const link = new shapes.standard.Link();
        link.source(rect);
        link.target(rect2);
        link.addTo(graph);

    });
    return {
       mydiv
    };
  },
};
</script>