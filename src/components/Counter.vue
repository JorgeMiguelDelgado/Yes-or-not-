<template>
    <h2>{{ customTitle }}</h2>
    
    <p>{{counter }} = {{squarecounter}}</p>
    
    <div>
        <button @click="incrementar">+1</button>
        <button @click="decrementar">-1</button>
    </div>

</template>

<script>
export default {
    //Propiedades
    props:{
        title: String,
        start: {
            type: Number,
            default: 3,
            validator(value){
                return value >=0
            }
            
        },
    },
    data()
    {
        return{
            counter: this.start
        }
    },
    methods:{
        getSquarevalue()
        {
            return this.counter * this.counter
        },
        incrementar()
        {
            
            this.counter++
            
        },
        decrementar()
        {
            this.counter--
        }
    },
    computed:{
        squarecounter()
        {
            return this.counter * this.counter
        },
        customTitle()
        {
            return this.title || 'Counter'
        }
        
    }
}
</script>

<style>
    button
    {
        margin: 0 5px;
        background-color: #64bb87;
        border-radius: 5px;
        color: white;
        cursor: pointer;
        border: 1px solid white;
        padding: 5px 15px;
        transition: 0.3s ease-in-out;
        
    }
    button:hover
    {
        background-color: #5aa67b;
        transition: 0.3s ease-in-out;
    }
</style>