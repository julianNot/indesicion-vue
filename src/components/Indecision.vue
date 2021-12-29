<template>
  <h1>Indecision App</h1>
  <input v-model="question" type="text" />
  <p>No olvides terminar con '?'</p>
  <h2>{{ question }}</h2>
  <h2>{{ answer }}</h2>
</template>

<script>
export default {
    name: 'Indecision',
    data() {
        return {
            question : "",
            answer : "",
        }

    },
    methods: {
        async getAnswer(){
            this.answer = 'Esperando ...'
            const data = await fetch('https://yesno.wtf/api').then(resp => resp.json()).then(resp => resp)
            console.log(data);
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

<style></style>
