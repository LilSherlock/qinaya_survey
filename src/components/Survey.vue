<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      Para conocer tu experiencia nos gustaria que termines este formulario.
    </p>
  </div>

  <div class="surveyContainer" v-for="(question, index) in questions" :key="index">
    <h3 class="surveyTittle">{{ question.question }}</h3>
    <h4 class="surveyDescription">Seleciona una de estas {{ Object.keys(question.options).length }} opciones</h4>
    <div class="checkboxList">
      <div class="checkBox" v-for="(option, index) in question.options" :key="index">
        <input type="radio" name="" id="" :value="option" v-model="question.answers">
        <p>{{ option }}</p>
      </div>
    </div>
  </div>

  <div class="errorContainer">
    <h3>{{ this.errors }}</h3>
  </div>
  <div class="buttonContent" >
      <button class="button" type="submit" @click="validate()"> Enviar </button>
  </div>
  <br>
</template>

<script>
import axios from "axios";
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data() {
    return {
      questions: [
        {
          id: 1,
          question:'Selecciona un resultado de lo que te parece.',
          options: {
            a: 'Una cuca',
            b: 'Pues bien creo',
            c: 'Triste',
            d: 'Sin palabras',
          },
          answers: ''
        },
        {
          id: 2,
          question:'Que te parece nuestro servicio.',
          options: {
            a: 'Si',
            b: 'No'
          },
          answers: ''
        },
      ],
      errors: ''
    }
  },
  methods: {
    check() {
      console.log(this.questions)
    },
    removeError() {
      setTimeout(()=> {
        this.errors = ''
        
      }, 4000)
    },
    validate() {

      if(this.questions[0].answers == '') {
        this.errors = 'Faltan datos por rellenar'
        this.removeError()
        return
      }

      if(this.questions[1].answers == '') {
        this.errors = 'faltan datos por rellenar'
        this.removeError()
        return
      }
      const params = new URLSearchParams();

      let jsonString = JSON.stringify(this.questions);

      params.append('survey', jsonString)
      axios.post('https://qinaya.co/api/survey', params).then((result) => {
        if (result.data.Status == "200") {
          this.errors = 'Formulario enviado con exito!'
          this.removeError()
          return;
        }
      });

    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.surveyContainer {
  /* border: 1px solid black; */
  padding: 20px;
  width: 70%;
  margin: 15px auto;
  box-shadow: rgba(0, 0, 0, 0.3) 0px 0px 0px 3px;
  border-radius: 5px;
}
.surveyTittle {
  text-align: left;
}
.surveyDescription {
  text-align: left;
}

.errorContainer {
  margin: 0px auto;
  color: #CD1E50
}
.button {
    background-color: #CD1E50;
    border: none;
    color: white;
    /* padding: 15px 60px; */
    text-align: center;
    text-decoration: none;
    width: 20%;
    height: 50px;
    display: inline-block;
    font-size: 16px;
    margin: 2px 2px;
    border-radius: 10px;
    cursor: pointer;
    transition: box-shadow 600ms cubic-bezier(.33,.11,.02,.99), transform  600ms cubic-bezier(.33,.11,.02,.99);
}
.button:hover {
    background-color: #000000;
    color: white;
    transform: scale(1)
    translateY(-0.2rem);
}
.button:active {
    background-color: #000000;
    color: white;
    transform: scale(1.1);
}
.checkBox {
  display: flex;
  align-items: baseline;
}


ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
