<template>
  <div class="mx-8 my-4" v-if="state.isLoaded">
    <p class="mx-2 my-2 font-bold">게시글 목록</p>
    <div class="mx-2 grid grid-cols-2 gap-4">
      <div class="bg-gray-100 p-4 rounded-xl shadow-md" v-for="(val, idx) in state.post_list" :key="idx">
          <p class="font-bold">{{val?.title}}</p>
          <p class="text-sm">{{val?.time.toLocaleString()}}</p>
          <p class="text-sm">{{val?.author}}</p>
          <p class="text-sm">{{val?.read_count}}명 읽음</p>
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
        new Post("Kotlin을 사용해야 하는 이유",new Date(), "다은",23),
        new Post("코딩 입문 언어는 C언어죠",new Date(),"파이썬 싫어",39),
        new Post("최고의 동아리 EDCAN",new Date(), "밤샘 개발자",59),
        new Post("부장님 사랑합니다",new Date(),"vue강의 개꿀",44)
    
      ];
      state.isLoaded=true;
    }, 1500);
  });



</script>


