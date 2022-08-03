<template>
  <!--  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <h1>{{msg}}</h1> -->
  <link
    rel="stylesheet"
    href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200"
  />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link
    href="https://fonts.googleapis.com/css2?family=Varela+Round&display=swap"
    rel="stylesheet"
  />

  <body>
    <div class="main-box">
      <h3>Task Schenduler</h3>
      <div class="add-task">
        <div class="inputs">
          <span>Tarea:</span>
          <input
            id="taskTitle"
            class="tarea"
            type="text"
            placeholder="Nueva Tarea"
          />
          <span>Duración (m):</span>
          <input id="taskTime" class="duracion" type="number" />
        </div>
        <button @click="addTask">&#43;</button>
      </div>

      <h2 class="h2">Lista de Tareas <span class="material-symbols-outlined list">fact_check</span></h2>

      <div class="table-box">
        <ul id="table">
          <li class="tasks box" v-for="(t, index) in tasks" :key="index">
            <strong>{{ " "+ t.title + "   "}}</strong>  |  {{" " + t.time }} minutos
            <button :key="index" class="remove-button" @click="removeItem">
              &times;
            </button>
          </li>
        </ul>
        <p>
          Tiempo trabajado: <strong style="color:rgb(104, 216, 104)"> 170 </strong> minutos
        </p>
      </div>
    </div>
  </body>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      name: "",
      newTask: { title: " ", time: 0 },
      tasks: [],
    };
  },
  created() {
    this.tasks = JSON.parse(localStorage.getItem("tasks")) || [];
  },
  components: {},
  methods: {
    addTask() {
      const title = document.getElementById("taskTitle").value;
      const time = parseInt(document.getElementById("taskTime").value);
      if (title !== "" && time !== "") {
        this.newTask.title = title;
        this.newTask.time = time;
        this.tasks.push(this.newTask);
        this.newTask = {
          title: "",
          time: 0,
        };
      } else {
        alert("La tarea y el tiempo deben tener un valor");
      }

      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },

    removeItem(index) {
      this.tasks.splice(index, 1);
    },

    computed: {
      totalTime() {
        if (!this.tasks.length) {
          return 0;
        }

        let total = 0;

        this.tasks.forEach((t) => {
          total += parseInt(t.time);
        });

        return total;
      },
    },

    /* removeTask (index) {
      this.tasks.splice(index, 1)
      localStorage.setItem("tasks", JSON.stringify(this.tasks))
    }, */
  },
};
</script>

<style>
* {
  font-family: 'Varela Round', sans-serif;
  color: rgb(68, 68, 68);
}

.duracion {
  width: 50px;
}
.tarea {
  width: 300px;
  margin-left: 5px;
}
.add-task {
  margin: 0 auto;
  background-color: #ccffc7;
  width: max-content;
  padding: 5px;
  display: flex;
  flex-direction: row;
  align-items: center;
  height: 50px;
  gap: 2px;
  justify-content: space-evenly;
  border-radius: 50px;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
}
.add-task button {
  background-color: rgb(104, 216, 104);
  color: rgb(14, 117, 14);
  border: none;
  width: 40px;
  height: 40px;
  font-size: 30px;
  border-radius: 30px;
  margin: 2px;
}
.add-task button:hover {
  background-color: rgb(159, 240, 159);
  transition: 500ms ease;
}
.inputs {
  text-align: center;
}

.inputs > * {
  margin-left: 10px;
  height: 30px;
  border: none;
  border-radius: 10px;
  padding: 2x;
  font-size: 16px;
}
.inputs > * :focus {
  border: none;
}

.remove-button {
  background-color: rgb(250, 166, 166);
  color: rgb(216, 123, 123);
  font-size: 20px;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  margin: 10px;
  border: none;

}

.remove-button:hover {
  background-color: rgb(255, 188, 188);
  transition: 500ms ease;
}
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  min-width: 700px;
  max-width: 1000px;
  margin: 0 auto;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
#table {
  margin: 0 auto;
}
.box {
  margin: 0 auto;
  background: white;
  border-radius: 20px;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
  margin-top: 10px;
  width: 500px;
  height: 35px;
  padding: 10px;
  display: flex;
  align-items: center;
  text-align: center;
}
ul {
  text-decoration: none;
  list-style: none;
  text-align: center;
}

.table-box {
  width: 800px;
  height: 800px;
  border: #ccffc7 2px solid;
  border-radius: 30px;
  margin: 0 auto;
}
h2 {
  text-align: center;
}

h3 {
  color: rgb(159, 240, 159);
  margin-top: 80px;
  text-align: center;
  font-weight: bolder;
}
p {
  text-align: center;
}

/* .main-box {
  width: 1300px;
  height: 100%;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
  margin: 0 auto;
} */
li {
  display: flex;
}
.list{
  margin-top:15px;
  text-align: center;
  font-size: 25px;
}
</style>
