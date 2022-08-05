<template>
   <div class="bg-dark h-screen">
      <div class="flex" style="height:88vh;">
       <!-- Side Nav -->
       <div class="w-56 bg-black h-full flex-none">
          <div class="p-6">
          <img src="https://storage.googleapis.com/pr-newsroom-wp/1/2018/11/Spotify_Logo_RGB_White.png" class="h-10">
          </div>
          <div class="mx-2 mb-5">
             <button v-for="(page,index) in pages" v-bind:key="index" @click="setID=page.id" :class="'w-full focus:outline-none flex text-sm text-white font-semibold rounded px-3 py-2 items-center justify-start ' + `${setID === page.id ? 'bg-light text-white' : 'text-lightest' }` " >
              <i :class="'fas fa-'+ page.icon + ' text-xl  mr-3' "></i>
              <p>{{page.name}}</p>
             </button>
          </div>
          <div class="mx-5">
             <h1 class="mb-3 text-xs text-lightest tracking-widest uppercase">Playlists</h1>
             <button class="flex items-center justify-start opacity-75 hover:opacity-100">
                <img :src="'addNew.png'" class="h-8 w-8 mr-3 mb-2" />
                <p class="text-sm text-white font-semibold">Create Playlist</p>
             </button>
             <button class="flex items-center justify-start opacity-75 hover:opacity-100">
                <img :src="'Like.png'" class="h-8 w-8 mr-3 " />
                <p class="text-sm text-white font-semibold">Liked Songs</p>
             </button>
             <div class="h-px w-full bg-light my-3"> </div>
          </div>
          <div class="mx-5">
             <div class="w-full h-10 overflow-y-scroll">
                <p v-for="(album,index) in albums" v-bind:key="index"  class="text-lightest hover:text-white text-sm  py-1">{{album.name}}</p>
             </div>
             <button class="flex items-center justify-start text-lightest hover:text-white py-2">
                <i class="fas fa-arrow-circle-down mr-3 rounded-full text-sm"></i>
                <p class="text-sm font-semibold">Install App</p>
             </button>
          </div>
          <div class="relative">
             <div class="w-full h-full flex justify-end items-start opacity-0 hover:opacity-100 p-5 absolute">
                <div class="bg-black rounded-full h-4 w-4 ">
                 <i class="fas fa-chevron-down text-white text-sm"></i>  
                </div>
             </div>
             <img :src="'playing.jpg'" />
          </div>
       </div>
      
       <!-- Main Content -->
       <div class="w-full h-full relative overflow-y-scroll">
         <!-- Header -->
          <div class="w-full sticky top-0 py-4 px-6 flex items-center justify-between bg-dark">
          <div class="flex items-center">
             <button class="rounded-full bg-black w-8 h-8 text-white mr-3">
                <i class="fas fa-chevron-left text-xl"></i>
             </button>
             <button class="rounded-full bg-black w-8 h-8 text-white">
                <i class="fas fa-chevron-right text-xl"></i>
             </button>
          </div>
          <div class="relative">
             <button @click="showDropdown=true" class="focus:outline-none bg-light rounded-full py-1 px-2 flex items-center">
                <img :src="'myFace.jpeg'" class="rounded-full h-6 w-6 mr-2">
                <p class="text-white font-semibold text-xs mr-3">Neelaksh Mathur</p>
                <i v-if="showDropdown === false" class="fas fa-sort-down text-white"></i>
                <i v-if="showDropdown === true" class="fas fa-sort-up text-white"></i>
             </button>
             <div v-if="showDropdown===true" class="absolute bg-light w-full rounded mt-1">
                <button @click="showDropdown=false" class="focus:outline-none w-full text-sm py-2 text-lightest hover:text-white border-b border-white opacity-75 hover:opacity-100">Account</button>
                <button @click="showDropdown=false" class="focus:outline-none w-full text-sm py-2 text-lightest hover:text-white border-b border-light opacity-75 hover:opacity-100">Log Out</button>
             </div>
           </div>
          </div>
          <!-- Cards -->
          <div class="px-6 py-3">
           <div class=" flex items-center justify-between">
              <h1 class="pl-2 text-2xl font-semibold text-white tracking-wider hover:underline">Recently Played</h1>
              <h2 class="pr-8 pt-4 text-xs text-lightest uppercase tracking-wider hover:underline mb-3">See All</h2>
           </div>  
             <div class="w-full flex flex-wrap">
              <div v-for="(recent,index) in recents" v-bind:key="index" class="m-2 w-48 relative">
              <div class="absolute w-full h-full flex items-end justify-end p-5 opacity-0 hover:opacity-100">
                 <div class="bg-green rounded-full h-10 w-10 flex items-center justify-center">
                   <i class="fas fa-play text-white text-xl"></i>  
                 </div>
              </div>
              <div class=" bg-light w-full h-full p-5 rounded-lg shadow-md">
                <img :src="recent.src" class="h-auto w-full shadow mb-2">
                <h1 class="text-sm font-semibold text-white tracking-wide">{{recent.title}}</h1>
                <h2 class="text-xs text-lightest tracking-wide ">{{recent.artist}}</h2> 
              </div>
             </div>
            </div>
           </div>
           <div class="px-6 py-3">
           <div class="pl-2">
              <h1 class="text-2xl font-semibold text-white tracking-wider hover:underline">Made for Neelaksh</h1>
              <h2 class="text-sm text-lightest">Get better recommendations the more you listen.</h2>
           </div>  
             <div class="w-full flex flex-wrap">
              <div v-for="(custom,index) in customs" v-bind:key="index" class="m-2 w-48 relative">
               <div class="absolute w-full h-full flex items-end justify-end p-5 opacity-0 hover:opacity-100">
                 <div class="bg-green rounded-full h-10 w-10 flex items-center justify-center">
                   <i class="fas fa-play text-white text-xl"></i>  
                 </div>
              </div>
              <div class="bg-light w-full h-full p-5 rounded-lg shadow-md">
                <img :src="custom.src" class="h-auto w-full shadow mb-2">
                <h1 class="text-sm font-semibold text-white tracking-wide">{{custom.title}}</h1>
                <h2 class="text-xs text-lightest tracking-wide ">{{custom.artist}}</h2> 
              </div>
             </div>
            </div>
           </div>
          </div>
        </div>
       <!-- Play Bar -->
       <div class="w-full flex items-center justify-between px-3 bg-light border-t border-dark" style="height:12vh;">
         <div class="flex items-center w-1/4">
            <div>
               <h1 class="text-sm text-white tracking-wide font-semibold">G.O.A.T.</h1>
               <h2 class="text-xs text-lightest tracking-wide">Diljit Dosanjh</h2>
            </div>
            <i class="fas fa-heart text-base text-green mx-4"></i>
            <i class="fas fa-window-maximize text-base text-lightest hover:text-white"></i>
         </div>
         <div class="flex flex-col justify-center w-2/4 items-center">
            <div class="flex items-center">
               <button class="mx-6 text-lightest hover:text-white"><i class="fas fa-random text-sm"></i></button>
               <button class="text-lightest hover:text-white"><i class="fas fa-step-backward text-sm"></i></button>
               <button @click.prevent="playSong('song.mp3'),pause=true" class="rounded-full h-8 w-8 flex items-center focus-outline:none justify-center mx-6 border-lightest border text-lightest hover:text-white"><i v-if="pause===false" class="fas fa-play text-sm"></i><i v-if="pause===true" class="fas fa-pause"></i></button>
               <button class="text-lightest hover:text-white"><i class="fas fa-step-forward text-sm"></i></button>
               <button class="mx-6 text-lightest hover:text-white"><i class="fas fa-redo text-sm"></i></button>
            </div>
            <div class="w-3/4 flex items-center justify-center mt-3">
             <p class="text-xs text-lightest mr-1">0:28</p>
               <div class="w-full h-1 bg-dark rounded-full flex items-center">       
               <div class="h-1 rounded-full bg-green" style="width:18%;">
               </div>
               <div class="h-3 w-3 bg-white rounded-full -ml-1 shadow">
               </div>
              </div>
             <p class="text-xs text-lightest ml-1">3:43</p> 
            </div>
         </div>
         <div class="flex items-center w-1/4 justify-end">
            <i class="fas fa-layer-group text-lightest hover:text-white"></i>
            <i class="mx-3 fas fa-mobile text-lightest hover:text-white"></i>
            <i class="fas fa-volume-up text-lightest hover:text-white"></i>
            <div class="w-20 ml-1 bg-lightest rounded-full h-1">               
            </div>
         </div>
       </div>
   </div>
