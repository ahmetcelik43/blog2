<template>

  <div class="search-content">
     <br>
        <div  class="search-form" > 
          <div class="input-container">
             <b-spinner  class="icon" variant="primary" type="grow"  :class="spinner ? 'spinner-show':'spinner-hide'" ></b-spinner>
           <b-form-input  trim  @keyup="checkForm($event)" :class="searchText ? 'search-input-success':'search-input-error'" v-model="searchText" size="md" class="mr-sm-2 input-field"  placeholder="Ara">
          </b-form-input>
   <ul class="search-ul"   :class="searchText!='' ? 'search-show':'search-hide'">
          <li>
            <a class="atag" @click="close"> <vue-fontawesome   icon="window-close"  color="grey"> </vue-fontawesome> </a>
           <br>
           <br>
            </li>
          
          
          <li class="search-li" v-for="(entry) in searchTexts" v-bind:key="entry">

           <vue-fontawesome  id="search-icon" icon="search"  color="white"> </vue-fontawesome> <a class="search-text-input" @click="searchevent(entry)">   {{entry}}
          </a>
          </li>
        </ul>
  </div>

 

        <!-- <b-button @click="searchOnSubmit($event)" :disabled="searchText!=null ? false:true " type="submit" size="sm"> <vue-fontawesome class="my-2 my-sm-0"   icon="search"   color="lightgray"></vue-fontawesome>
        </b-button>
   -->
  
        </div>
      
 <!--
 <ul v-if="errors" class="errors-ul">
            <li  v-for="error in errors" v-bind:key="error"><strong class="text-danger">{{ error }}</strong></li>

    </ul>
-->
   </div>
</template>

<script lang="ts">
import Vue from 'vue';
import axios from 'axios';

export default Vue.extend({
  name: 'Categorys',
  props: ['articleAll'],
  data(){
   return{ categories:[],spinner:false,searchText: '',
 searchTexts:[''],searchs:[''],articles:String[10]
   }
  },
  
   created()
  {
this.articles=this.articleAll

 this.articles.forEach((value, index) => {
  
this.searchs.push(value.baslik);

});
  },
  methods:{

close()
{
this.searchText=''
},
searchevent(value)
{
  this.spinner=true
  this.searchText=value
   setTimeout(function(){ 
            
  this.$root.$router.push('/articledetails/'+encodeURIComponent(this.searchText));

           }.bind(this),3000);

},

   
 checkForm: function (e) {
       e.preventDefault();

this.searchText=e.target.value
     if (this.searchText!='') {
if (e.keyCode === 13) {
  this.spinner=true
    // Cancel the default action, if needed
    // Trigger the button element with a click
          setTimeout(function(){ 
            
  this.$root.$router.push('/articledetails/'+encodeURIComponent(this.searchText));

           }.bind(this),3000);



  }
else
{   
  this.searchTexts.splice(0,this.searchTexts.length)
  this.searchs.forEach((value, index) => {
 if(value.includes(this.searchText))
   {
      
    this.searchTexts.push(value);

   
      

      //this.searchTexts.push(value);

   }   
 
            });
}

       }

     
    },
  }
});
</script>

<style scoped>

.search-content
{
background-color: rgb(230,230,230,0.5);
width:100%;
 border-bottom:1px solid black;

height: 100px;

}

.search-show
{
  display: block;
}
.search-hide
{
  display: none;
}
.icon {
width: 10%;
height: 2em;
margin-right:3px;  
margin-top: 5px;
display:inline-block;
}

.search-input-error
{
  border:solid red 1px;
}
.search-input-success
{
  border:none;
}
.search-form
{

margin-left: auto;
margin-right: auto;
width:100%;
padding-left: 5px;
}
  .input-container {
  width: 100%;

}

.spinner-show

{
visibility: visible;
}
.spinner-hide
{
visibility:hidden;
}

#search-icon
{
  margin-left:5px;
  display:inline-block;
  font-size: 25px;
}
.search-ul
{
  z-index: 100;
  list-style: none;
margin-left: auto;
margin-right: auto;
  max-width: 82%;
  min-width: 82%;

position: relative;
background-color:rgb(62, 62, 63);
overflow-y: auto;
max-height: 400px;
border-radius: 5px;
overflow-x: hidden;
text-overflow: ellipsis;

}
.search-ul li:hover
{
  background-color:rgb(230,230,230,0.5);
}
.search-ul li:first-child:hover
{
background-color:rgba(62, 62, 63,0.9);
}
.search-li
{
height:40px;
padding-bottom: 5px;
padding-right:6px;
color:white;
margin-left: -40px;
 
}

.atag
{
  float: right;
  padding-right: 5px;
  font-size: 25px;
}

.search-text-input
{
   text-overflow: ellipsis;
  overflow: hidden; 
  width: 200px; 
  white-space: nowrap;
  margin-left: 3px;
    display:inline-block

}
.input-field {
  max-width: 80%;
    min-width: 80%;

  padding: 10px;
  display:inline-block;

}
</style>