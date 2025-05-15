<script setup>
import axios from "axios";
import {onMounted} from "vue";

const assets = {
  USD: {
    available: 0,
    frozen: 0,
  },
  BTC: {
    available: 0,
    frozen: 0,
  }
}

onMounted(() => {
  init()
})

const init = async () => {
  await get('/api/assets').then((response) => {
    this.assets = response.data;
  }).catch((error) => {
    console.log(error);
  })
}

const get = async (url) => {
  return await axios.get(url);
}
</script>

<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand" href="/">
          Exchange
        </a>
      </div>
    </nav>
    <div class="card-header">
      Balance
    </div>
    <div class="card-body">
      <table class="table table-striped">
        <thead>
          <tr>
            <th>Asset</th>
            <th>Available</th>
            <th colspan="3">Frozen</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>USD</td>
            <td>{{ assets.USD.available }}</td>
            <td>{{ assets.USD.frozen }}</td>
          </tr>
          <tr>
            <td>BTC</td>
            <td>{{ assets.BTC.available }}</td>
            <td>{{ assets.BTC.frozen }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

  <header>
  </header>
</template>

<style scoped>

</style>
