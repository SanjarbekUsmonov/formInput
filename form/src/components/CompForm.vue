<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <label>Email</label>
      <input type="email" required v-model="email">

      <label>Password</label>
      <input type="password" required v-model="password">

      <div v-if="paswwordEror" class="eror"> {{paswwordEror}}</div>

      <label>Role:</label>
      <select v-model="role">
        <option value="developer">Web deleloper</option>
        <option value="designer">Web designer</option>
      </select>

        <label>Skills:</label>
        <input type="text" v-model="tempSkills" @keyup.alt="addSkill">
        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{skill}}</span>
        </div>

      <div class="terms">
        <input type="checkbox" v-model="terms" required>
        <label>Accep terms and condition</label>
      </div>

       <div class="submit">
        <button>Create and Acound</button>
       </div>
    </form>
    <p>Email: {{email}}</p>
    <p>Password: {{password}}</p>
    <p>Role: {{role}}</p>
    <p>Terms accepted: {{terms}}</p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      email:'mario',
      password:'',
      role:'designer',
      terms: false,
      tempSkills:'',
      skills:[],
      paswwordEror:''

    }
  },
  methods: {
    addSkill(e){
     if(e.key === ',' && this. tempSkills){
     if(!this.skills.includes(this.tempSkills )){
       this.skills.push(this.tempSkills)
      }
     this.tempSkills = ''
     }
    }
  },
  deleteSkill(skill){
    this.skills = this.skills. filter((item)=>{
      return skill !== item
    })
  },
  handleSubmit(){
    this.paswwordEror = this.password.length > 5 ? '': 'Password must be at least 6 chars long'
  }
}
</script>

<style>
form{
  max-width: 420px;
  margin: 30px auto;
  background: rgb(219, 218, 218);
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
input,select{
display: block;
padding: 10px 6px;
width: 100%;
box-sizing: border-box;
border: none;
border-bottom: 1px solid #ddd;
color: #555;
}
input[type="checkbox"]{
 display: inline-block;
width: 16px;
margin: 0 10px 0 0;
position: relative;
top: 2px;
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
 button{
  background: blue;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
 }
 .submit{
  text-align: center;
 }
 button:hover{
  /* box-shadow: 2px 2px 3px 3px blue; */
  opacity: 0.6;
  cursor: pointer;
 }
 .eror{
  color: red;
 }
</style>
