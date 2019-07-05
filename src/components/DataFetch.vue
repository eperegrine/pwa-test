<template>
  <div>
    <p>{{data}}</p>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

interface SampleData {
  name: string,
  age: Number
}

const TEST_KEY: string = "TEST"

@Component
export default class HelloWorld extends Vue {
  
  private data: SampleData = {name:"", age: 0}

  created() {
    console.log(navigator);
    
    let a = localStorage.getItem(TEST_KEY);
    if (a != null) {
      console.log("FROM LS");
      
      this.data = JSON.parse(a);
    } else {
      setTimeout(() => {
        this.data = {name:"test", age: 101};
        localStorage.setItem(TEST_KEY, JSON.stringify(this.data));
      }, 1000);
    }
  }

}
</script>