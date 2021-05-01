<template>
  <div class="user-info">
    <img
      :src="data.avatar"
      :alt="data.name"
      class="avatar"
    />

    <div>
      <h2>
        {{ data.name }}&nbsp;
        <a
          class="full-name-link"
          :href="`https://github.com/${data.login}`"
          target="_blank"
        >
          ({{ data.login }})
          </a>
      </h2>

      <ul class="user-data">
        <li>Seguidores: {{ data.followers }}</li>
        <li>Seguindo: {{ data.following }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  /**
   * Nome padrão, que pode ser
   * alterado por quem utilizar
   * o componente
   */
  name: 'user-info',

  mounted() {
    console.log(this.data);
  },

  /**
   * Propriedades repassadas ao
   * componente
   */
  props: {
    data: Object,
  }
}
</script>

<style scoped>
.avatar {
  border-radius: 100px;
  height: 200px;
  margin-right: 10px;
  width: 200px;
}

.full-name-link {
  color: '#333';
  font-weight: 'bold';
  text-decoration: 'underline';
}

.user-info {
  align-items: center;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.user-data {
  list-style-type: none;
  margin: 0;
  padding: 0;
  margin-top: 10px;
}
</style>




