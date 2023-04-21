<script setup lang="ts">
import { ref } from 'vue'
import * as EmployeeData from '../assets/data/EmployeeData.json'
//interface
interface employees {
  name: string,
  popularity: number,
  biography: string,
  image: string,
  colleagues: string[]
}
// data
const popularity = ref([
  {
    num: 1,
    name: 'smaller',
  },
  {
    num: 2,
    name: 'small',
  },
  {
    num: 3,
    name: 'medium',
  
  },
  {
    num: 4,
    name: 'large',
  },
  {
    num: 5,
    name: 'larger',
  }
  
  
])
const EmployeeDataRef = ref<employees[]>(EmployeeData.employees)
const currentEmp = ref<number>(0)
//function
const onChange = () => {
  
}
</script>

<template>
  <div class="dashboard ">
    <div class="dashboard__left-side">
      <img src="../assets/logo/the-godfather.svg" alt="">
      <div style="margin-top: 100px">
        <div
          v-for="(emp, inx) of EmployeeDataRef"
          :id="emp.name"
          :class="emp.name !== EmployeeDataRef[currentEmp].name || 'active'"
        >
          <p
            class="pointer"
            :class="popularity.find((val) => val.num == emp.popularity)?.name"
            @click="currentEmp = inx"
          >
            {{ emp.name }}
          </p>
        </div>
      </div>
    </div>
    <div class="dashboard__header-img">
    </div>
    <div class="dashboard__content flex">
      <div style="width: 330px;flex: 0 0 auto">

      </div>
      <div class="flex" style="flex: 1 1 auto">
        <img class="dashboard__avatar" :src="'/src/assets/images/Profile pics/'+ EmployeeDataRef[currentEmp].image" alt="">
        <div class="dashboard__text">
          <p
            style="margin-top: 0"
            class="text-left"
            :class="popularity.find((val) => val.num == EmployeeDataRef[currentEmp].popularity)?.name"
          >
              {{EmployeeDataRef[currentEmp].name}}
          </p>
          <div class="flex algin-center">
            <p style="margin-right: 15px">Popularity</p>
            <input type="range" min="1" max="5" v-model="EmployeeDataRef[currentEmp].popularity" @change="onChange"/>
          </div>
          <div class="dashboard__box text-left">
            <p>Biography</p>
            <p>{{ EmployeeDataRef[currentEmp].biography }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.dashboard {
  position: relative;
  &__left-side{
    position: absolute;
    top: 0;
    width: 300px;
    height: 100vh;
    z-index: 100;
    background-color: rgba(0, 0, 0, 0.5);
    img{
      margin: 35px;
    }
    .pointer{
      cursor: pointer;
    }
    .active{
      background-color: rgba(0, 0, 0, 0.5);;
      color: #fff;
    }
  }
  &__header-img {
    position: relative;
    overflow: hidden;
    height: 277px;
    background-image: url('../assets/images/Header image/Godfather header.jpg');
    background-size: cover;
    background-position: 0px 20%; // cut img
    background-repeat: no-repeat;
    box-shadow: inset 0 0 35px 29px rgba(0, 0, 0, 0.8);
  }
  &__content {
    transform: scale(1) translateY(-36px);
    position: relative;
    margin-right: 120px;
  }
  &__avatar{
    height: 150px;
    width: 150px;
    border: 1px solid #fff;
    margin-right: 26px;
  }
  &__box{
    background-color: #1b1d24;
    padding: 10px;
    border-radius: 10px;
    p {
      margin: 10px 0;
    }
  }
  &__text {
    p{
      color: #fff;
    }
  }
}
.text-left {
  text-align: left;
}
.algin-center{
  align-items: center;
}
.smaller {
  font-size: small;

}
.small {
  font-size: medium;
}
.medium {
  font-size: large;
}
.large {
  font-size: larger;
}
.larger {
  font-size: x-large;
}
input[type=range] {
  -webkit-appearance: none;
  width: 100%;
  height: 3px;
  background: #000;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
}

input[type=range]:hover {
  opacity: 1;
}

input[type=range]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  background: #fff;
  cursor: pointer;
}

input[type=range]::-moz-range-thumb {
  width: 10px;
  height: 2px;
  background: #4CAF50;
  cursor: pointer;
}
</style>
