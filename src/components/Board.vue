<template>
  <div>
  <header>
    my Trello
  </header>
  <main>
    <!-- タスクの総数 -->
    <p class="info-line"> All:{{ totalCardCount }} task</p>
    <!-- タスクリスト -->
    <draggable class="list-index" :list="lists" @end="movingList">
    <!-- <div class="list-index"> -->
    <list v-for="(item,index) in lists" 
    :key="item.id" 
    :title="item.title" 
    :listIndex="index"
    :cards="item.cards"
    @change="movingCard"
    ></list>
    <list-add></list-add>
    </draggable>
    <!-- </div> -->
  </main>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import ListAdd from "./ListAdd.vue"
import List from "./List.vue"
import { mapState } from "vuex"

export default {
name:"board",
components: {
    ListAdd,
    List,
    draggable,
  },
computed: {
  ...mapState([
  'lists'
  ]),
  totalCardCount(){
    return this.$store.getters.totalCardCount
  },
},
methods: {
  movingCard:function(){
    this.$store.dispatch('updateList',{ lists: this.lists })
  },
  movingList:function(){
    this.$store.dispatch('updateList',{ lists: this.lists })
  }
},

}
</script>