<template>
    <div class="container">
        <div class="content">
            <h1>{{msg}}</h1>
            
            <main>
                <div class="creator">
                    <div class="ajout-form">
                        <input  placeholder="Nouveau participant" v-model="challa" id="newPerson">
                        <button v-on:click="newMember($event, challa)"> Ajouter </button>
                    </div>
                        
                    <div class="list">

                        <h3>Liste des participants</h3>
                        <ul>
                            <li v-for="element in participants" :key="'el-'+element">
                                {{element}}
                                
                            </li>
                        </ul>
                    
                        <button v-on:click="allReset($event)">Reset</button>
                        
                    </div>
                
                    <div class="generator">
                        <label for="groups"> Nombre de groupes : </label> 
                        <input type="number" min="2" placeholder="2" v-model="groups_number" id='groups'>
                        <button v-on:click="goGroup($event, participants, groups_number)"> Generate</button>
                    </div>
                </div>
                <div class="results">
                    <article>
                       
                        <div class="group-lists" v-for="gl in group_lists" :key="'gl'+gl[0]"> 
                            <h3> {{gl[0]}} :</h3> 
                            <ul>
                                <li v-for="el in gl.membres" :key="el"> {{el}}</li>
                            </ul>
                            
                        </div> 
                    </article>
                </div>
            </main>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Creator',
  props: {
    msg: String
  },
  data(){
      return{
          participants: [],
          challa: "",
          groups_number: 0,
          group_lists: [
              {
                name:"",
              membres: []   
              }
          ]
          
          
      }
  },
  mounted(){
      this.participants= [];
      this.participantsCopy= [];
      this.group_lists=[];
  },
  methods: {
     newMember(e, item){
         e.preventDefault();
         console.log(this.challa);
         if (item !== "") {
             this.participants.push(item);
             this.participantsCopy.push(item);
         }
         console.log(this.participants);
        //  this.challa="";
     },
     allReset(e){
         e.preventDefault();
         this.participants = this.participantsCopy;
         this.group_lists= []
     },
     goGroup(e, noms, num){
         e.preventDefault();
        let lefties= (noms.length)%(num);
        let fullies=(noms.length - lefties)/(num)
       
        for (let i=0; i<num;i++){
        let newGroupe= ["groupe n°"+(i+1), []]
        this.group_lists.push(newGroupe)
        console.log(this.group_lists);
        }


        for (let g = 0; g <= num; g++) {
            var element = [];
            if(noms.length>= noms.length-(fullies*g)){
                element = [];
                for (let j = 0; j < fullies; j++) {
                    const rand = Math.floor(Math.random() * noms.length);
                    element.push(noms[rand])
                    noms.splice(rand,1);
                }
                this.group_lists[g].membres = element
            }

            if(noms.length<fullies){
                
                for (let j = 0; j < num; j++) {
                    const rand = Math.floor(Math.random() * noms.length);
                    this.group_lists[j].membres.push(noms[rand])
                    noms.splice(rand,1);
                }
            }   
        }         
    } 
  }
}
</script>

<style >
    .container{
        height: 100%;
    }   
    .content{
        height: 100%;
    }   
  
    h1{
        font-size: 4rem;
        color: whitesmoke;
        margin: 2rem;
    }
    main{
        display: flex;
        flex-wrap: wrap;
        justify-content: space-evenly;
        height:80%;
    }
    .creator, .results{
        background: rgba(252, 252, 255, 0.363);
        padding: 1rem ;
        width: 47%;
        height:100%;
        margin:0 auto;
        border-radius: 1rem ;
    }
    .ajout-form{
        width: 85%;
        margin: 0 auto;
        display: flex;
        justify-content: space-between;
    }
    main input{
        padding: 0.75rem;
        margin-right: 0.25rem;
        border: none;
        border-radius: 1rem; 
    }
    .ajout-form input{
        width: 80%;
    }
    .creator button{
        padding: 0.5rem;
        border-radius: 1rem;
        border: none;
        background: rgb(83, 61, 126);
        color: white;
    }
    .list{
        width: 85%;
        height: 80%;
        margin: 1rem  auto;
        
        
    }
    .list ul{
        background: rgba(255, 255, 255, 0.836);
        list-style: none;
        height: 80%;
        padding: 1rem;
        margin: 1rem 0;
         border-radius: 1rem;
         overflow:auto;
    }
    .list h3{
        background: rgb(83, 61, 126);
        color: whitesmoke;
        padding: 0.5rem 0;
        border-radius: 1rem;
    }
   .generator{
       color: white;
    }
    .generator button{
        font-size: 1.25rem;
        padding: 0.75rem;
        margin-left: 1rem;
    }

    .results{
        width: 45%;
    }
    article{
        padding: 1rem;
        height: 100%;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-evenly;
    }
    .group-lists{
        background: white;
        width: 45%;
        height: fit-content;
        border-radius: 1rem;
    }
    .group-lists h3{
        background: rgb(83, 61, 126);
        color: white;
        padding: 0.5rem 0;
    }
    .group-lists ul{
        padding: 0.5rem;
    }

    @media screen and (max-width: 800px) {
        main{
         flex-direction: column;
        }
    }
</style>