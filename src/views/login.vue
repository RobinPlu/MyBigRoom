<template>
    <div class="hello">
        <div class="inscription">
            <h1>inscription / connexion</h1>

            <h2>Inscription</h2>
            <p>
                <label for="name">Name</label>
                <input id="name" v-model="loginSubscribe" type="text" name="name">
            </p>

            <p>
                <label for="password">Password</label>
                <input id="password" v-model="passwordSubscribe" type="text" name="password">
            </p>

            <p>
                <button @click="subscribe(loginSubscribe, passwordSubscribe)">S'inscrire</button>
            </p>

            <h2>Connexion</h2>
            <p>
                <label for="username">Name</label>
                <input id="username" v-model="loginConnect" type="text" name="username">
            </p>

            <p>
                <label for="passwordLog">Password (>8car.)</label>
                <input id="passwordLog" v-model="passwordConnect" type="text" name="passwordLog">
            </p>

            <p>
                <button @click="connect(loginConnect, passwordConnect)">Connexion</button>
            </p>
        </div>


    </div>
</template>

<script>
    import axios from "axios";

    export default {
        name: "Home",
        props: {
            msg: String
        },
        data() {
            return {
                info: null,
                name: "",
                password: "",
                username: "",
                passwordLog: "",
                submit: "",

                loginSubscribe: "",
                passwordSubscribe: "",
                loginConnect: "",
                passwordConnect: "",
                isConnected: true,
            };
        },
        mounted: function() {
            // get les chatrooms


            // get les users
            axios
                .get(
                    "http://localhost:8888/PHP_SQL/controllers/users_controller.php?action=getUsers"
                )
                .then(
                    response => {
                        //console.log(response.data);
                        this.users = response.data;
                        console.log("users:", this.users);
                    },
                    function(error) {
                        console.log(error);
                    }
                );
        },

        methods: {
            subscribe: function(login, password) {
                axios
                    .get(
                        "http://localhost:8888/PHP_SQL/controllers/users_controller.php?action=inscription&login=" +
                        login +
                        "&password=" +
                        password
                    )
                    .then(
                        response => {
                            console.log(response);
                        },
                        function(error) {
                            console.log(error);
                        }
                    );
            },
            connect: function(login, password) {
                axios
                    .get(
                        "http://localhost:8888/PHP_SQL/controllers/users_controller.php?action=connexion&login=" +
                        login +
                        "&password=" +
                        password
                    )
                    .then(
                        response => {
                            console.log(response);
                            if(response.data==true){
                                this.isConnected=true;
                            }
                        },
                        function(error) {
                            console.log(error);
                        }
                    );
            }
        }
    };
</script>
<style>
    body {
        margin: 0;
        padding: 0;
    }
</style>