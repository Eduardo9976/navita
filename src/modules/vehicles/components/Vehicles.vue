<template>
  <div class="vehicles">
    <h1>Veículos</h1>
    <div class="card">
      <h3>Marcas</h3>
      <div class="card-content">
        <h4>Marca</h4>
        <i class="fas fa-arrow-down"></i>
        <ul>
          <li v-for="manufacturer in manufacturers" :key="manufacturer.codigo">
            <p>{{manufacturer.nome}}</p>
            <a href="/" @click.prevent.stop="getModels(manufacturer.codigo)">Ver modelos</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="card models">
      <h3>Modelos</h3>
      <div class="card-content">
        <h4>Modelo</h4>
        <Loading v-if="loading" />
        <transition appear mode="out-in">
          <div v-if="models">
            <ul>
              <li v-for="(model, index) in models" :key="index">{{model.nome}}</li>
            </ul>
          </div>
          <p v-else class="cardText">Selecione um Fabricante para listar os seus modelos.</p>
        </transition>
      </div>
    </div>
    <span class="toTop" @click="toTop"><img src="../img/arrowUp.png" alt="Seta que leva para o todo da página"></span>
  </div>
</template>

<script>
import Loading from '../../loading/components/Loading'
export default {
  name: "Vehicles",
  data() {
    return {
      manufacturers: {},
      models: undefined,
      loading: false,
    };
  },
  components: {
    Loading
  },
  methods: {
    async getManufacturers() {
      const response = await fetch(
        "https://parallelum.com.br/fipe/api/v1/carros/marcas"
      );
      const responseJSON = await response.json();
      this.manufacturers = responseJSON;
    },
    async getModels(code) {
      this.loading = true;
      window.scrollTo({ top: 1000, behavior: "smooth" });
      const response = await fetch(
        `https://parallelum.com.br/fipe/api/v1/carros/marcas/${code}/modelos`
      );
      const responseJSON = await response.json();
      this.models = responseJSON.modelos;
      this.loading = false;
    },
    toTop() {
      window.scrollTo({ top: 0, behavior: "smooth" });
    }
  },
  created() {
    this.getManufacturers();
  },
};
</script>

