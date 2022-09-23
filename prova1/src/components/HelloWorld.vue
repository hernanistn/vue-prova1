<template>
  <div class="center-row-direction">
    <form @submit.prevent="submit()">
      <label for="name">Nome</label>
      <input type="text" id="name" v-model="nomeAluno" required /><br>
      <label for="nota1" id="nota1">Nota1</label>
      <input type="number" id="nota1" v-model="nota1" required /><br>
      <label for="nota1" id="nota2">Nota2</label>
      <input type="number" id="nota2" v-model="nota2" required><br>
      <label for="nota1" id="nota3">Nota3</label>
      <input type="number" id="nota3" v-model="nota3" required /><br>
      <label for="nota1" id="nota1">Média aproveitamento</label>
      <input type="number" id="mediaAprov" v-model="mediaAprov" required /><br>
      <input type="submit" id="submit" value="Salvar" />
    </form><br>

    <div>
      <table>
        <tr v-for="aluno in alunos" :key="aluno.id">
          <div :class="getClass(aluno)">
          <td>{{aluno.nomeAluno}}</td>
          <td>{{handleAproved(aluno)}}</td>
        </div>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      alunos: [],
      nomeAluno: '',
      nota1: null,
      nota2: null,
      nota3: null,
      mediaAprov: null,
      aproved : null
    }
  },

  methods: {
    submit() {
      const newAluno = {
        id: 0,
        nomeAluno: this.nomeAluno,
        nota1: this.nota1,
        nota2: this.nota2,
        nota3: this.nota3,
        mediaAprov: this.mediaAprov,
        aproved : false
      }
      newAluno.id = this.alunos.length + 1
      newAluno.aproved = this.isAproved(newAluno)
      this.alunos.push(newAluno)
      this.clearFields()
    },
    clearFields() {
      this.nomeAluno = ''
      this.nota1 = null
      this.nota2 = null
      this.nota3 = null
      this.mediaAprov = null
    },
    isAproved(aluno) {
      const media = (aluno.nota1 + (aluno.nota2 * 2) + (aluno.nota3 * 3) + aluno.mediaAprov) / 7
      if (media >= 7) {
        return true
      }
      return false
    },
    getClass(aluno){
      if(aluno.aproved){
        return "blue-background"
      }
      return "red-backgroud"
    },
    handleAproved(aluno){
      if(aluno.aproved){
        return "Aprovado"
      }
      return "Reprovado"
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.red-backgroud{
  background-color: red;
}

.blue-background{
  background-color: blue;
}

.center-row-direction {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
