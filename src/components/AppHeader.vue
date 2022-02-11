<template>
  <header>
      <!-- Utilizzato BootstrapVue per l'header e la navbar solo per un primo approccio -->
        <b-navbar toggleable="lg" fixed type="dark" variant="dark">
            <div>
                <img src="https://fontmeme.com/permalink/211007/c072857f28ffed69c9266a55183f4c20.png" alt="">
            </div>
            <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
            <b-collapse id="nav-collapse" is-nav>
            <!-- Right aligned nav items -->
            <b-navbar-nav class="ml-auto">
                <b-nav-form>
                <b-form-input size="sm" class="mr-sm-2" placeholder="Search"
                    :class="[active? 'active': '']" @keyup.enter.prevent="getSearch" v-model="inputText"
                    id="search"
                >
                </b-form-input>
                        
                <font-awesome-icon @focus="startSearch" @click="getSearch" icon="search" 
                    id="icon-search"
                />
                </b-nav-form>
            </b-navbar-nav>
            </b-collapse>
        </b-navbar>
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
    .bg-dark{
        background-color: rgb(20, 20, 20)!important;

    }
}
.navbar-expand-lg {
    justify-content: space-between;
    padding: 0 2rem;

    form{
        display: flex;

        #icon-search{
            color: #fff;
            font-size: 1.9rem;
            padding: 3px;
            margin-left: 5px;
        }

        // #search{
        //     display: none;
        //     &.active{
        //             display: block;
        //         }
        // }

    }
}
.navbar-dark .navbar-brand {
    color: #e50914;
    font-size: 2rem;
    font-weight: 700;
    letter-spacing: .2rem;
}
.navbar-dark .navbar-brand:hover, .navbar-dark .navbar-brand:focus {
    color: #e50914;
}
.navbar{
    min-height: 100px;
}

.navbar-collapse {
     flex-grow: 0;
}

</style>
