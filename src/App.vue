<template>
  <div class="mx-8 my-4" v-if="state.isLoaded">
    
    <div>
      <p class="text-sm font-bold">이름</p>
      <input id="input_name" :value="state.name" @input="changedInput" class="bg-gray-200 rounded-lg px-2 py-1"/>
      <p v-if="state.name.length<1" class="text-sm text-red-500 font-bold">이름을 입력해주세요.</p>
      <p v-else-if="!/^[가-힣a-zA-Z]+$/.test(state.name)" class="text-sm text-red-500 font-bold">한글, 영어만 입력 가능합니다.</p>
      <p v-else-if="!/^.{2,8}$/.test(state.name)" class="text-sm text-red-500 font-bold">2~8글자 사이로 입력해주세요.</p>
      <p v-else-if="state.name.length >= 2" class="text-sm text-blue-500 font-bold">멋진 이름을 가지고 계시네요!</p>
      
      <p class="text-sm font-bold">아이디</p>
      <input id="input_id" :value="state.id" @input="changedInput" class="bg-gray-200 rounded-lg px-2 py-1"/>
      <p v-if="state.id.length<1" class="text-sm text-red-500 font-bold">아이디를 입력해주세요.</p>
      <p v-else-if="!/^[A-za-z]/.test(state.id)" class="text-sm text-red-500 font-bold">첫글자는 영문이여야 합니다.</p>
      <p v-else-if="!/^[a-zA-Z0-9_-]{4,16}$/.test(state.id)" class="text-sm text-red-500 font-bold">영문 or 숫자 4자 이상 16자 미만으로 입력해주세요.</p>
      <p v-else-if="state.id.length >= 2" class="text-sm text-blue-500 font-bold">사용 가능한 아이디입니다.</p>

      <p class="text-sm font-bold">비밀번호</p>
      <input id="input_password" :value="state.password" type="password" @input="changedInput" class="bg-gray-200 rounded-lg px-2 py-1"/>
      <p v-if="!/^[a-zA-Z0-9]{8,20}$/.test(state.password)" class="text-sm text-red-500 font-bold">영문 or 숫자 8자 이상 20자 미만으로 입력해주세요.</p>
      <p v-else class="text-sm text-blue-500 font-bold">사용 가능한 비밀번호 입니다.</p>

      <p class="text-sm font-bold">비밀번호 확인</p>
      <input id="input_passwordCheck" :value="state.passwordCheck" type="password" @input="changedInput" class="bg-gray-200 rounded-lg px-2 py-1"/>
      <p v-if="state.passwordCheck.length==0" class="text-sm text-red-500 font-bold">비밀번호를 입력해주세요</p>
      <p v-else-if="state.password==state.passwordCheck" class="text-sm text-blue-500 font-bold">비밀번호가 일치합니다.</p>
      <p v-else class="text-sm text-red-500 font-bold">비밀번호가 일치하지 않습니다.</p>

      <button class="bg-blue-300 rounded-lg px-2 py-1 font-bold mx-1 my-3">회원가입</button>      
    </div>

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
  <div>
    
  </div>

</template>
<script setup>
  import {onMounted, reactive} from "vue";

  class Post{
    constructor(title,content, time, author, read_count){
      this.title=title;
      this.content=content
      this.time=time;
      this.author=author;
      this.read_count=read_count;
    }
  }

  const state = reactive({
    name:"",
    id:"",
    password:"",
    passwordCheck:"",
    
    
    post_list: [],
  });

  const changedInput=({target:{id,value}})=>{
    const name=id.split("_")[1];
    state[name]=value;
  };

  onMounted(()=>{
    setTimeout(()=>{
      state.post_list=[
        new Post("Kotlin을 사용해야 하는 이유","",new Date(), "다은",23),
        new Post("코딩 입문 언어는 C언어죠","",new Date(),"파이썬 싫어",39),
        new Post("최고의 동아리 EDCAN","",new Date(), "밤샘 개발자",59),
        new Post("부장님 사랑합니다","",new Date(),"vue강의 개꿀",44)
      ];
      state.isLoaded=true;
    }, 1500);
  });



</script>


