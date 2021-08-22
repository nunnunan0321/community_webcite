<template>
  <div class="mx-8 my-4" v-if="state.isLoaded">
    <p class="mx-2 my-2 font-bold">게시글 목록</p>
    <div class="mx-2 grid grid-cols-2 gap-4">
      <div class="bg-gray-100 p-4 rounded-xl shadow-md" v-for="(val, idx) in state.post_list" :key="idx">
          <p class="font-bold">{{val?.title}}</p>
          <p class="text-sm">{{val?.time.toLocaleString()}}</p>
          <p class="text=sm">{{val?.author}},{{val?.read_count}}명 읽음</p>
      </div>
    </div>
  </div>
  <div v-else>
    <p>로딩중입니다...</p>
  </div>

</template>
<script setup>
  import {onMounted, reactive} from "vue";

  class Post{
    constructor(title, time, author, read_count){
      this.title=title;
      this.time=time;
      this.author=author;
      this.read_count=read_count;
    }
  }

  const state = reactive({
    post_list: [],
  });

  onMounted(()=>{
    setTimeout(()=>{
      state.post_list=[
        new Post("ㅇㅏㄴ녀ㅇ 하세요 ? ㅇ아니 이발롬 왜 지ㄹㅣㅑ 랄이",new Date(), "나",2),
        new Post("게시물입니다",new Date(),"ㅈㄷㅇ",2),
        new Post("134",new Date(), "ㅂㅎㅊ",2),
        new Post("ㄴㅇ려ㅑㅈㄷ라",new Date(),"ㅈㅇㅅ",2)
    
      ];
      state.isLoaded=true;
    }, 1500);
  });



</script>


