<template>
  <div>
    <h1>My view of me</h1>
    <p>This part says alot about you.</p>

    <br>
    <p>Scoring:</p>
    <p>1 - No this is not me</p>
    <p>2 - Not Quite Me</p>
    <p>3 - Yes this is me</p>

    <div>
      <form>
        <div>
          <div v-bind:class="{ color1: this.score1 == '' && this.attempt != 0 }">
            <span>1.</span>
            {{questions.questions[0]}}
          </div>
          <label>
            <input type="radio" v-model="score1" name="score" value="1" required>
            1
          </label>
          <label>
            <input type="radio" v-model="score1" name="score" value="2">
            2
          </label>
          <label>
            <input type="radio" v-model="score1" name="score" value="3">
            3
          </label>
        </div>
        <div>
          <div v-bind:class="{ color1: this.score2 == '' && this.attempt != 0 }">
            <span>2.</span>
            {{questions.questions[1]}}
          </div>
          <label>
            <input type="radio" v-model="score2" name="score2" value="1" required>
            1
          </label>
          <label>
            <input type="radio" v-model="score2" name="score2" value="2">
            2
          </label>
          <label>
            <input type="radio" v-model="score2" name="score2" value="3">
            3
          </label>
        </div>
        <div>
          <div v-bind:class="{ color1: this.score3 == '' && this.attempt != 0 }">
            <span>3.</span>
            {{questions.questions[2]}}
          </div>
          <label>
            <input type="radio" v-model="score3" name="score3" value="1" required>
            1
          </label>
          <label>
            <input type="radio" v-model="score3" name="score3" value="2">
            2
          </label>
          <label>
            <input type="radio" v-model="score3" name="score3" value="3">
            3
          </label>
        </div>
        <div>
          <div v-bind:class="{ color1: this.score4 == '' && this.attempt != 0 }">
            <span>4.</span>
            {{questions.questions[3]}}
          </div>
          <label>
            <input type="radio" v-model="score4" name="score4" value="1" required>
            1
          </label>
          <label>
            <input type="radio" v-model="score4" name="score4" value="2">
            2
          </label>
          <label>
            <input type="radio" v-model="score4" name="score4" value="3">
            3
          </label>
        </div>
        <div>
          <div v-bind:class="{ color1: this.score5 == '' && this.attempt != 0 }">
            <span>5.</span>
            {{questions.questions[4]}}
          </div>
          <label>
            <input type="radio" v-model="score5" name="score5" value="1" required>
            1
          </label>
          <label>
            <input type="radio" v-model="score5" name="score5" value="2">
            2
          </label>
          <label>
            <input type="radio" v-model="score5" name="score5" value="3">
            3
          </label>
        </div>
        <!-- <ul v-for="(list, index) in questions.questions" :key="index">
        <li>
          <div>{{index + 1}}</div>
          {{list[0]}}
        </li>
        <label>
          <input type="radio" v-model="score" name="score" value="1">
          1
        </label>
        </ul>-->
        <!-- <router-link v-if="score !== null" to="/successful" tag="button">Submit</router-link> -->
        <input type="submit" @click.prevent="validateForm">
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Questions",
  data() {
    return {
      score1: "",
      attempt: 0,
      score2: "",
      score3: "",
      score4: "",
      score5: "",
      questions: [],
      tok:
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoiMDAwMDAwMDMiLCJpYXQiOjE1MzM2NDQwOTMsImV4cCI6MTU2NTA5MzY5M30.oMv_mQN6mAAmAVrRAozC7Ytk3omAye9P_TQ8Xyg3VOE"
    };
  },
  methods: {
    getQuestions: async function() {
      const res = await fetch("http://test.natterbase.com:3002/questions", {
        method: "GET",
        headers: new Headers({
          "x-access-token": this.tok
        })
      }).then(result => result.json());
      console.log(res);
      this.questions = res;
    },
    validateForm: function() {
      console.log("Runing thissss");
      if (
        this.score1 == "" ||
        this.score2 == "" ||
        this.score3 == "" ||
        this.score4 == "" ||
        this.score5 == ""
      ) {
        this.attempt++;
        alert("Please answer all the questions");
      } else {
        this.$router.push("/successful");
      }
    }
  },
  mounted() {
    this.getQuestions();
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
li {
  list-style: none;
}
.color1 {
  color: red;
}
.color2 {
  color: white;
}
</style>
