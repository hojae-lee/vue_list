<template>

  <!-- 모달창 -->
  <!-- openModal 이 true일 경우만 모달이 열릴것임. Vue에서 모달창을 만드는 방법. -->
  <div class="black-bg" v-if="openModal == true">
    <div class="white-bg">
      <h4>모달창이에용</h4>
      <p>모달창 내용이 들어가용</p>
      <button @click="closeModal" class="btnClass">닫기</button>
    </div>
  </div>

  <div class="menu">
    <!-- v-for="작명 in 몇회" :key="작명" (고유한 키속성)작명 없으면 오류나요~ 왜냐면 반복문 돌린 요소를 컴퓨터가 구분하기 위해 씀 괄호쳐서 Vue 반복문 특 변수 작명2개까지 가능 -->
    <a v-for="(menuTitle, i) in 메뉴들" :key="i">{{ menuTitle }}</a>
  </div>

  <img alt="Vue logo" src="./assets/logo.png">
  <div>
    <h2>뷰를 이용한 간단한 리스트 만들기</h2>
  </div>
    <!-- {{logo}} -->

  <!-- 아래의 주석 친 코드를 밑에 v-for 로 변경. -->
  <!-- <div>
    <img src="./assets/room0.jpg" class="room-img">
    <h4 @click="openModal = true" :style="nameClass">{{ products[0] }}</h4>
    <p>{{ price[0] }} 만원</p>
    <button @click="increase(1)">허위매물신고</button> <span>신고수: {{ 신고수[0] }}</span>
  </div>
  <div>
    <img src="./assets/room1.jpg" class="room-img">
    <h4>{{ products[1] }}원룸</h4>
    <p>{{ price[1] }} 만원</p>
    <button @click="increase(2)">허위매물신고</button> <span>신고수: {{ 신고수[1] }}</span>
  </div>
  <div>
    <img src="./assets/room2.jpg" class="room-img">
    <h4>{{ products[2] }}원룸</h4>
    <p>{{ price[2] }} 만원</p>
    <button @click="increase(3)">허위매물신고</button> <span>신고수: {{ 신고수[2] }}</span>
  </div> -->

  <div v-for="(pi, index) in dataLength" :key="pi">
    <img :src="products[index].image" class="room-img">
    <h4 @click="openModal = true" :style="nameClass">{{ products[index].title }}</h4>
    <p>{{ products[index].price }} 만원</p>
    <button @click="increase(index)" class="btnClass">허위매물신고</button> <span>신고수: {{ 신고수[index] }}</span>
  </div>
</template>

<script>

import data from './data.js';

let alertArray = [];
const dataKeys = Object.keys(data);

for (let i = 0; i < dataKeys.length; i++) {
  alertArray.push(0);
}

export default {
  name: 'App',
  data() { // 데이터 보관함을 만듬
    return {
      // 여기에 데이터 보관하셈. HTML에 {{데이터 이름}} 해서 꽂아 넣으면댐!
      // 이 문법 언제 쓸까요?! 데이터 바인딩을 하는 이유 - HTML을 하드코딩 해놓으면 나중에 변경이 어려움. Vue의 실시간 자동 렌더링 쓰려면 하셈!
      // Vue는 신기해서 data를 변경하면 data와 관련된 HTML에도 실시간으로 반영됨.
      // 자주 변경될 데이터들은 밑에 저장해놨다가 콧수염으로 사용하세요.
      price: [60, 50, 50],
      // price_2 : 50,
      logo: '원룸샵',
      // HTML 속성도 데이터 바인딩 가능 :style="nameClass",  :속성="데이터이름"
      nameClass: 'color : blue',
      메뉴들: ['Home', 'Products', 'About'],
      // products: ['역삼동원룸', '천호동원룸', '마포구원룸'],
      products: data,
      dataLength: dataKeys.length,
      신고수: alertArray,
      // 모달창의 현재 상태를 저장, 현재 데이터에 따라 UI가 어떻게 보일지 작성.
      openModal: false
    }
  },
  methods: { // 함수만드는 공간.
    increase(data) {
      this.신고수[data]++;
    },
    closeModal() {
      this.openModal = false;
    }
  },
  components: {
  }
}
</script>

<style>
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
.room-img {
  width: 60%;
  margin-top: 40px;
}
.btnClass {
  background: tomato;
  border: none;
  color: #fff;
}
</style>