</template>

<script>


export default {
 name:'App',
 data:function(){
    return {
     pages:[
        {id:'home', name:'Home', icon:'home'},
        {id:'search', name:'Search', icon:'search'},
        {id:'library', name:'Your Library', icon:'chart-bar'}
     ],
     setID: 'home',
     albums:[
        {name:'Desi Hip Hop'},
        {name:'No Breadx Just Jam Please!'},
        {name:'Lucky Ali'},
        {name:'EDM Mix'},
        {name:'Punjabi Songs'},
        {name:'Old Melody'}
     ],
     showDropdown:false,
     recents:[
        {src:'1_recent.png', title:'Sidhu Moose Wala', artist:'Artist'},
        {src:'2_recent.png', title:'Diljit Dosanjh', artist:'Artist'},
        {src:'3_recent.png', title:'Moosetape', artist:'Sidhu Moose Wala'},
        {src:'4_recent.png', title:'Same Beef', artist:'Bohemia,Sidhu Moose Wala'},
        {src:'5_recent.png', title:'Mission ISRO with Harsha Bhogle', artist:'Spotify Studios'},
        {src:'6_recent.png', title:'Lucky Ali', artist:'By Neelaksh Mathur'}
     ],
     customs:[
        {src:'daily_1.png', title:'Daily Mix 1', artist:'By Spotify'},
        {src:'daily_2.png', title:'Daily Mix 2', artist:'By Spotify'},
        {src:'daily_3.png', title:'Daily Mix 3', artist:'By Spotify'},
        {src:'daily_4.png', title:'Daily Mix 4', artist:'By Spotify'},
        {src:'daily_5.png', title:'Daily Mix 5', artist:'By Spotify'},
        {src:'daily_6.png', title:'Daily Mix 6', artist:'By Spotify'}
     ],
     pause:false
    };
 },
 methods:{
   playSong(song){
      if(song){
         var audio = new Audio(song);
         audio.play();
      }
   } 
 }
};


</script>

<style scoped>
/* width */
::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  background:black;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: black;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background:#888;
}

</style>
