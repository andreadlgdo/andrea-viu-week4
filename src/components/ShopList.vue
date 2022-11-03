<template>
  <!--Que es el list, realmente esta en data //¿Como hacemos?-->
  <div>
    {{ text }}
    <!--Otra manera de hacerlo. Derntro de methods, va this
    <button @click="$emit('delete')">Delete</button>-->
    <button class="item-del" @click="deleteEvent">Delete</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  //Muchas maneras de escribir las props
  props: ["text"],
  methods: {
    deleteEvent(): void {
      this.$emit("delete");
    },
  },
});
</script>

<style scoped>
.item-del {
  background: #de1919 !important;
}
</style>
