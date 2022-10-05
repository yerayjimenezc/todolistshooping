<template>
  <v-container fluid class="wrapper-main" justify="center" align="center">
    <v-row justify="center" align="center">
      <v-col id="header" cols="11" sm="9" class="d-flex align-end">
        <h1 class="title">Lista de la compra</h1>
        <v-spacer />
        <v-icon v-if="$vuetify.theme.dark" @click="$vuetify.theme.dark = !$vuetify.theme.dark">mdi-white-balance-sunny
        </v-icon>
        <v-icon v-else @click="$vuetify.theme.dark = !$vuetify.theme.dark" color="white">mdi-weather-night
        </v-icon>
        <v-icon class="ps-3">mdi-account-cancel-outline
        </v-icon>
        <span v-if="user" class="ps-1 font-weight-thin">Hola, {{user}}</span>
      </v-col>
    </v-row>

    <v-row justify="center" align="center">
      <v-col cols="11" sm="9">
        <v-text-field v-model="msg" color="red" label="Productos..." @keyup.enter="addProduct" rounded solo>
        </v-text-field>
      </v-col>
    </v-row>
    <v-row justify="center" align="center">
      <v-col cols="11" sm="9">
        <v-card elevation="10" v-if="products.length === 0" class="d-flex align-center text-center">
          <v-col class="pa-1">
            <v-card-text>No hay productos en tu lista 😱.</v-card-text>
          </v-col>
        </v-card>
        <CardProduct v-for="(product, idx) in filterProducts" :product="product" :key="idx"
          @delete="callback(product.id)" @status="changeStatus(product.id)">
        </CardProduct>
        <v-card elevation="10" class="d-flex align-center text-center">
          <v-col class="pa-1">
            <v-card-text class="footext">pendientes: {{countPendientes}}</v-card-text>
          </v-col>
        </v-card>
      </v-col>
    </v-row>
    <v-row justify="center" align="center">
      <v-col cols="11" sm="9">
        <v-card elevation="10" class="d-flex align-center text-center">
          <v-col class="pa-1">
            <v-card-text :class="(filter === '') ? 'textactive' : 'textinactive'" @click="filter = ''">Todos
            </v-card-text>
          </v-col>
          <v-col class="pa-1">
            <v-card-text :class="(filter === 'pendientes') ? 'textactive' : 'textinactive'"
              @click="filter = 'pendientes'">
              Pendientes</v-card-text>
          </v-col>
          <v-col class="pa-1">
            <v-card-text :class="(filter === 'comprados') ? 'textactive' : 'textinactive'"
              @click="filter = 'comprados'">
              Comprados</v-card-text>
          </v-col>
        </v-card>
      </v-col>
    </v-row>

  </v-container>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      user: false,
      msg: '',
      filter: '',
      products: [
        {
          id: 0,
          name: 'hola',
          active: false,
        },
        {
          id: 1,
          name: 'no estoy pendiente',
          active: true,
        }
      ]
    }
  },
  computed: {
    countPendientes() {
      return this.products.filter(product => product.active === false).length
    },
    filterProducts() {
      if (this.filter === '') {
        return this.products
      }
      if (this.filter === 'pendientes') {
        return this.products.filter(product => product.active === false)
      }
      if (this.filter === 'comprados') {
        return this.products.filter(product => product.active === true)
      }
    }
  },
  methods: {
    addProduct() {
      this.products.push({ name: this.msg, active: false, id: this.products.length });
      this.msg = ''
    },
    callback(idx) {
      const index = this.products.map(product => product.id).indexOf(idx)
      this.products.splice(index, 1)
    },
    changeStatus(idx) {
      this.products[idx].active = !this.products[idx].active
    }
  }
}
</script>

<style>
.title {
  color: white;
}

.wrapper-main {
  background-image: linear-gradient(to bottom,
      rgba(8, 8, 7, 0.7),
      rgba(93, 0, 255, 0.7)), url('https://picsum.photos/1900/300/?blur=2');
  background-size: auto 250px;
  padding-top: 0;
}

.textactive {
  padding: 0;
  font-size: 12px;
  font-weight: 300;
  cursor: pointer;
  color: rgb(173, 28, 173);
}

.textinactive {
  padding: 0;
  font-size: 12px;
  font-weight: 300;
  cursor: pointer;
  color: primary;
}


#header {
  margin-top: 100px;
}
</style>