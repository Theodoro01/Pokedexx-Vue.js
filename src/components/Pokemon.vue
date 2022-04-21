<template>
    <div id="pokemon">
  

        <div class="card">
            <div class="card-image">
                <figure>
                    <img :src="currentImg">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
  
                    <div class="media-content">
                        <p class="title is-4">{{num}} - {{name}}</p>
                        <p class="subtitle is-6">{{pokemon.type}}</p>
                    </div>
                </div>

                <div class="content">
                    <button class="button is-medium" @click="mudarSprite">Sprite</button>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
import axios from 'axios';

export default({

    created: function(){
        axios.get(this.url).then((response)=>{
            this.pokemon.type = response.data.types[0].type.name; 
            this.pokemon.front = response.data.sprites.front_default;
            this.pokemon.back = response.data.sprites.back_default; 
            this.currentImg = this.pokemon.front;
        }).catch((err)=>{
            console.log(err)
        });
    }, 

    data(){
        return {
            isfront: true,
            currentImg: '',
            pokemon: {
                type: '',
                front: '',
                back: '',
            }
        }
    },

    props: {
        num: Number,
        name: String,
        url: String
    },
    methods: {

        mudarSprite(){
            if(this.isfront){
                this.isfront = false;
                this.currentImg = this.pokemon.back;
            }else{
                this.isfront = true;
                this.currentImg = this.pokemon.front;
            }
        },
        computed:{
            upper: function(value){
                var newName = value[0].toUpperCase() + value.slice([1]);
                return newName;
            }
        }
    }
});

</script>

<style scoped>

    #pokemon {
        margin-top: 2%;
    }

</style>
