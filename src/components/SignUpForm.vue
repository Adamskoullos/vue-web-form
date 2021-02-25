<template>
    <form @submit.prevent="handleSubmit">
        <label>Email:</label>
        <input type="email" required v-model="email">
        <label>Password:</label>
        <input type="password" required v-model="password">
        <div v-if="passwordError" class="error">{{ passwordError }}</div>
        <label>Role:</label>
        <select v-model="role">
            <option value="Front-End">Front-End</option>
            <option value="Back-End">Back-End</option>
            <option value="Full-Stack">Full-Stack</option>
        </select>
        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label>Accept terms and conditions</label>
        </div>

        <label>Skills:</label>
        <input type="text" v-model="tempSkills" @keyup="addSkill">
        <div v-for="skill in skills" :key="skill" class="pill" @click="deleteSkill">
            {{ skill }}
        </div>
        <div class="submit">
            <button>Create an account</button>
        </div>
    </form>
    <h4>Email: {{ email }}</h4>
    <h4>Password: {{ password }}</h4>
    <h4>Role: {{ role }}</h4>
    <h5>Terms accepted: {{ terms }}</h5>
</template>

<script>
export default {
    data(){
        return{
            email: '',
            password: '',
            role: '',
            terms: false,
            tempSkills: '',
            skills: [],
            passwordError: ''
        }
    },
    methods:{
        addSkill(e){
         if(e.key === ',' || e.key === ' ' && this.tempSkills){
             if(!this.skills.includes(this.tempSkills)){
                 this.skills.push(this.tempSkills.slice(0,this.tempSkills.length-1))
             }
             this.tempSkills = ''
         }       
        },
        deleteSkill(e){
            // console.log(e.target.textContent) Grab skill
            // remove skill from skills array
            this.skills.splice(this.skills.indexOf(e.target.textContent),1)
        },
        handleSubmit(){
            // validate password
            this.passwordError = this.password.length > 5 ? '':'Password must be at least 6 characters'
            if(!this.passwordError){
                console.log(`email: ${this.email}`)
                console.log(`password: ${this.password}`)
                console.log(`role: ${this.role}`)
                console.log(`skills: ${this.skills}`)
                console.log(`terms accepted: ${this.terms}`)
            }
        }
    }
}
</script>

<style>
    form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label {
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
  button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
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