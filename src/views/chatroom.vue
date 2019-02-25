<template>
  <div>
    <link rel="stylesheet" href="https://puteborgne.sexy/_css/normalize.css"/>
    <link rel="stylesheet" href="https://puteborgne.sexy/_css/skeleton.css"/><Chatroom/>
    <h1>Chatrooms</h1>

    <div v-for="message in messages">
      <p><b>User {{message.user_id}} </b> : {{message.content}} </p>
      <button v-on:click="supprimerMessage(message.id)">Supprimer</button>
    </div>

    <label>Nouveau message :</label>
    <input name="message" v-model="message" placeholder="texte" type="text">
    
    <button v-on:click="envoyerMessage()">Envoyer</button>
  </div>
</template>
<script>
  import axios from "axios";
  import HelloWorld from "@/components/HelloWorld.vue";
export default {
  name: "chatroom",
  components: {
    HelloWorld
  },
  data() {
    return {
      message: "",
      messages: []
    };
  },
  mounted: function() {
    console.log("CHATROOM ID : ", this.$route.query);
    axios
      .get(
        "http://localhost:8888/PHP_SQL/controllers/chatroom_controller.php?action=getMessagesOfChatroom&chatroomId=" +
          this.$route.query.chatroomId
      )
      .then(
        response => {
          console.log(response.data);
          this.messages = response.data;
        },
        function(error) {
          console.log(error);
        }
      );
  },
  methods: {
    envoyerMessage: function() {
      axios
        .get(
          "http://localhost:8888/PHP_SQL/controllers/chatroom_controller.php?action=addMessage&userId=5&chatroomId=" +
            this.$route.query.chatroomId +
            "&content=" +
            this.message
        )
        .then(
          response => {
            this.users = response.data;
            console.log("users:", this.users);
          },
          function(error) {
            console.log(error);
          }
        );
    },
    supprimerMessage: function(id) {
      axios
              .get(
                      "http://localhost:8888/PHP_SQL/controllers/chatroom_controller.php?action=deleteMessage&id=" +
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
  }
};
</script>

<style>
  p{
    padding: .5em 1em;
    display: inline;
    background: #f2f7f7;
    margin: 1em;
  }
</style>