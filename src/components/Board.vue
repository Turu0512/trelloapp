<template>
  <div>
  <header>
    my Trello
  </header>
  <main>
    <!-- タスクの総数 -->
    <p class="info-line"> All:{{ totalCardCount }} task</p>
    <!-- タスクリスト -->
    <div class="list-index">
    <list v-for="(item,index) in lists" 
    :key="item.id" 
    :title="item.title" 
    :listIndex="index"
    :cards="item.cards"
    ></list>
    <list-add></list-add>
    </div>
  </main>
  </div>
</template>

<script>
import ListAdd from "./ListAdd.vue"
import List from "./List.vue"
import { mapState } from "vuex"

export default {
name:"board",
components: {
    ListAdd,
    List,
  },
computed: {
  ...mapState([
  'lists'
  ]),
  totalCardCount(){
    return this.$store.getters.totalCardCount
  }
},
}
</script>