<template>
  <div class="home">
    <p>{{greetText}}</p>
    <p>挨拶した回数　：　{{count}}回</p>
    <p v-if="isRegulars">いつもありがとうございます</p>
    <p>
      <MyButton :greet="greetText" @click="onMyButtonClick">挨拶する</MyButton>
    </p>
    <p>
      <ResetButton v-model="greetText"></ResetButton>
    </p>
  </div>
</template>

<script lang="ts">
import { Component, Watch, Vue } from 'vue-property-decorator';
import MyButton from "@/components/MyButton.vue"
import ResetButton from "@/components/ResetButton.vue" // @ is an alias to /src

@Component({
  components: {
    ResetButton,
    MyButton,
  },
})
export default class Home extends Vue {
  private count: number = 0;
  public greetText: string = "Hello";

  public get isRegulars(): boolean {
    return this.count >= 5;
  }

  @Watch('count')
  public countChanged(){
    if(this.count === 5){
      alert("常連になりました")
    }
  }

  public onMyButtonClick(count: number){
    this.count = count;
    this.greetText = "こんにちは"
  }
}
</script>
