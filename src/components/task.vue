<template>
  <div>
    <div>
      <b-card bg-variant="light" text-variant="black" :header="datatask.title" class="text-center">
        
        <b-card-text class="text-left">
          <p>Description: {{datatask.description}}</p>
          <p>Point: {{datatask.point}}</p>
          <p>assignedTo: {{datatask.assignedTo}}</p>
        </b-card-text>
        <span v-show="datatask.status!='back-log'" @click="updateStatusToBack(datatask)">
          <img src="https://img.icons8.com/color/38/000000/chevron-left.png" />
        </span>
        <span @click="deleteTask(datatask)">
          <img src="https://img.icons8.com/color/38/000000/trash.png" />
        </span>
        <span v-show="datatask.status!='done'" @click="updateStatus(datatask)">
          <img src="https://img.icons8.com/color/38/000000/chevron-right.png" />
        </span>
      </b-card>
    </div>
  </div>
</template>

<script>
import db from "../../config/firebase";

export default {
  props: ["datatask"],
  data() {
    return {

    };
  },
  methods: {
    updateStatus(task) {
      console.log(task.id, "ini ID");

      if (task.status == "back-log") {
        db.collection("Task")
          .doc(task.id)
          .update({
            status: "todo"
          })
          .then(function() {
            console.log("Document successfully updated!");
          })
          .catch(function(error) {
            // The document probably doesn't exist.
            console.error("Error updating document: ", error);
          });
      } else if (task.status == "todo") {
        db.collection("Task")
          .doc(task.id)
          .update({
            status: "doing"
          })
          .then(function() {
            console.log("Document successfully updated!");
          })
          .catch(function(error) {
            // The document probably doesn't exist.
            console.error("Error updating document: ", error);
          });
      } else if (task.status == "doing") {
        db.collection("Task")
          .doc(task.id)
          .update({
            status: "done"
          })
          .then(function() {
            console.log("Document successfully updated!");
          })
          .catch(function(error) {
            // The document probably doesn't exist.
            console.error("Error updating document: ", error);
          });
      }
    },
    updateStatusToBack(task) {
      if (task.status == "done") {
        db.collection("Task")
          .doc(task.id)
          .update({
            status: "doing"
          })
          .then(function() {
            console.log("Document successfully updated!");
          })
          .catch(function(error) {
            // The document probably doesn't exist.
            console.error("Error updating document: ", error);
          });
      } else if (task.status == "todo") {
        db.collection("Task")
          .doc(task.id)
          .update({
            status: "back-log"
          })
          .then(function() {
            console.log("Document successfully updated!");
          })
          .catch(function(error) {
            // The document probably doesn't exist.
            console.error("Error updating document: ", error);
          });
      } else if (task.status == "doing") {
        db.collection("Task")
          .doc(task.id)
          .update({
            status: "todo"
          })
          .then(function() {
            console.log("Document successfully updated!");
          })
          .catch(function(error) {
            // The document probably doesn't exist.
            console.error("Error updating document: ", error);
          });
      }
    },
    deleteTask(task) {
      db.collection("Task")
        .doc(task.id)
        .delete()
        .then(function() {
          console.log("Document successfully deleted!");
        })
        .catch(function(error) {
          console.error("Error removing document: ", error);
        });
    }
  }
};
</script>

<style>
.text-center {
  margin-bottom: 2rem;
}
</style>
