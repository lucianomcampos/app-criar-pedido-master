<template>
  <div class="main">
    <div class="container">
      <div class="title">
        <h1>Criar Pedido</h1>
      </div>
      <br />

      <br />
      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <span class="input-group-text" id="basic-addon1"
            >Selecione o Destinatário</span
          >
        </div>
        <input
          id="inputRemittee"
          type="text"
          class="form-control"
          aria-describedby="basic-addon1"
          v-model="searchRemittee"
        />
      </div>

      <div class="card" style="width: 18rem;">
        <ul
          class="list-group list-group-flush"
          v-for="remittee in selectedRemittee"
          :key="remittee.id"
        >
          <a
            @click="selectRemittee($event)"
            class="list-group-item list-group-item-action"
            >{{ remittee.name }}</a
          >
        </ul>
      </div>

      <span class="card-selected">Destinatário não selecionado</span>

      <hr />
      <br />
      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <span class="input-group-text" id="basic-addon1"
            >Selecione o Produto</span
          >
        </div>
        <input
          type="text"
          class="form-control"
          aria-describedby="basic-addon1"
          v-model="searchProduct"
        />
      </div>
      <div class="card" style="width: 18rem;">
        <ul
          class="list-group list-group-flush"
          v-for="product in selectedProduct"
          :key="product.code"
        >
          <a class="list-group-item list-group-item-action">{{
            product.title
          }}</a>
        </ul>
      </div>
      <span class="card-selected">Produto não selecionado</span>
      <hr />
      <span class="btn-css">
        <button type="button" class="btn btn-primary">Confirmar Pedido</button>
      </span>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import { remittees } from './services/httpGetRemittees';
import { products } from './services/httpGetProducts';

export default {
  name: 'App',

  setup() {
    const searchRemittee = ref('');
    const searchProduct = ref('');
    const remitteeSelected = ref('');

    const selectedRemittee = computed(() => {
      return remittees.filter((remittee) =>
        remittee.name.match(searchRemittee.value)
      );
    });
    const selectedProduct = computed(() => {
      return products.filter((product) =>
        product.title.match(searchProduct.value)
      );
    });

    function selectRemittee(event) {
      event.preventDefault();

      console.log(event);
    }

    return {
      selectedRemittee,
      searchRemittee,
      searchProduct,
      remitteeSelected,
      selectedProduct,
      selectRemittee,
    };
  },
};
</script>

<style>
.main {
  font-family: 'Arvo', serif;
  padding: 4ch;
}
.card-selected {
  font-size: 12px;
  width: 200px;
  background-color: azure;
}
.btn-css {
  display: flex;
  justify-content: flex-end;
}
</style>
