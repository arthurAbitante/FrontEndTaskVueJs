<script>
import axios from 'axios';

export default {
  name: 'Tarefas',
  props: {
    msg: String
  },
  data: () => {
    return {
      tarefas: [],
      tarefa: undefined,
      mensagem: ""
    }
  },
  methods: {
    lista: (scope) => {
      axios.get(`http://127.0.0.1:5173/api/Tarefas`).then((res) => {
        console.log(res)
        scope.tarefas = res.data
      })
    },
    salvar() {
      if(this.tarefa){
        this.alterar()
        return
      }

      axios.post('http://127.0.0.1/:44314/api/Tarefas', {
       // nome: document.getElementById("nome").value,
       // telefone: document.getElementById("telefone").value,
       // endereco: document.getElementById("endereco").value
      }).then((res)=> {
        this.lista(this)
      })

      
    },
    excluir(id){

      if(confirm("Confirma a exclusão?")){
        axios.delete(`https://localhost:44314/api/Tarefas/${id}`,{
        }).then(() => {
          this.lista()
        })
      }
    },
    editar(tarefa){
    //  nome: document.getElementById("nome").value = cliente.nome,
     // telefone: document.getElementById("telefone").value = cliente.telefone,
     // endereco: document.getElementById("endereco").value = cliente.endereco,
      this.tarefa = tarefa
    },
    alterar(){
    //  this.cliente.nome = document.getElementById("nome").value
    //  this.cliente.telefone = document.getElementById("telefone").value
     // this.cliente.endereco = document.getElementById("endereco").value

      axios.put(`https://localhost:44314/api/Tarefas/${this.tarefa.id}`, {
      }).then((res)=> {
        this.lista(this)
        this.tarefa = undefined

      //  document.getElementById("nome").value = ""
       // document.getElementById("telefone").value = ""
       // document.getElementById("endereco").value = ""
      })
    }
  },
  created(){
    this.lista(this)
  }
}

</script>

<template>
<div>

  <form>
    <div class="form-group">
      <label for="titulo">Titulo</label>
      <input type="hidden" id="id" name="id">
      <input type="text" class="form-control" id="titulo" name="titulo" placeholder="Digite o titulo">
    </div>
    <div class="form-group">
      <label for="telefone">Descrição</label>
      <input type="text" class="form-control" id="descricao" name="descricao" placeholder="Digite a descrição">
    </div>
        <div class="form-group">
      <label for="data">Data</label>
      <input type="text" class="form-control" id="data" name="data" placeholder="Digite a data">
    </div>
    <div class="form-group">
      <label for="tempo">Tempo de duração</label>
      <input type="text" class="form-control" id="tempo" name="tempo" placeholder="Digite o tempo de duração">
    </div>
        <div class="form-group">
      <label for="tipo">Tipo</label>
      <input type="text" class="form-control" id="tipo" name="tipo" placeholder="Digite o tipo">
    </div>
    <button v-on:click="salvar()" type="button" class="btn btn-primary">Enviar</button>

    <div style="color: red">
      {{mensagem}}
    </div>
  </form>


  <table class="table table-striped">
    <thead>
      <tr>
        <th>
          Id
        </th>
        <th>
          Título
        </th>
        <th>
          Descrição
        </th>
        <th>
          Data
        </th>
        <th>
          Tempo de duração
        </th>
        <th>
          Tipo
        </th>
        <th colspan="2">
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="tarefa in tarefas" v-bind:key="tarefa.id">
        <td>
          {{tarefa.id}}
        </td>
        <td>
          {{tarefa.titulo}}
        </td>
        <td>
          {{tarefa.descricao}}
        </td>
        <td>
          {{tarefa.data}}
        </td>
        <td>
          {{tarefa.tempoDuracao}}
        </td>
        <td>
          {{tarefa.tipo}}
        </td>
        <td>
          <button class="btn btn-primary" v-on:click="editar(tarefa)">Editar</button>
        </td>
        <td>
          <button class="btn tbn-primary" v-on:click="excluir(tarefa.id)">Remover</button>
        </td>
      </tr>
    </tbody>
  </table>
</div>
    <h1 class="green">{{ msg }}</h1>

</template>

<style>

</style>
