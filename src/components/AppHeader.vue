<template>
  <header>
    <div>
        BoolFlix
    </div>
    <div>
        <input type="text" :class="[active? 'active': '']" @keyup.enter="getSearch" v-model="inputText" id="search" placeholder="Start here your search">
        <!-- <button @click="getSearch"><font-awesome-icon icon="search" /></button> -->
        <font-awesome-icon @focus="startSearch" @click="getSearch" icon="search" />
    </div>

  </header>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core';
import { faSearch } from '@fortawesome/free-solid-svg-icons';

library.add(faSearch);

export default {
  name: 'AppHeader',
  data() {
      return {
          inputText:'',
          searchText: '',
          active: false,
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
      startSearch(){
          this.active = true;
      },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
header{
    height: 100px;
    color: #fff;
    background-color: #000;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 2rem;

    div:first-child{
        color: red;
        font-size: 2rem;
        font-weight: 900;
        letter-spacing: .1rem;
    }

    div:nth-child(2){
        display: flex;
        align-items: center;

        #search{
            display: none;
            padding: 6px;
            border-radius: 10px;
            margin-right: 10px;
        }
        #search.active{
            display: block;
        }
    }

    div:nth-child(2):hover{
        input{
            display: block;
        }
    }
}

</style>
