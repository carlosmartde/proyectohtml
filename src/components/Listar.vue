<template>
    <div class="container">
        <br/><br/>
        <router-link to="/crear" class="btn btn-success">Agregar nuevo empleado</router-link> 
        <br/><br/>

    <div class="card">
        <div class="card-header">
            EMPLEADOS
        </div>
        <div class="card-body">
            <table class="table">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>NOMBRE</th>
                        <th>CORREO</th>
                        <th>ACCIONES</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="empleado in empleados" :key="empleado.id">
                        <td>{{ empleado.id }}</td>
                        <td>{{ empleado.nombre }}</td>
                        <td>{{ empleado.correo }}</td>
                        <td>
                            <div class="btn-group" role="group" aria-label="">
                                <router-link :to="{name:'Editar',params:{id:empleado.id}}" class="btn btn-info">EDITAR</router-link>
                                <button type="button" v-on:click="borrarEmpleado(empleado.id)" class="btn btn-danger">BORRAR</button>
                            </div>
                        </td>
                    </tr>
                    
                </tbody>
            </table>
        </div>
    </div>
    </div>

</template>

<script>
export default{

        data (){

            return{
                empleados:[]
            }

        },
        created:function(){
            this.consultarEmpleados();

        },
        methods:{
            consultarEmpleados(){
                fetch('http://localhost/empleados/')
                .then(respuesta=>respuesta.json())
                .then((datosRespuesta)=>{

                    console.log(datosRespuesta)
                    this.empleados=[]
                    if(typeof datosRespuesta[0].success==='undefined'){
                            this.empleados=datosRespuesta;
                    }
                })
                .catch(console.log)
            },

            borrarEmpleado(id){
                console.log(id);
                fetch('http://localhost/empleados/?borrar='+id)
                .then(respuesta=>respuesta.json())
                .then((datosRespuesta)=>{

                    console.log(datosRespuesta)
                    window.location.href="Listar"
                })
                .catch(console.log)
            }
        }
}
</script>

<style scoped>
body{
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #182a3f;
  min-height: 100vh;
  margin: 0;
  padding: 0;
}
</style>