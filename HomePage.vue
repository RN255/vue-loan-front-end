<template>
  <main>
    <section id="banner">
      <img id="logo" src="../assets/logo.png" alt="logo" />
    </section>

    <section id="apply">
      <h1>Apply for a loan now &#x1F44D;</h1>

      <!-- choose a loan value -->

      <form @submit.prevent="addTodo">
        <label>loan amount</label>
        <input v-model="newTodo" placeholder="£" />
        <label>Loan term (months)</label>

        <div class="LoanTermRadio">
          <input
            v-model="newMonths"
            type="radio"
            id="12"
            name="loanTerm"
            value="12"
          />
          <label for="12">12</label>
          <input
            v-model="newMonths"
            type="radio"
            id="18"
            name="loanTerm"
            value="18"
          />
          <label for="18">18</label>
          <input
            v-model="newMonths"
            type="radio"
            id="24"
            name="loanTerm"
            value="24"
          />
          <label for="24">24</label>
        </div>

        <br />
        <button id="submit">Submit</button>
      </form>

      <section id="loanHist">
        <h2>Your loan history</h2>
        <ul>
          <li v-for="todo in filteredTodos" :key="todo.id">
            <input type="checkbox" v-model="todo.done" />
            <p :class="{ done: todo.done }">
              {{ todo.text }} ({{ todo.months }} month term)
            </p>
            <button @click="removeTodo(todo)">delete</button>
          </li>
        </ul>
        <button @click="hideCompleted = !hideCompleted">
          {{ hideCompleted ? "Show all" : "Hide repaid" }}
        </button>
      </section>
    </section>
  </main>
</template>

<script>
//id for our list
let id = 0;

export default {
  name: "HomePage",
  props: {
    msg: String,
  },

  data() {
    return {
      message: "Hello World!",
      subMessage: "welcome to the real world",
      counter: {
        count: 0,
      },
      titleClass: "title",
      text: "",
      toggleValue: true,
      //our list
      newTodo: "",
      hideCompleted: false,
      todos: [
        { id: id++, text: "Learn HTML", done: true, months: null },
        { id: id++, text: "Learn JavaScript", done: true, months: null },
        { id: id++, text: "Learn Vue", done: false, months: null },
      ],
    };
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos;
    },
  },
  methods: {
    increment() {
      this.counter.count++;
    },
    deleteCount() {
      this.counter.count = 0;
    },
    changeClasstitle() {
      if (this.titleClass == "title") {
        this.titleClass = "titleGreen";
      } else {
        this.titleClass = "title";
      }
    },
    toggle() {
      this.toggleValue = !this.toggleValue;
    },
    //add to list
    addTodo() {
      this.todos.push({
        id: id++,
        text: this.newTodo,
        done: false,
        months: this.newMonths,
      });
      this.newTodo = "";
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo);
    },
  },
  //data accessed after component is mounted - lifecycle hook
  mounted() {
    this.$refs.p.textContent = "mounted!";
  },

  // the new
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700;900&display=swap");

* {
  font-family: "Montserrat", sans-serif;
  margin: 0;
  padding: 0;
}

#logo {
  width: 150px;
  border-radius: 50%;
  padding: 25px;
}

#banner {
  color: #ffffff;
  width: 200px;
  height: 100vh;
  position: fixed;
  background: transparent linear-gradient(162deg, #3718b2 0%, #cd33a4 100%);
}

/* main section */

#apply {
  padding-left: 200px;
  width: 400px;
  margin: auto;
  padding-top: 10vh;
}

#apply h1 {
  font-size: 24px;
  font-weight: bold;
  color: #212121;
}

#apply label {
  display: inline-block;
  margin-top: 15px;
  font-size: 14px;
  font-weight: normal;
  color: #6e6e6e;
}

#apply form {
  padding-top: 15px;
  width: 100%;
}

#apply form input {
  font-size: 20px;
  padding: 8px;
  margin-top: 10px;
  margin-bottom: 15px;
  font-weight: bold;
  border: 1px solid #cbcbcb;
  border-radius: 3px;
  width: 93%;
}

#apply input::placeholder {
  color: black;
}

/* radio buttons */

.LoanTermRadio input[type="radio"] {
  opacity: 0;
  position: fixed;
}

.LoanTermRadio label {
  text-align: center;
  background-color: rgb(238, 236, 236);
  padding: 10px 0px;
  border: 1px solid #cbcbcb;
  border-radius: 3px;
  width: 31%;
  margin: 0 2px;
}

.LoanTermRadio label:hover {
  background-color: #3718b220;
  transition: 0.25s;
}

.LoanTermRadio input[type="radio"]:checked + label {
  background-color: #3718b240;
}

/* styling for input warnings */

#LoanAmountWarning {
  color: #e3242b;
}

#LoanTermWarning {
  color: #e3242b;
}

/* submit button */

#apply #submit {
  margin-top: 10px;
  color: #ffffff;
  font-weight: bold;
  background: #7600ff;
  width: 100%;
  padding: 10px 0px;
  border: none;
  border-radius: 3px;
}

/* loan history area */

#loanHist {
  margin-top: 5vh;
}

#loanHist ul {
  margin-top: 3vh;
}

#loanHist li {
  list-style: none;
  margin: 3% 0;
  display: flex;
}

#loanHist li input {
  margin-right: 15px;
}

#loanHist li .done {
  color: #e3242b;
}

#loanHist li button {
  margin-left: auto;
  padding: 1px;
}

@media (max-width: 700px) {
  #logo {
    width: 40px;
    border-radius: 50%;
    padding: 5px 15px;
  }

  #banner {
    width: 100vw;
    height: 50px;
    position: static;
    background: transparent linear-gradient(162deg, #3718b2 0%, #cd33a4 100%);
  }

  #apply {
    padding-left: 0px;
    width: 90%;
    margin: auto;
    padding-top: 5vh;
  }

  #apply h1 {
    font-size: 40px;
  }

  #apply label {
    margin-top: 15px;
    display: inline-block;
  }

  #apply form input {
    width: 96%;
  }

  .LoanTermRadio label {
    width: 99%;
  }

  #apply #submit {
    width: 100%;
    margin-bottom: 50px;
  }

  #loanHist {
    margin-bottom: 50px;
  }
}
</style>
