<template>
    <div id="pokemon">
         <div class="card">
            <div class="card-image">
                <figure>
                <img :src="currentImg" alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                <div class="media-content">
                    <p class="title is-4">{{num}} - {{name | upper}}</p>
                    <p class="subtitle is-6">{{pokemon.type}}</p>
                </div>
                </div>

                <div class="content">
               <button class="button is-medium is-fullwidth" @click="changeSprite">Mudar Sprite</button>
                </div>
            </div>
            </div>
    </div>
 
</template>

<script>
import axios from "axios";

export default {

data(){
    return{
        isFront:true,
        currentImg:"",
        pokemon: {
            type:"",
            front:"",
            back:"",
        }
    }
},

    created: function(){
        axios.get(this.url).then((data) =>{
            this.pokemon.type = data.data.types[0].type.name;
            this.pokemon.front = data.data.sprites.front_default;
            this.pokemon.back = data.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
            
        })
    },

    props:{
        num:Number,
        name: String,
        url: String,
    },
    filters:{
        upper:function(value){
            var newName = value[0].toUpperCase() + value.slice(1);
            return newName;
        }
    },
    methods:{
        changeSprite:function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }else{
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>


<style>

#pokemon{
    padding:2%;
}

</style>