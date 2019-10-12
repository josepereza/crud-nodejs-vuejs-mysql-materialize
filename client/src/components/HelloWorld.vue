<template>
  <div class="hello">
    <div id="todo-list-example" class="container">
      <h2>Todo list -Nodejs - Vuejs- Materialize</h2>
      <form v-on:submit.prevent="addNewUser">
        <div class="row">
          <div class="input-field">
            <input type="text" v-model="usernombre" id="nombreinput" placeholder="Nombre" class="validate" />
            <label for="nombreinput">Nombre</label>
          </div>
        </div>

       <div class="row">
          <div class="input-field">
           <input v-model="userpoblacion" id="poblacioninput"  type="text" placeholder="poblacion" class="validate" />     
           <label for="poblacioninput">Poblacion</label>
          </div>
       </div>
        
        <div class="row">
            <div class="input-field">
              <input v-model="usersaldo" id="saldoinput" class="form-control" placeholder="saldo" type="text" />
        <label for="saldoinput">saldo</label>
            </div>
        </div>
        <button v-if="this.isEdit == false"
          type="submit"
          class="btn btn-success btn-block mt-3">Submit</button>
        <button v-else 
          type="button"
          v-on:click="updateUser()"
          class="btn btn-primary btn-block mt-3">Update</button>
      </form>
      <table class="table">
        <tr v-for="todo in todos" v-bind:key="todo.id" v-bind:title="todo.nombre">
          <td class="text-left">{{todo.nombre}}</td>
          <td class="text-left">{{todo.poblacion}}</td>
          <td class="text-left">{{todo.saldo}}</td>
          <td class="text-right">
            <button
              v-on:click="editUser(todo.id,todo.nombre,todo.poblacion,todo.saldo)"
              class="btn btn-info">Edit</button>
            <button v-on:click="deleteUser(todo.id)" class="btn red">Delete</button>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      id: "",
      usernombre: "",
      userpoblacion: "",
      usersaldo: null,
      isEdit: false
    };
  },
  mounted() {
    this.getUsers();
  },
  methods: {
    getUsers() {
      this.axios.get("http://173.249.39.9:3000/api/listado").then(result => {
        this.todos = result.data;
      });
    },
    addNewUser() {
      this.axios
        .post("http://173.249.39.9:3000/api/crear", {
          nombre: this.usernombre,
          poblacion: this.userpoblacion,
          saldo: this.usersaldo
        })
        .then(res => {
          this.usernombre = "";
          this.userpoblacion = "";
          this.usersaldo = null;
          this.getUsers();
          console.log(res);
        })
        .catch(err => {
          console.log(err);
        });
    },
    editUser(id, title, pueblo, saldo) {
      this.id = id;
      this.usernombre = title;
      this.userpoblacion = pueblo;
      this.usersaldo = saldo;
      this.isEdit = true;
    },
    updateUser() {
      this.axios
        .put(`http://173.249.39.9:3000/api/modificar/${this.id}`, {
          nombre: this.usernombre,
          poblacion: this.userpoblacion,
          saldo: this.usersaldo
        })
        .then(res => {
          this.usernombre = "";
          this.userpoblacion = "";
          this.usersaldo = null;
          this.isEdit = false;
          this.getUsers();
          console.log(res);
        })
        .catch(err => {
          console.log(err);
        });
    },
    deleteUser(id) {
      this.axios
        .delete(`http://173.249.39.9:3000/api/borrar/${id}`)
        .then(res => {
          this.username = "";
          this.getUsers();
          console.log(res);
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>