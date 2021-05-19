<template>
  <div id="app" class="container">
<div class="page-header">
    <h1>Lista de Animes</h1>  
</div>
<div>
    <form>
      <table class="table table-striped">
        <thead>
          <tr>
            <th> Id </th>
            <th> Nombre </th>
            <th> Genero </th>
            <th> Capitulos </th>
            <th> Nota </th>
            <th>Acciones</th>
          </tr>
        </thead>
        <tbody>
         
        <tr v-for="anime in animes2" :key="anime">  
                <td>{{anime.id}}</td> 
                <td>{{anime.anime_name}}</td>            
                <td>{{anime.genre}}</td> 
                <td>{{anime.chapters}}</td>
                <td>{{anime.rating}}</td>
        </tr>
          <tr>
              <td> 
              <input type="text" class="form-control" placeholder="Ingrese el id del anime" v-model="anime_nueva.id" />
            </td>
            <td> 
              <input type="text" class="form-control" placeholder="Ingrese el nombre del anime" v-model="anime_nueva.nombre" />
            </td>
            <td>  
              <input type="text" class="form-control" placeholder="Ingrese el genero" v-model="anime_nueva.genero" />
            </td>
            <td>
              <input type="number" class="form-control" placeholder="Ingrese el numero de capitulos" v-model="anime_nueva.capitulos" /> 
            </td>
            <td>
              <input type="number" class="form-control" placeholder="Ingrese la nota" v-model="anime_nueva.nota"/> 
            </td>
            <td> 
               <input type="button" v-on:click="agregar(anime)" value="Crear"/>
                <input type="button" v-on:click="modificar(anime)" value="Modificar"/>
                <input type="button" v-on:click="eliminar(anime)" value="Eliminar"/>   |
            </td>
          </tr>
        </tbody>
      </table>
    </form>
</div>
  </div>
</template>
<script>
import Firebase from 'firebase'
import toastr from 'toastr'
let config = {
  apiKey: "AIzaSyAa_-x54jkLBY7QZA0fMPn8J7wRn7mqjtk",
  authDomain: "root-setting-261509.firebaseapp.com",
  databaseURL: "https://root-setting-261509-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "root-setting-261509",
  storageBucket: "root-setting-261509.appspot.com",
  messagingSenderId: "591450892066",
  appId: "1:591450892066:web:661ffa33edfe08d315677b"
  
}
let app = Firebase.initializeApp(config)
let db = app.database()
const db2 = firebase.firestore();

let animesRef = db.ref('animes')
let animesRef2 = db2.collection("animes");

export default {
  name: 'App',
  firebase: {
    animes: animesRef,
    animes2: animesRef2
  },
  data(){
    return {
      anime_nueva: {
        id: '',
        nombre: '',
        genero: '',
        capitulos: '',
        nota: ''

      }
    }
  },
  methods:{
    agregar: function() {
      animesRef.push(this.anime_nueva, function(error){
        console.log(animesRef2)
        if (error){
          toastr.error('Error al intentar agregar el registro.', 'Aviso');
        }else{          
          toastr.success('Registro agregado correctamente.', 'Aviso');
        }
      });
      this.anime_nueva.id = '';
      this.anime_nueva.nombre = '';
      this.anime_nueva.genero = ''; 
      this.anime_nueva.capitulos = ''; 
      this.anime_nueva.nota = ''; 
    },
    modificar: function(p_anime){      
      animesRef.child(p_anime['key']).set({ 
        nombre: p_anime.nombre,
        cantidad: p_anime.cantidad,
        genero:p_anime.genero,
        capitulos:p_anime.capitulos,
        nota:p_anime.nota

      }, function(error){
        if (error){
          toastr.error('Error al intentar modificar el registro.', 'Aviso');
        }else{          
          toastr.success('Registro modificado correctamente.', 'Aviso');
        }
      });      
    },
    eliminar: function(p_anime){
      animesRef.child(p_anime['.key']).remove(function(error){ 
        if (error){
          toastr.error('Error al intentar eliminar el registro.', 'Aviso');
        }else{          
          toastr.success('Registro eliminado correctamente.', 'Aviso');
        }
      });      
    },
  }
}
</script>

