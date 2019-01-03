<template>
  <div class="quest">
    <div class="lines">
      <h3>My view of me</h3>
      <p>This part measures the extent to which you have traits to make an employee great.</p>

      <br>
      <p>Scoring:</p>
      <p>1) No this is not me</p>
      <p>2) Not Quite Me</p>
      <p>3) Yes this is me</p>
    </div>
    <!-- <div class="borders">
          <div v-bind:class="{ color1: this.score1 == '' && this.attempt != 0 }">
            <h4>1.</h4>
            {{questions.questions[0]}}
          </div>

          <input id="sc1" type="radio" v-model="score1" name="score" value="1" required>
          <label for="sc1">1</label>

          <input id="sc2" type="radio" v-model="score1" name="score" value="2">
          <label for="sc2">2</label>

          <input id="sc3" type="radio" v-model="score1" name="score" value="3">
          <label for="sc3">3</label>
        </div>
        <div class="borders">
          <div v-bind:class="{ color1: this.score2 == '' && this.attempt != 0 }">
            <h4>2.</h4>
            {{questions.questions[1]}}
          </div>

          <input id="sc21" type="radio" v-model="score2" name="score2" value="1" required>
          <label for="sc21">1</label>
          <input id="sc23" type="radio" v-model="score2" name="score2" value="2">
          <label for="sc23">2</label>
          <input id="sc22" type="radio" v-model="score2" name="score2" value="3">
          <label for="sc22">3</label>
        </div>
        <div class="borders">
          <div v-bind:class="{ color1: this.score3 == '' && this.attempt != 0 }">
            <h4>3.</h4>
            {{questions.questions[2]}}
          </div>

          <input id="sc31" type="radio" v-model="score3" name="score3" value="1" required>
          <label for="sc31">1</label>
          <input id="sc32" type="radio" v-model="score3" name="score3" value="2">
          <label for="sc32">2</label>
          <input id="sc33" type="radio" v-model="score3" name="score3" value="3">
          <label for="sc33">3</label>
        </div>
        <div class="borders">
          <div v-bind:class="{ color1: this.score4 == '' && this.attempt != 0 }">
            <h4>4.</h4>
            {{questions.questions[3]}}
          </div>

          <input id="sc41" type="radio" v-model="score4" name="score4" value="1" required>
          <label for="sc41">1</label>

          <input id="sc42" type="radio" v-model="score4" name="score4" value="2">
          <label for="sc42">2</label>

          <input id="sc43" type="radio" v-model="score4" name="score4" value="3">
          <label for="sc44">3</label>
        </div>
        <div class="borders">
          <div v-bind:class="{ color1: this.score5 == '' && this.attempt != 0 }">
            <h4>5.</h4>
            {{questions.questions[4]}}
          </div>

          <input id="sc51" type="radio" v-model="score5" name="score5" value="1" required>
          <label for="sc51">1</label>
          <input id="sc52" type="radio" v-model="score5" name="score5" value="2">
          <label for="sc52">2</label>
          <input id="sc53" type="radio" v-model="score5" name="score5" value="3">
          <label for="sc53">3</label>
    </div>-->
    <div>
      <form @submit.prevent="validateForm">
        <ul v-for="(list, index) in questions.questions" :key="index">
          <li>
            <div>{{index + 1}}</div>
            <span v-bind:class="{ color1:  score[index] == '' && this.attempt != 0 }">{{list}}</span>
          </li>
          <input id="sc1" type="radio" v-model="score[index]" :name="'score' + index" value="1">
          <label for="sc1">1</label>

          <input id="sc2" type="radio" v-model="score[index]" :name="'score' + index" value="2">
          <label for="sc2">2</label>

          <input id="sc3" type="radio" v-model="score[index]" :name="'score' + index" value="3">
          <label for="sc3">3</label>
        </ul>
        <!-- <router-link v-if="score !== null" to="/successful" tag="button">Submit</router-link> -->
        <input class="start" type="submit">
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Questions",
  data() {
    return {
      score: [],
      attempt: 0,
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
      if (this.score.length != this.questions.questions.length) {
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

<style scoped>
.quest {
  padding: 0px 400px;
  text-align: left;
}
.lines {
  line-height: 0.5;
}
.borders {
  border: 0.5px solid black;
  border-radius: 5px;
  padding: 20px 5px;
  margin-bottom: 20px;
}
.borders input[type="radio"] {
  display: none;
}

.borders label {
  display: inline-block;
  margin: 0px 20px;
  padding: 10px 40px;
  font-family: Arial;
  font-size: 16px;
  border-radius: 4px;
}

.borders label:hover {
  background-color: rgb(238, 153, 153);
}
.borders input[type="radio"]:checked + label {
  background-color: rgb(226, 93, 93);
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
.start {
  background-color: tomato;
  height: 50px;
  width: 80px;
  border-radius: 10px;
  margin-top: 20px;
}
</style>
