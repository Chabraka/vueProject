<template>

    
    <div v-show="gridView" class="game-card">
        <router-link :to="'/game/' + id" class="router-link-no-style"> 
            <img class="game-thumbnail" :src="thumbnail" :alt="title">
            <h3> {{ title }} </h3>
        </router-link>
    </div>
    

    <div v-show="!gridView" class="game-list">
        <div class="image_like">
            <img :src="thumbnail" :alt="title">
            <div class="like" :class="{ 'anim-like': isLiked }" @click="onIsLikedChanged"></div>
            <router-link :to="'/game/' + id" class="router-link-no-style">
                <div class="plus"><i class="fa-solid fa-plus fa-xl"></i></div>
            </router-link>
            
        </div>
        

        <div>
            <h3> {{ title }} </h3>
            <p> {{ short_description }} </p>
            <div class="details-game">
                <p> {{ genre }} </p>
                <p> {{ platform }} </p>
            </div>
        </div>
    </div>
    

</template>

<script>


export default {
    name : 'GameCard',

    props : {
        id : Number,
        title : String,
        thumbnail : String,
        short_description : String,
        genre: String,
        platform: String,
        release_date: Date,

        isLiked: {
            type: Boolean,
            default: false
        },

        gridView: Boolean,
       
    }, 

    emits: ["toggleLike"],

    methods: {

        

        onIsLikedChanged() {
            console.log("Emit Like: " + this.id);
            console.log("isLike: " + this.isLiked);
            this.$emit('toggleLike', this.id);
        },
           
	
    },
 
}

</script>

<style scoped>

    @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@600&display=swap');
    .game-card{    
        width:20rem;
        text-align: center;
        box-shadow: 0.1rem .2rem .4rem rgba(13, 230, 219, 0.295);
        background:#fff;
        margin:4rem 2rem;
        background-color: rgb(15, 3, 44);
        color: rgb(162, 245, 245);
        margin :1.3rem;
        transition: all 0.2s ease;
    }

    .game-card:hover{    
        scale: 1.05;
    }

    .game-thumbnail{
        width: 100%;
    }

    h3{
        margin: 0.2rem;
        padding: 1rem;
        font-family: Orbitron ;
    }

    .game-list{    
        display: flex;
        width: 31rem;
        min-height: 8rem;
        text-align: start;
        padding: 1rem;
        margin: 1rem;
        box-shadow: 0.1rem .2rem .4rem rgba(13, 230, 219, 0.295);
        background-color: rgb(15, 3, 44);
        transition: all 0.2s ease;
    }

    .game-list:hover{    
        scale: 1.05;
    }

    .image_like{
        margin-right: 1rem;
        display: flex;
        flex-direction: column;
        align-items: start;
        
    }

    .game-list>div>img{
        width:11rem;
        object-fit: contain;
    }

    .details-game{
        display: flex;
        justify-content: space-between;
    }

    .game-list p{    
        margin: 0.5rem;
        font-weight: 100;
        font-size: 0.8rem;
    }

    .like {
        cursor: pointer;
        height: 100px;
        width: 100px;
        background-image: url(https://abs.twimg.com/a/1446542199/img/t1/web_heart_animation.png);
        position: absolute;
        transform: translate(-40%, 75%);
    }
    .anim-like {
        animation-name: anim-like;
        animation-duration: 0.8s;
        animation-timing-function: steps(28); 
        background-position: right;
    }

    @keyframes anim-like {
        from{background-position: left;}
        to{background-position: right;}
    }

    .plus{
        cursor: pointer;
        position: absolute;
        transform: translate(130%, 35%);
        padding:0.3rem;
        border: 1px solid #2eb7eb;
        border-radius: 30px;
    }

    .plus:hover{
        color: #2eb7eb;
    }

    .router-link-no-style {
        color: inherit;
        text-decoration: none;
    }
   

</style>

