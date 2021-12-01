<template>
  <header>
    <h2>AppHeader</h2>
    <!-- Input e button per la ricerca da spostare poi nell Header -->
    <!-- <label>Ricerca qui il tuo film: </label> -->
    <input type="text" @keyup.enter="getSearch" v-model="inputText" id="search" placeholder="Start here your search">
    <button @click="getSearch">Search</button>

  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  data() {
      return {
          inputText:'',
          searchText: '',
      }
  },
  props: {
    
  },
  methods: {
      getSearch(){
          this.searchText = this.inputText.toLowerCase();
          this.inputText = '';
          this.$emit('searchUser', this.searchText);
      },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
header{
    height: 100px;
    color: #fff;
}

</style>
