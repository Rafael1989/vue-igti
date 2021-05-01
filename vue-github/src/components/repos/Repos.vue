<template>
  <div class="repos">
    <ul v-if="!!repos && repos.length > 0">
      <li
        v-for="(repo, index) in repos"
        :key="index"
      >
        <a
          :href="repo.html_url"
          target="_blank"
        >{{ repo.name }}</a>
          </li>
    </ul>
    <p v-else>
      Não há nenhum {{ type === 'repos' ? 'repositório' : 'favorito' }} para ser exibido.
    </p>
  </div>
</template>

<script>
export default {
  name: 'repos',

  props: {
    repos: Array,
    type: String,
  },
};
</script>

<style>
.repos ul,
.repos li {
  list-style-type: none;
  margin: 0;
  padding: 0;
  font-family: monospace;
  font-size: 1.1em;
  margin-bottom: 5px;
}

a {
  color: #333;
  font-weight: bold;
  text-decoration: none;
  text-transform: none;
}
</style>
