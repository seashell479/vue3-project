<template>
  <input type="text" :value="name" />
  <button class="btn btn-primary" @:click="onsubmit">click</button>

  <!-- <div v-bind:class="nameClass">
    <h1>안녕하세요 {{ name }}님 🦄</h1>
    <p>버튼을 눌러보세요! 이름이 변경되나요? 🤩</p>
    <input v-bind:type="inputType" :value="name">
    <button class="btn btn-primary" @click="updateName()">click</button> -->

  <!-- <h1>안녕하세요 {{ name }}님 🦄</h1> -->
  <!-- <h3>당신의 나이는 {{ age }}세 입니까? 🙌</h3>
    <p class="study">지금 Vue 공부를 시작하셨군요?? 👾</p>
    <p>Vue 공부 {{ greet }}</p>
    <p>버튼을 눌러보세요! 그리고 콘솔도 확인해보세요~</p> -->
  <!-- <p>버튼을 눌러보세요! 이름이 변경되나요? 🤩</p>
    <button class="btn btn-primary" v-on:click="updateName()">한/영 변환</button> -->

  <!-- <h1>값 증가: {{ count1 }}</h1>
    <h1>값 곱셈: {{ count2 }}</h1>
    <div class="d-flex text-center justify-content-center">
      <button v-on:click="increase()" class="btn btn-primary mt-2">증가</button>
      <button v-on:click="multiple()" class="btn btn-primary ms-2 mt-2">곱셈</button>
      <button v-on:click="refresh()" class="btn btn-primary ms-2 mt-2">리셋</button>
      <button v-on:click="something('sum')" class="btn btn-primary mt-2">증가</button>
      <button v-on:click="something('mul')" class="btn btn-primary ms-2 mt-2">곱셈</button>
      <button v-on:click="something('reset')" class="btn btn-primary ms-2 mt-2">리셋</button>
    </div> 
  </div>-->
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const name = ref("Eun-Hyun Kim");

    function onsubmit() {
      console.log(name.value);
    }

    return { name, onsubmit };
  }
}

// export default {
//   setup() {
//     const name = ref("Eun-Hyun Kim");
//     const inputType = ref("text");
//     const nameClass = ref("originClass");

//     function updateName() {
//       name.value = "ehkim";
//       inputType.value = "number";
//       nameClass.value = "changeClass"
//     }

//     return { name, inputType, nameClass, updateName };
//   },
// }

// export default {
//   setup() {
//     const information = reactive({ id:1, name: "Eun-Hyun Kim", age: 24});

//     function updateName(){
//       information.name = "ehkim";
//       console.log(information);
//     }

//     return { information, updateName };
//   },
// };


// export default {
//   setup() {
//     const count1 = ref(1);
//     const count2 = ref(1);

//     function something(state) {
//       switch (state) {
//         case "sum": count1.value++
//           break;
//         case "mul": count2.value = count2.value * 2
//           break;
//         case "reset": count1.value = 1;
//           count2.value = 1;
//       }
//     }
//     return {
//       count1, count2, something
//     }

    // if else, 중첩 if문 써서 하기
    // function something(state) {
    //   if (state === "sum") {
    //     count1.value++;
    //   } else if (state === "mul") {
    //     count2.value = count2.value * 2;
    //   } else {
    //     count1.value = 1;
    //     count2.value = 1;
    //   }
    // }
    // return {
    //   count1, count2, something
    // }

    // 함수 3개 만들어서 하기
    // function increase() {
    //   count1.value++;
    // }

    // function multiple() {
    //   count2.value = count2.value * 2;
    // }

    // function refresh() {
    //   count1.value = 1;
    //   count2.value = 1;
    // }

    // return {
    //   count1, count2, increase, multiple, refresh
    // }

    // const name = "김은현";
    // const age = 24;
    // let name = "김은현";
    // const name = ref("김은현");

    // function updateName() {
    //   if (name.value === "김은현") {
    //     name.value = "Eun-Hyun Kim";
    //   } else {
    //     name.value = "김은현";
    //   }
    //   console.log(name);
    // }

    // function printlog() {
    //   console.log("Button Clicked 😍");
    // }

    // function greeting(name) {
    //   return "화이팅 😍" + name;
    // }

    // const greet = greeting(name);
    // console.log(greet);

    // return { 바인딩
    //   name, updateName
    //   Count
    // };
//   }
// }
</script>

<style>
div {
  text-align: center;
}

div.originClass {
  color: black;
}

div.changeClass {
  color: darkslateblue;
}

/* h1 {
  color: darkslateblue;
  font-weight: bold;
}

h3 {
  color: lightseagreen;
} */

.study {
  color: tomato;
  font-weight: bold;
  font-size: 20px;
}
</style>
