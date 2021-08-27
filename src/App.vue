<template>
  <div id="app">
    
    <h2>Random Gif Cat</h2>
    <form @submit.prevent="generarNuevoGatitoUrl">
      <div id="form">
      <div id="input">
      <label for="titulo">Titulo:</label>
      <input required type="text" v-model="formulario.titulo" 
      placeholder="añade un titulo al gatito">
    </div>
    <div id="input">
      <label for="filtro">Filtro:</label>
      <select required v-model="formulario.filtro" id="lista filtro">
        <option value="" selected disabled></option>
        <option value="blur">blur</option>
        <option value="mono">mono</option>
        <option value="sepia">sepia</option>
        <option value="negative">negative</option>
        <option value="paint">paint</option>
        <option value="pixel">pixel</option>
      </select>
      
    </div>
    <div id="input">
      <label for="color">Color:</label>
      <select required v-model="formulario.color">
        <option value="red">Rojo</option>
        <option value="blue">Azul</option>
        <option value="green">Verde</option>
        <option value="purple">Morado</option>
        <option value="orange">Naranja</option>
      </select>
    </div>
    <div id="input">
      <label for="tamaño">Tamaño:</label>
      <input required type="number" 
      name="tamaño" 
      step="100" 
      min="100" 
      max="1000"
      v-model.number="formulario.tamaño">
    </div>
    <button class="btn btn-primary" type="submit">Obtener mi gatito</button>

    </div>
    </form>
    
    
    
    
    
    <div>
      
      <!--img v-bind:src="gatitoUrl"-->
      
      <img :src="gatitoUrl" 
      alt="gatito" 
      />
    </div>

    
  </div>
</template>

<script>


export default {
  name: 'App',
  data: () => ({
    gatitoUrl: "",
    formulario: {
      titulo: null,
      filtro: null,
      color: null,
      tamaño: null,
    }
  }),
  
  //computed: {
  //  gatitoUrl() {
  //    return "https://cataas.com" + "/cat/says/" + `${this.titulo}`
  //  }
  //},
  //data() {
  //  return {
      
  //      titulo: "",
        //tituloUrl: "cat/says/" + titulo
  //    }
    
  //},
  
  methods: {
    generarNuevoGatitoUrl() {
      console.log(this.formulario);
      
      this.gatitoUrl = `https://cataas.com/cat/gif/says/${this.formulario.titulo}?filter=${this.formulario.filtro}&color=${this.formulario.color}&width=${this.formulario.tamaño}&height=${this.formulario.tamaño}`;
      
    },
    async gatito() {
      const catImg = await fetch(`https://cataas.com/cat`);
      const data = await catImg.json();
      this.data = data;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
#form {
  background-color: rgb(255, 118, 118);
  padding: 2rem;
}
#input{
  padding: 1rem;
}
body {
  background-color: aqua;
}
</style>
