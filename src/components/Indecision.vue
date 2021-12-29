<template>
    <img :src="image" alt="Git answer">
    <div class="bg-dark"> 
      <h1>Indecision App</h1>
      <div class="indecision-container">
          <input v-model="question" type="text" />
          <p>No olvides terminar con '?'</p>
      </div>
      <div>
          <h2>{{ question }}</h2>
          <h2>{{ answer }}</h2>
      </div>
    </div>

</template>

<script>
export default {
    name: 'Indecision',
    data() {
        return {
            question : "",
            answer : "",
            image : "@/assets/logo.png"
        }

    },
    methods: {
        async getAnswer(){
            this.answer = 'Esperando ...'
            const {answer, image} = await fetch('https://yesno.wtf/api').then(resp => resp.json()).then(resp => resp)
            this.answer = answer
            this.image = image
        }
    },
    watch : {
        question(value){
            if(!value.includes('?')) return

            this.getAnswer()
        }
    },
}

</script>

<style scoped>
    img, .bg-dark {
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
    }

    .bg-dark {
        background-color: rgba(0, 0, 0, 0.4);
    }

    .indecision-container {
        position: relative;
        z-index: 99;
    }
    
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 5px;
        border: none;
    }
    input:focus {
        outline: none;
    }

    p {
        color: white;
        font-size: 20px;
        margin-top: 0px;
    }

    h1, h2 {
        color: white;
    }
    
    h2 {
        margin-top: 150px;
    }

</style>
