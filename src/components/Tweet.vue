<template>
<div class="tweet-item" @click="liketweet(tweet.id)"> 
    <div class="user-profile__tweet">
        <div class="user-profile__user">
             {{userName}}
        </div>
        <div class="user-profile__content">
             {{tweet.content}}
        </div>



    </div>

   
    
</div>
  
</template>

<script>
export default {
    name:'Tweet',
    props:{
        userName:{
            type:String,
            required:true

        },
        tweet:{
            type:Object,
            required:true
        }
    },
    methods:{
        liketweet(id){
            this.$emit('favourite',id)
        }
    }

}
</script>

<style lang="scss" scoped>
.tweet-item{
    padding: 10px;
    background-color:white;
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    border-radius: 5px;
    margin-top: 10px;
    width: 100%;
    box-sizing: border-box;
    transition: all 0.5 ease;

    &:hover{
        transform: scale(1.1,1.1);
    }
}

</style>