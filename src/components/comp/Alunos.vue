<template>
  <div class="container">
    <div class="col-lg-8">
      <div class="card">
        <div class="card-header">
          <titulo title="Alunos"/>
          <!-- <h4>{{ title }}</h4> -->
          <small>Cadastro de Alunos</small>
          <div class="row">
            <div class="col-lg-9">
              <input
                class="form-control"
                type="text "
                id="name"
                v-model="name"
                v-on:keyup.enter="Adicionar()"
              />
            </div>
            <div class="col-lg-1">
              <button class="btn btn-primary" @click="Adicionar()">Cadastrar</button>
            </div>
          </div>
        </div>
        <div class="card-body">
          <table class="table table-sm" v-if="Alunos.length">
            <tr>
              <th>#</th>
              <th>Nome</th>
              <th>Idade</th>
              <th>Comando</th>
            </tr>
            <tr v-for="(item, index) in Alunos" :key="index">
              <td>{{ item.id }}</td>
              <!-- <td>{{item.id}}</td> -->
              <td>{{ item.name }}</td>
              <td>{{ item.age }}</td>
              <td><button class="btn btn-danger btn-sm" @click="Remover(item)">Excluir</button></td>
            </tr>
          </table>
        </div>
        <div class="card-footer bg-danger text-warning" v-if="!Alunos.length">
          Nenhum aluno cadastrado
        </div>
      </div>
    </div>

  </div>
</template>

<script>

import titulo from '../comp/shared/titulo';

export default {
  components:{
    titulo
  },
  data() {
    return {
      name: "",
      title: "Alunos",
      Alunos: [],
    };
  },
  //vai buscar os dados no servidor
  created(){
    this.$http
    .get('http://localhost:3000/alunos')
    .then(res => res.json())
    .then(alunos => this.Alunos = alunos)
  },
  props: {},
  methods: {
    Remover(studentName) {
        this.$http
        .delete(`http://localhost:3000/alunos/${studentName.id}`)
        .then(()=>{
          let indice = this.Alunos.indexOf(studentName)
          this.Alunos.splice(indice, 1)
        })
        
    },

    Adicionar() {
      let _objAluno = {name: this.name, age: "33" };

      this.$http
        .post('http://localhost:3000/alunos', _objAluno)
        .then(res => res.json())
        .then(studentBack => {
          this.Alunos.push(studentBack);
          this.name = '';
        })
        //.then(alunos => this.Alunos = alunos)


    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card {
  margin-top: 0.5em;
}
</style>
