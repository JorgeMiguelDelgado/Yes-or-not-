<template>
    <img v-if="img" :src="img" alt="bg">
    <div class="bg-dark">
        <div class="indecision-container">
            <input type="text" v-model="question" @keypress.enter="addq" placeholder="¿Cual es tu pregunta ?">
            <p>Recuerda terminar con un signo de interrogacion</p>
            <div v-if="isValidQuestion">
                <h2>{{question || 'Y tu pregunta es ... ?'}}</h2>
                <h1>{{ answer  === 'yes'? 'Si!': 'No!' }}</h1>
            </div>
        </div>
    </div>
    
</template>

<script>
export default {
    data()
    {
        return {
        question: null,
        answer: null,
        img: null,
        isValidQuestion: false,
        
        }
    },
    methods:{
        async getAnswer(){
            this.answer = 'Pensando ...'
            const {answer, image} = await fetch('https://yesno.wtf/api')
            .then(r=> r.json())
            

            this.answer = answer
            this.img = image
        }
    },
    watch:{
        question(value, oldValue)
        {
            this.isValidQuestion = false
            this.img=null
            if(!value.includes('?')) return
            this.isValidQuestion = true
            
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