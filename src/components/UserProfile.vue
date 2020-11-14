<template>

 <div class="user-profile__wrapper">
   <div class="user-profile__data">

          @{{user.name}} - {{FullName}}
      <strong>Followers</strong>{{follower}}
      <div class="user-profile__admin-badge" v-if="user.isAdmin">
          Admin
      </div>
      <button class="user-profile__button" @click="addFollowers"> follow</button>
      <br>

       <form class="user-profile__create-form" @submit.prevent="createNewTweet"> 
            <label  for="newTweet"><strong>New Tweet</strong></label>
            <textarea id="newTweet" v-model="newTweetContent" rows="4"/>

            <div>
              <label  for="newTweet"><strong> Tweet Option</strong></label>
              <select id="tweetId" v-model="selectedTweetType">
                <option :value="option.value" v-for="(option) in options" :key="option.value">
                  {{option.name}}
                </option>
              </select>

            </div>
            <button>Tweet</button>

        </form>
   </div>
 


          <div class="user-profile__tweets-wrapper">
              <Tweet v-for="tweet in user.tweets "
              :key="tweet.id"
              :userName="user.name" 
              :tweet="tweet" 
              @favourite="togglefavourite"/>
          </div>

          <div class="online__users">
            <div>
              <p>Online Users</p>

            </div>


          </div>

       
</div>
  
  
</template>


<script>
import Tweet from "./Tweet"
export default {
    name:'UserProfile',
    components:{
       Tweet 

    },
     data(){
    return{
      newTweetContent:'',
      selectedTweetType:'instant',
      options:[
        {value:"draft",name:"Draft"},
        {value:"instant",name:"Instant"}
      ],
      follower:0,
      user:{
        id:1,
        email:'bwangocho@gmail.com',
        isAdmin:true,
        lastName:'Wangocho',
        name:'Brian',
        tweets:[
            {id:1,content:"awsome app",status:"1",type:"instant"},
              {id:2,content:"awsome app2",status:"1",type:"instant"},
                {id:3,content:"awsome app4",status:"0",type:"instant"},
                  {id:4,content:"awsome app5",status:"0",type:"instant"},
                    {id:5,content:"awsome app6",status:"1",type:"instant"}
        ]
      }
    }
  },
  computed:{
    FullName(){
      return `${this.user.name}${this.user.lastName}`; 
    }
  },
  watch:{
    follower(newfollowercount,oldfollowercount){
      if(oldfollowercount<newfollowercount){
        console.log(`${this.user.name} has gained a follower `);
      }

    }

  },
  methods:{
    addFollowers(){
      this.follower++;
    },
    togglefavourite(id){
        console.log(`${id}`)
    },
    createNewTweet(){
      if(this.newTweetContent && this.selectedTweetType !='draft'){
        ///unshift  basically means put this at the start of the list in js
        ///push puts it at the end of the list
          this.user.tweets.unshift(
            {
              id:this.user.tweets.length+1,
              content:this.newTweetContent,
              status:'1',
              type:this.selectedTweetType

            }
          )
          this.newTweetContent='';
      }
    }
  },
  mounted(){
    // works only when a component is created
    this.addFollowers();
  }

}
</script>

<style lang="scss" scoped>
.user-profile__wrapper{
display: flex;
justify-content: space-evenly;
  flex-wrap: wrap;

}
.user-profile__data{
   box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
    border-radius: 5px;
    padding: 30px;

    .user-profile__admin-badge{
      background-color: blue;
    }
    .user-profile__button{
      background-color: blue;
      width: 50%;
      border-radius: 40%;
    }
  
  .user-profile__create-form{
   box-sizing: border-box;
   margin: 5px;
   flex-direction: column;
   

  }


}

.user-profile__tweets-wrapper{
  width: 50%;
}
.online__users{
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  widows: 40%;
}
</style>