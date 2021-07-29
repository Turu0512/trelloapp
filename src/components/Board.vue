<template>
<div>
 <header>
  my Trello
 </header>
 <main>
  <!-- タスクの総数 -->
  <p class="info-line"> All:0 task</p>
  <div class="list-index">
   <list v-for="(item,index) in lists"
   :key="item.id"
   :title="item.title"
   :listIndex="index"></list>
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
    List
  },
 computed: {
  ...mapState([
   'lists'
  ]),
 },
}
</script>