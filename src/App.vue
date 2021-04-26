<template>
  <div class="container-app">

        <div class="container-quiz">
          <div class="header-quiz">
            <h1>Quiz App</h1>
          </div>
         
          <div class="box" v-for="(question,index) in questions.slice(a, b)" :key="index" v-show="quiz">
              
              <div class="box-question">
                <h2>Question {{b}}/{{questions.length}}</h2>
                <p>{{question.question}}</p>
              </div>
              <div class="box-propositions">
                <ul>
                  <li v-for="(proposition,index) in question.propositions" :key="index" class="li" @click="selected(proposition,index)" :class=" correct ? check(proposition) : ''">
                    {{proposition.answer}} </li>
                  
                </ul>
              </div>
              
              
          </div>
          <div class="box-score" v-if="score_show">
              
              
              <h2>Your score is</h2>
              <h2>{{score}}/{{questions.length}}</h2>
              <div class="btn-restart">
                  <button @click="restartQuiz">Restart</button>
              </div>
          </div>
          <div class="footer-quiz">
                <div class="box-button">
                    <button  @click="nextQuestion()">Next</button>
                </div>  
                  
                  
                  
          </div>
          
          
            
        </div>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
export default {
  data(){
    return{
      questions:[
        {
          question:"Kako povezujemo JavaScript?",
          propositions:[
            {answer:'<script>',correct:true},
            {answer:'<js>'},
            {answer:'<scripting>',},
            {answer:'<javascript>',}
          ]
        },
    
        {
          question:"Kako izbacujemo alert?",
          propositions:[
            {answer:'msg("Hello World")'},
            {answer:'alertBox("Hello World")'},
            {answer:'alert("Hello World")',correct:true},
            {answer:'msgBox("Hello World")'},
            
            
          ]
          
        },
        {
          question:"Pravilna sintaksa za uslov?",
          propositions:[
            {answer:'if i = 5 then',},
            {answer:'if (i == 5)',correct:true},
            {answer:'if i == 5 then',},
            {answer:'if i = 5',},
            
            
          ]
          
        },
        {
          question:"Koja petlja je tačna?",
          propositions:[
            {answer:'for i = 1 to 5',},
            {answer:'for (i <= 5; i++)'},
            {answer:'for (i = 0; i <= 5)'},
            {answer:'for (i = 0; i <= 5; i++)',correct:true},
            
          ]
          
        },
        {
          question:"Kako dodati komentar?",
          propositions:[
            {answer:"Komentar"},
            {answer:'//Komentar',correct:true},
            {answer:'<!--Komentar-->'},
            {answer:'*Komentar'},
            
          ]
          
        }
      ],
      a:0,
      b:1,
      next:true,
      score_show:false,
      quiz:true,
      score:0,
      correct:false,
      
    }
  },
  name: 'App',
  components: {
    //HelloWorld
  },
  computed:{
      
  },
  methods:{
    
    selected(e){
      this.correct = true;
      this.next = false;
      if (e.correct) {
        this.score++;
      }
    },
    check(proposition){
        if (proposition.correct) {
          return 'correct'
        }else{
          return 'incorrect' 
        }
    },
    nextQuestion(){
      if (this.next) {
        return;
      }
      if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = false;    
      }
      else{
        this.a++;
        this.b++;
        this.correct = false;
        this.next = true;
        
      }
      
    },
  
    
    restartQuiz(){
      
      Object.assign(this.$data, this.$options.data()); // restart u vue
       
    },
    
  }
}
</script>