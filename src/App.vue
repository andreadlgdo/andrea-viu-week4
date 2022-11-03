<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <h1>SHOPPING LIST</h1>
  <!--Esta clase se va a aplicar cuando la lista tenga dos o mas elementos-->
  <div :class="[{ warning: isWarning }, 'shop-wrap']">
    <!-- (A) ADD NEW ITEM -->
    <form id="shop-form">
      <input
        type="text"
        id="shop-item"
        class="item-name"
        placeholder="Item Name"
        required
      />
      <input type="submit" id="shop-add" value="Add" @click="añadirTarea()" />
    </form>

    <!-- (B) SHOPPING LIST -->
    <div id="shop-list">
      <!--Vamos a estraerlo a un componente-->
      <!--    <div v-for="(item, index) in list" :key="item">
        {{ item }}
        <button @click="eliminarElemento(index)">Delete</button>
      </div>-->
      <!--tambien se puede escribir shop-list-->
      <ShopList
        v-for="(item, index) in list"
        :key="item"
        @delete="eliminarElemento(index)"
        :text="item"
      ></ShopList>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ShopList from "@/components/ShopList.vue";

export default defineComponent({
  name: "App",
  components: { ShopList },
  data: function () {
    //Todo lo que este aqui, estara vinculado a lo de arriba
    return {
      list: ["patata", "leche", "patatitas"],
    };
  },
  computed: {
    //No suelen tener parametros
    //Cogen cosas de date
    isWarning: function (): boolean {
      return this.list.length > 2;
    },
  },
  methods: {
    //A la lista le añadimos un elemento, con la funcion añadir elemento
    añadirTarea: function (): void {
      //this.list.push("arroz");
      this.list = [...this.list, "arroz"];
    },
    eliminarElemento: function (tareaindex: number): void {
      this.list.filter((element, index) => index !== tareaindex);
    },
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#shop-wrap,
#shop-wrap > * {
  box-sizing: border-box;
}
#shop-wrap input {
  padding: 10px;
  border: 0;
}
#shop-wrap input[type="button"],
#shop-wrap input[type="submit"] {
  cursor: pointer;
  color: #fff;
  background: #5a75d6;
}
#shop-form,
.item-row {
  display: flex;
  align-items: center;
}
#shop-item,
.item-name {
  flex-grow: 1;
}

/* (B) WRAPPER */
.shop-wrap {
  max-width: 500px;
  padding: 15px;
  background: #f2f2f2;
  border: 2px solid #eee;
}

/* (C) SHOPPING LIST */
.item-row {
  margin-top: 10px;
}
.item-name {
  padding: 5px;
  background: #fff;
}
.item-name.item-got {
  background: #f5fffa;
}
.item-name.item-got:before {
  content: "\02713";
  margin-right: 5px;
  font-weight: bold;
  color: #00d036;
}

.warning {
  background: red;
}
* {
  font-family: arial, sans-serif;
}
</style>
