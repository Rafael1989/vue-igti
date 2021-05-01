<template>
  <div>
    <search
      :onEnter="onFetchData"
      :isFetchingData="isFetchingData"
      description="Usuário do Github..."
    />
    <div v-if="isFetchingData || !userInfo">
      <simple-message :message="isFetchingData ? 'Carregando...' : 'Informe um usuário válido do Github'" />
    </div>
    <div v-else>
      <user-info :data="userInfo" />
    </div>
  </div>
</template>

<script>
import Search from '../shared/Search';
import SimpleMessage from '../shared/SimpleMessage';
import UserInfo from '../shared/UserInfo';

export default {
  name: 'home',

  /**
   * Componentes utilizados por Home
   */
  components: {
    Search,
    SimpleMessage,
    UserInfo,
  },

  props: {
    onFetchData: Function,
    userInfo: Object,
    isFetchingData: Boolean,
  },
};
</script>

<style>
</style>
