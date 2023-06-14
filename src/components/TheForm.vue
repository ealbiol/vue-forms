<template>
  <!--submit prevent to prevent default refresh behaviour.-->
  <form @submit.prevent="submitForm">
    <!--//CSS class invalid will be applied if userNameValidity equals 'invalid'.-->
    <div
      class="form-control"
      :class="{ invalid: userNameValidity === 'invalid' }"
    >
      <label for="user-name">Your Name</label>
      <input
        v-model.trim="userName"
        id="user-name"
        name="user-name"
        type="text"
        @blur="validateInput(userName)"
      />
      <!--Shown when invalid input in blur event.-->
      <p v-if="userNameValidity === 'invalid'">Please enter a valid name.</p>
    </div>
    <!--v-model in INPUT:-->
    <div class="form-control">
      <label for="age">Your Age (Years)</label>
      <input v-model="userAge" id="age" name="age" type="number" />
    </div>
    <!--v-model in DROPWDOWN:-->
    <div class="form-control">
      <label for="referrer">How did you hear about us?</label>
      <select v-model="referrer" id="referrer" name="referrer">
        <option value="google">Google</option>
        <option value="wom">Word of mouth</option>
        <option value="newspaper">Newspaper</option>
      </select>
    </div>
    <!--v-model in CHECKBOXES:-->
    <!--It needs an empty array as initial property and attribute value with different value in each checkbox.Example: value="news"-->
    <div class="form-control">
      <h2>What are you interested in?</h2>
      <div>
        <input
          v-model="interest"
          id="interest-news"
          name="interest"
          type="checkbox"
          value="news"
        />
        <label for="interest-news">News</label>
      </div>
      <div>
        <input
          v-model="interest"
          id="interest-tutorials"
          name="interest"
          type="checkbox"
          value="tutorials"
        />
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input
          v-model="interest"
          id="interest-nothing"
          name="interest"
          type="checkbox"
          value="nothing"
        />
        <label for="interest-nothing">Nothing</label>
      </div>
    </div>
    <div class="form-control">
      <!--v-model in RADIO BUTTONS:-->
      <h2>How do you learn?</h2>
      <div>
        <input
          v-model="how"
          value="video"
          id="how-video"
          name="how"
          type="radio"
        />
        <label for="how-video">Video Courses</label>
      </div>
      <div>
        <input
          v-model="how"
          value="blogs"
          id="how-blogs"
          name="how"
          type="radio"
        />
        <label for="how-blogs">Blogs</label>
      </div>
      <div>
        <input
          v-model="how"
          value="other"
          id="how-other"
          name="how"
          type="radio"
        />
        <label for="how-other">Other</label>
      </div>
    </div>
    <div>
      <div class="form-control">
        <RatingControl v-model="rating" />
      </div>
      <!--v-model SINGLE CHECKBOX: When clicking on checkbox it will be the property confirm which was false becomes true.-->
      <div class="form-control">
        <input
          v-model="confirm"
          type="checkbox"
          id="confirm-terms"
          name="confirm-terms"
        />
        <label for="confirm-terms">Agree to terms of use?</label>
      </div>
      <!--No need for button event since any button inside form triggers submit.-->
      <button>Save Data</button>
    </div>
  </form>
</template>
<script>
import RatingControl from './RatingControl.vue';
export default {
  components: {
    RatingControl,
  },
  data() {
    return {
      userName: '',
      userAge: null,
      referrer: 'google', // initial value as in value in <option>: value="google"
      interest: [], // Empty array due to multiple options
      how: null,
      confirm: false,
      userNameValidity: 'pending',
      rating: null,
    };
  },
  methods: {
    submitForm() {
      console.log('userName:', this.userName);
      this.userName = '';
      console.log('userAge:', this.userAge);
      this.userAge = '';
      console.log('referrer', this.referrer);
      this.referrer = '';
      console.log('interest', this.interest);
      this.interest = [];
      console.log('how', this.how);
      this.how = '';
      console.log('confirm', this.confirm);
      this.confirm = false;
      console.log(this.rating);
      this.rating = '';
    },
    validateInput() {
      console.log('Element blurred', this.userName);
      if (this.userName === '') {
        this.userNameValidity = 'invalid';
      } else {
        this.userNameValidity = 'valid';
      }
    },
  },
  watch: {
    //userName(newUserName) {
    //  console.log('userName:', newUserName);
    //},
  },
};
</script>
<style scoped>
form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #ffffff;
}

.form-control {
  margin: 0.5rem 0;
}

.form-control.invalid input {
  border-color: red;
}

.form-control.invalid label {
  color: red;
}

label {
  font-weight: bold;
}

h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}

input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  padding: 0.75rem 2rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}
</style>
