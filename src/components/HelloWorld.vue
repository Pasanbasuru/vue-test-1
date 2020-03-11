<template>
  <div class="hello">
    <button v-on:click="notifyMe()">Notify Me</button>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  public notifyMe() {
    if (!window.Notification) {
      console.log("Browser does not support notifications.");
    } else {
      // check if permission is already granted
      if (Notification.permission === "granted") {
        // show notification here
        var notify = new Notification("Qumatic", {
          body: "How are you doing?",
          icon:
            "https://lh3.googleusercontent.com/bcHo5Ur4PVsdFyAjJ0fKFkpVmUtRDQGAYo7cqo1fV5t15VuJDK6bnuSnMzjGPx477KYZ"
        });
      } else {
        // request permission from user
        Notification.requestPermission()
          .then(function(p) {
            if (p === "granted") {
              // show notification here
              var notify = new Notification("Qumatic", {
                body: "How are you doing?",
                icon:
                  "https://lh3.googleusercontent.com/bcHo5Ur4PVsdFyAjJ0fKFkpVmUtRDQGAYo7cqo1fV5t15VuJDK6bnuSnMzjGPx477KYZ"
              });
            } else {
              console.log("User blocked notifications.");
            }
          })
          .catch(function(err) {
            console.error(err);
          });
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
  color: #42b983;
}
</style>
