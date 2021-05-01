<template>
  <div id="app">

    <div>
      <div class="title">
        <h1>Pesquisa de usuários no Github com Vue&nbsp;&nbsp;</h1>
        <img
          src="./assets/logo.png"
          alt="Vue logo"
          class="logo"
        />
      </div>

      <!--
        Links que ativam/desativam abas
        A aba "ativa" é definida a partir
        do estado da aplicação
      -->
      <ul class="header">
        <li>
          <a
            class="linkButton"
            @click="setCurrentTab('home')"
            :class="{ active: isActive('home') }"
          >
            Home
            </a>
        </li>

        <li>
          <a
            class="linkButton"
            @click="setCurrentTab('repos')"
            :class="{ active: isActive('repos') }"
          >
            Repositórios {{ getCountRepositorios }}
            </a>
        </li>

        <li>
          <a
            class="linkButton"
            @click="setCurrentTab('starred')"
            :class="{ active: isActive('starred') }"
          >
            Favoritos {{ getCountStarred }}
            </a>
        </li>
      </ul>
    </div>

    <!-- Exibição de componentes conforme activeLink -->
    <div class="content">

      <home
        v-show="isActive('home')"
        :userInfo="userInfo"
        :onFetchData="fetchUserInfoFromGithub"
        :isFetchingData="isFetchingData"
      ></home>

        <repos
          v-show="isActive('repos')"
          :repos='repos'
          type='repos'
        ></repos>

          <repos
            v-show="isActive('starred')"
            :repos='starred'
            type='starred'
          ></repos>
    </div>
  </div>

</template>

<script>
/**
 * Importação dos componentes
 */
import Home from './components/home/Home';
import Repos from './components/repos/Repos';
import { UserServiceObservable } from './services/UserServiceObservable';

export default {
  /**
   * Indicando utilização dos componentes
   */
  components: {
    Home,
    Repos,
  },

  /**
   * Aqui é um ponto recomendável para instanciar
   * objetos que não são reativos.
   */
  created() {
    this.userServiceObservable = new UserServiceObservable();
  },

  /**
   * Boa prática - data() deve ser uma função
   * retornando um objeto. Isso garante
   * imutabilidade e estado único para
   * cada componente.
   *
   * data() contém o "estado" do app/componente
   * que "reage" às mudanças
   */
  data() {
    return {
      /**
       * Indicador do link ativo
       */
      activeLink: 'home',

      /**
       * Indicador de busca de dados
       * em andamento
       */
      isFetchingData: false,

      /**
       * Objeto de dados do usuário
       * do Github
       */
      userInfo: null,

      /**
       * Lista de repositórios
       * do usuário
       */
      repos: null,

      /**
       * Lista de repositórios
       * favoritados pelo usuário
       */
      starred: null,
    };
  },

  /**
   * O objeto Vue também pode
   * conter métodos para manipular
   * o estado de data()
   */
  methods: {
    /**
     * Indica se o link que chega do parâmetro
     * é o link ativo no momento
     */
    isActive: function(currentTab) {
      return this.activeLink === currentTab;
    },

    /**
     * Define o valor do link ativo
     */
    setCurrentTab: function(currentTab) {
      this.activeLink = currentTab;
    },

    fetchUserInfoFromGithub: async function(userName) {
      /**
       * Indicando busca de dados
       */
      this.isFetchingData = true;

      /**
       * Executando o observable
       */
      this.userServiceObservable.getUserInfoFrom(userName).subscribe(
      /**
       * Tratando requisição ok
       */
        userInfo => {
          this.userInfo = userInfo,
          this.repos = userInfo.repos;
          this.starred = userInfo.starred;
          this.isFetchingData = false;
        },
        /**
         * Tratando requisição com erro
         */
        error => {
          console.error(error);

          this.userInfo = null,
          this.repos = null;
          this.starred = null;
          this.isFetchingData = false;
        },
      );
    }
  },

  computed: {

    getCountRepositorios() {
      if (this.isFetchingData || !this.repos) return '';
      return `(${this.repos.length})`;
    },

    getCountStarred() {
      if (this.isFetchingData || !this.starred) return '';
      return `(${this.starred.length})`;
    },
  }
};
</script>

<style>
/* Estilos CSS do componente principal */

.linkButton {
  cursor: pointer;
}

.title {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}

.logo {
  width: 50px;
}

h1,
h2,
p,
ul,
li {
  font-family: sans-serif;
}

ul.header li {
  display: inline;
  list-style-type: none;
  margin: 0;
}

ul.header {
  background-color: #111;
  padding: 0;
  margin: 0;
}

ul.header li a {
  color: #fff;
  font-weight: bold;
  text-decoration: none;
  padding: 20px;
  display: inline-block;
}

.content {
  background-color: #fff;
  padding: 20px;
}

.content h2 {
  padding: 0;
  margin: 0;
}

.content li {
  margin-bottom: 10px;
}

.invisible {
  display: none;
}

.loading {
  text-align: center;
  font-size: 2em;
  font-weight: bold;
}

.active {
  background-color: #0099ff;
}
</style>
