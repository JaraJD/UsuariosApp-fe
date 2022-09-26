
/* -----------------------------------HTML------------------------------------------------- */

<template>

    <div class="signUp_user">
        <div class="container_signUp_user">
            <h2>Registrarse</h2>

            <form v-on:submit.prevent="processSignUp" >
                <div class="formulario">
                    <div class="casillas">
                        <h3>Usuario</h3>
                        <input type="text" v-model="user.username" placeholder="Username">
                        <br>

                        <input type="password" v-model="user.password" placeholder="Password">
                        <br>

                        <input type="text" v-model="user.name" placeholder="Nombre">
                        <br>

                        <input type="email" v-model="user.email" placeholder="Email">
                        <br>
                    </div>
                    <div class="casillas">
                        <h3>Familiar</h3>
                        <input type="text" v-model="user.familiar.nombre" placeholder="Nombre">
                        <br>

                        <input type="text" v-model="user.familiar.apellido" placeholder="Apellido">
                        <br>

                        <input type="text" v-model="user.familiar.telefono" placeholder="Telefono">
                        <br>

                        <input type="text" v-model="user.familiar.genero" placeholder="Genero">
                        <br>

                        <input type="text" v-model="user.familiar.parentesco" placeholder="Parentesco">
                        <br>

                        <input type="email" v-model="user.familiar.email" placeholder="Email">
                        <br>
                    </div>
                    <div class="casillas">
                        <h3>Medico</h3>
                        <input type="text" v-model="user.medico.nombre" placeholder="Nombre">
                        <br>

                        <input type="text" v-model="user.medico.apellido" placeholder="Apellido">
                        <br>

                        <input type="text" v-model="user.medico.telefono" placeholder="Telefono">
                        <br>

                        <input type="text" v-model="user.medico.genero" placeholder="Genero">
                        <br>

                        <input type="text" v-model="user.medico.especialidad" placeholder="Especialidad">
                        <br>

                        <input type="text" v-model="user.medico.registro" placeholder="Registro">
                        <br>

                    </div>
                </div>
                
                

                <button type="submit">Registrarse</button>
            </form>
        </div>

    </div>

</template>

/* ------------------------------------------JS-------------------------------------------------------- */

<script>
import axios from 'axios';

export default {
    name: "SignUp",

    data: function(){
        return {
            user: {
                username: "",
                password: "",
                name: "",
                email: "",
                familiar: {
                    nombre: "",
                    apellido: "",
                    telefono: "",
                    genero: "",
                    parentesco: "",
                    email: "",
                },
                medico: {
                    nombre: "",
                    apellido: "",
                    telefono: "",
                    genero: "",
                    especialidad: "",
                    registro: "",
                }
            }
        }
    },
    methods: {
        processSignUp: function(){
            axios.post(
                "https://app-usuarios-server.herokuapp.com/user/",
                this.user,
                {headers: {}}
            )
                .then((result) => {
                    let dataSignUp = {
                        username: this.user.username,
                        token_access: result.data.access,
                        token_refresh: result.data.refresh,
                    }

                this.$emit('completedSignUp', dataSignUp)

            })
            .catch((error) => {
                console.log(error)
                alert("ERROR: Fallo en el registro.");
            });
        }
    }
}

</script>

/* ---------------------------------------CSS-------------------------------------------------- */

<style>
    .signUp_user{
        margin: 0;
        padding: 0%;
        height: 100%;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .container_signUp_user {
        border: 3px solid #283747;
        border-radius: 10px;
        width: 80%;
        height: 60%;

        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin: 10px 0 0 0;
    }

    .signUp_user h2{
        color: #283747;
    }

    .signUp_user form{
        width: 70%;
    }

    .formulario {
        display: flex;
        justify-content: space-around;
    }

    .casillas h3{
        text-align: center;
        height: 10px;
    }


    .signUp_user input{
        width: 100%;

        box-sizing: border-box;
        margin: 5px 0;

        border: 1px solid #283747;
    }

    .signUp_user button{
        width: 100%;
        height: 40px;

        color: #E5E7E9;
        background: #283747;
        border: 1px solid #E5E7E9;

        border-radius: 5px;
        padding: 10px 25px;
        margin: 5px 0 25px 0;

    }

    .signUp_user button:hover{
        color: #E5E7E9;
        background: crimson;
        border: 1px solid #283747;
    }

</style>