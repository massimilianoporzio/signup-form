<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email">

    <label>Password:</label>
    <input type="password" required v-model="password">
    <div class="error" v-if="passwordError.valueOf()">{{passwordError}}</div>

    <label>Role</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div v-for="(skill,index) in skills" :key="index" class="pill">
      <span @click="deleteSkill(skill)">{{skill}}</span>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms">
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>
<!--    <div>-->
<!--      <input type="checkbox" value="shaun" v-model="names">-->
<!--      <label>Shaun</label>-->
<!--    </div>-->
<!--    <div>-->
<!--      <input type="checkbox" value="yoshi" v-model="names">-->
<!--      <label>Yoshi</label>-->
<!--    </div>-->
<!--    <div>-->
<!--      <input type="checkbox" value="mario" v-model="names">-->
<!--      <label>Mario</label>-->
<!--    </div>-->
  </form>
  <p>Email: {{email}}</p>
  <p>Password: {{password}}</p>
  <p>Role: {{role}}</p>
  <p>Terms accepted: {{terms}}</p>
<!--  <p>Names checked: {{names}}</p>-->
</template>

<script setup>
import {ref} from "vue";

const name = "SignupForm"
let email = ref('')
let password = ref('')
let role = ref('designer')
let terms = ref('false')
let names = ref([])
let skills = ref([])
let tempSkill = ref('')

let passwordError = ref('')


function addSkill(e){

  if(e.key === ',' && tempSkill){
    if(!skills.value.includes(tempSkill.value))
    {
      skills.value.push(tempSkill.value)
    }

    tempSkill.value = ''
  }
}

function deleteSkill(skill){
  skills.value = skills.value.filter((s)=>s!==skill)
}

function handleSubmit() {
  //validate password
  console.log("HANDLE SUBMIT")
  passwordError.value = password.value.length > 5 ? '' : 'Password must have at least 6 characters'
}
</script>

<style scoped>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label{
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;

}
input, select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  color: white;
  border-radius: 20px;
}
.submit {
  text-align: center;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>
