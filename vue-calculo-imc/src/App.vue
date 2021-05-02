<template>
  <div id="app">
    <h1>Cálculo de IMC</h1>
    <div>
      <p>IMC é a sigla para Índice de Massa Corpórea, parâmetro adotado pela Organização Mundial de Saúde para calcular o peso ideal de cada pessoa.</p>

      <p>O índice é calculado da seguinte maneira: divide-se o peso do paciente pela sua altura elevada ao quadrado. Diz-se que o indivíduo tem peso normal quando o resultado do IMC está entre 18,5 e 24,9.</p>
          
      <p>Quer descobrir seu IMC? Insira seu peso e sua altura nos campos abaixo e compare com os índices da tabela. Importante: siga os exemplos e use pontos como separadores.</p>
      <form autocomplete="off">
          <div class="ui-g ui-fluid">
      
              <div class="ui-g-12">
                  <label for="peso">Peso (Ex: 95)</label>
                  <input id="peso" type="text" name="peso" placeholder="0,00" required v-model="peso">
              </div>

              <div class="ui-g-12">
                  <label for="altura">Altura (Ex: 185)</label>
                  <input id="altura" type="text" name="altura" placeholder="0,00" required v-model="altura">
              </div>
          
              <div class="ui-g-12">
                  <button type="button" @click="calcular()">Calcular</button>
              </div>
          </div>
      </form>
      <h2>
        Veja a interpretação do IMC
      </h2>

      <table>
          <tr>
              <th>IMC</th>
              <th>CLASSIFICAÇÃO</th>
              <th>OBESIDADE (GRAU)</th>
          </tr>
          <tr>
              <td>MENOR QUE 18,5</td>
              <td>MAGREZA</td>
              <td>0</td>
          </tr>
          <tr>
              <td>ENTRE 18,5 E 24,9</td>
              <td>NORMAL</td>
              <td>0</td>
          </tr>
          <tr>
              <td>ENTRE 25,0 E 29,9</td>
              <td>SOBREPESO</td>
              <td>I</td>
          </tr>
          <tr>
              <td>ENTRE 30,0 E 39,9</td>
              <td>OBESIDADE</td>
              <td>II</td>
          </tr>
          <tr>
              <td>MAIOR QUE 40,0</td>
              <td>OBESIDADE GRAVE</td>
              <td>III</td>
          </tr>
      </table>
      <h2>SEU IMC: {{imc}}</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',

  data() {
    return {
      peso: 0,
      altura: 0,
      imc: 0,
    };
  },

  methods: {
    calcular: function() {
      console.log(this.peso);
      if(this.peso.includes(",") || this.peso.includes(".") || this.altura.includes(",") || this.altura.includes("."))
        alert("Não use vírgula, nem ponto.")
      this.imc = (this.peso / ((this.altura/100) * (this.altura/100))).toFixed(2);
    },

  },
};
</script>

<style>
html {
    height: 100%;
    background-image: url(https://media.giphy.com/media/C4XAKMeIxZFQqM8ALj/giphy.gif);
    background-repeat: no-repeat, repeat;
    background-size: cover; 
  }

  body{
      padding: 10px;
  }
</style>
