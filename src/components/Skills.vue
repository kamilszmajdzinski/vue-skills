<template>

  <div class="hello">
    <h1>Skills</h1>
    <div class="holder">

      <form @submit.prevent = "onSubmit">
        <input 
          type = "text" 
          placeholder="Enter a skill you have.." 
          v-model="skill"
          v-validate = "'min:5'"
          name="skill" />

          <transition name="alert-in">
            <p 
              class="alert"
              v-if="errors.has('skill')">
              {{ errors.first('skill') }}
            </p>
          </transition>

      </form>

      <ul>
        <transition-group name = 'list' enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown" >
          <li v-for = "(data, index) in skills" :key="index" > {{ data.skill }} <i class="fas fa-ban" v-on:click = "removeSkill(index)"></i></li>
        </transition-group>
      </ul>

    </div>
  </div>

</template>


<script>
export default {
  name: 'Skills',
  data(){
    return{
      skill: '',
      skills: [
        {"skill": "react.js"},
        {"skill": "redux"},
        {"skill": "react-router"},
      ]
    }
  },
  methods: {
    onSubmit(){
      this.$validator.validateAll().then((result) => {
        if (result) {
          this.skills.push({ "skill": this.skill })
          this.skill = ''
        }
      })
    },
    removeSkill(index){
      this.skills.splice(index, 1)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.css";

  .holder {
    background: #fff;
  }

  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }

  ul i {
    right: 20px;
    position: absolute;
    transition: 0.5s ease;
  }

  ul i:hover {
    color: red;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
    position: relative;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }

  input {
    width: calc(100% - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323333;
    color: #687F7F;
  }

  .alert{
    background: #fdf2ce;
    font-weight: bold;
    display: inline-block;
    padding: 5px;
    margin-top: -20px;
  }

  .alert-in-enter-active {
    animation: bounce-in .5s;
  }

  .alert-in-leave-active {
    animation: bounce-in .5s reverse;
  }

  @keyframes bounce-in {
    0%{
      transform: scale(0)
    }
    50%{
      transform: scale(1.1)
    }
    100%{
      transform: scale(1)
    }
    
  }

</style>
