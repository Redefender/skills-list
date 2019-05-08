<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input type="text" placeholder="Enter a skill you have..." v-model="skill" v-validate="'min:5'" name="skill"/>
        <p class="alert" v-if="errors.has('skill')"> {{errors.first('skill')}}</p>
      </form>
      <ul>
        <li v-for="(data, index) in skills" :key='index'>{{index }}. {{data.skill}}</li>
      </ul>

      <p v-if="skills.length >= 1">You have more than one skill</p>
      <p v-else>You have less than or equal to one skill</p>
    </div>
    <p>These are the skills you posess</p>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data(){
    return {
      skill: '',
      skills: [
        {"skill": "Vue.js"},
        {"skill": "Frontend Developer"}
      ],

    }
  },
methods:{
  addSkill(){
    this.$validator.validateAll().then((result) => {
      if(result){
        this.skills.push({'skill' : this.skill});
        skill = '';
      } else{
        console.log('not valid')
      }
    });

  
  }
}



}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
   .holder {
    background: #fff;
  }

  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }
  input{
    width: calc(100% - 40px);
    border: 0;
    padding:20px;
    font-size:1.3em;
    background-color: #323333;
    columns: #687f7f;;
  }
</style>
