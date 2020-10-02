<template>
  <div>hello vue3</div>
  <h1 :style="{color: color}">x: {{position.x}}, y: {{position.y}}</h1>
  <h1>{{time}}</h1>
</template>

<script>
import { computed, reactive, ref, unref, watch, watchEffect } from "vue";
export default {
  name: "App",
  setup() {
    let position = reactive({});

    window.addEventListener("mousemove", (e) => {
      // console.log(e.pageX, e.pageY);
      position.x = e.pageX;
      position.y = e.pageY;
    });

    const color = computed(() => {
      const hex = (num) => (num % 255).toString(16);
      return `#${hex(position.x)}${hex(position.y)}00`;
    });

    const time = ref(0);
    setInterval(() => {
      time.value = Date.now();
    }, 800);

    watch(time, (val, prev) => {
      console.log("watch", val, prev);
    });

    watchEffect(() => {
      console.log('watch effec time', unref(time));
    })

    return { position, color, time };
  },
};
</script>
