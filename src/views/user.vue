<template>
  <div class="user">
    <link rel="stylesheet" href="https://puteborgne.sexy/_css/normalize.css"/>
    <link rel="stylesheet" href="https://puteborgne.sexy/_css/skeleton.css"/><Chatroom/>
    <h1>User</h1>
    <span>chatrooms où il a participé :</span>
    <p v-for="chatroom in chatrooms">
      <b>chatroom {{chatroom.id}} </b>
    </p>
    <div class="user_msg">
      <span>Messages écrits :</span>
      <p v-for="message in messages">
        <b>chatroom {{message.chatroom_id}}</b>
        : {{message.content}}
      </p>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import HelloWorld from "@/components/HelloWorld.vue";
export default {
  name: "user",
  components: {
    HelloWorld
  },
  data() {
    return {
      message: "",
      msgDelete: "",
      msgEdit: "",

      chatrooms: [],
      messages: []
    };
  },
  mounted: function() {
    console.log("USER ID : ", this.$route.query);
    axios
      .get(
        "http://localhost:8888/PHP_SQL/controllers/chatroom_controller.php?action=getMessagesOfUser&userId=" +
          this.$route.query.userId
      )
      .then(
        response => {
          this.messages = response.data;
        },
        function(error) {
          console.log(error);
        }
      );

    axios
      .get(
        "http://localhost:8888/PHP_SQL/controllers/chatroom_controller.php?action=getChatroomsOfUser&userId=" +
          this.$route.query.userId
      )
      .then(
        response => {
          this.chatrooms = response.data;
        },
        function(error) {
          console.log(error);
        }
      );


  }
};
</script>
<style>
  h1 {
    font-weight: bold !important;
  }
</style>