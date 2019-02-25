<template>
  <div class="hello">
    <link rel="stylesheet" href="https://puteborgne.sexy/_css/normalize.css"/>
    <link rel="stylesheet" href="https://puteborgne.sexy/_css/skeleton.css"/><Chatroom/>
    <h1>{{ msg }}</h1>
    <div v-if="!isConnected" class="inscription">
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

    <div v-else>
      <h2>Chattes rooms</h2>
      <div v-for="chatroom in chatrooms">
        <router-link :to="'chatroom?chatroomId=' + chatroom.id">Ouvrir "{{chatroom.name}}"</router-link> |
        <input type="text" v-model="chatroom.name">
        <button v-on:click="modifierChatroom(chatroom.id, chatroom.name)">Modifier nom</button>

        <button v-on:click="supprimerChatroom(chatroom.id)">Supprimer</button>
      </div>
      <input type="text" v-model="newChatroom">
      <button v-on:click="creerChatroom()">Créer chatroom "{{newChatroom}}"</button>

      <h2>Users</h2>
      <div v-for="user in users">
        <router-link :to="'user?userId=' + user.id">Ouvrir "{{user.login}}"</router-link> |
        <input type="text" v-model="user.login">
        <button v-on:click="modifierProfil(user.id, user.login)">Modifier nom</button>
        <button v-on:click="supprimerProfil(user.id)">Supprimer</button>
      </div>
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
                chatID: "",
                chatEdit: "",
                chatDelete: "",
                userID: "",
                userEdit: "",
                userDelete: "",

                loginSubscribe: "",
                passwordSubscribe: "",
                loginConnect: "",
                passwordConnect: "",
                isConnected: true,
                newChatroom: "",
                chatrooms: [],
                users: []
            };
        },
        mounted: function() {
            // get les chatrooms
            axios
                .get(
                    "http://localhost:8888/PHP_SQL/controllers/chatroom_controller.php?action=getChatrooms"
                )
                .then(
                    response => {
                        // console.log(response.data);
                        this.chatrooms = response.data;
                        console.log("chatrooms", this.chatrooms);
                    },
                    function(error) {
                        console.log(error);
                    }
                );

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
            modifierChatroom: function(id, newName) {
                console.log(id, newName);
                axios
                    .get(
                        "http://localhost:8888/PHP_SQL/controllers/chatroom_controller.php?action=modify&id=" +
                        id +
                        "&newName=" +
                        newName
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
            creerChatroom: function() {
                axios
                    .get(
                        "http://localhost:8888/PHP_SQL/controllers/chatroom_controller.php?action=create&name=" +
                        this.newChatroom
                    )
                    .then(
                        response => {
                            //console.log(response.data);
                          console.log(response)
                        },
                        function(error) {
                            console.log(error);
                        }
                    );
            },
            supprimerChatroom: function(id) {
                axios
                    .get(
                        "http://localhost:8888/PHP_SQL/controllers/chatroom_controller.php?action=delete&id=" +
                        id
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
            modifierProfil: function(id, newLogin) {
                axios
                    .get(
                        "http://localhost:8888/PHP_SQL/controllers/users_controller.php?action=modifyUser&id=" +
                        id +
                        "&newName=" +
                        newLogin
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
            supprimerProfil: function(id) {
                axios
                    .get(
                        "http://localhost:8888/PHP_SQL/controllers/users_controller.php?action=delete&id=" +
                        id
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
    color: #fff !important;
    padding: .5em 1.5rem !important;
    background-color: #288EEA !important;
    font-weight: bold !important;
    border-radius: 4px !important;
  }
  h2 {
    font-weight: bold !important;
  }

  button {
    border: 1px solid #288EEA !important;
    color: #288EEA !important;
  }

</style>
