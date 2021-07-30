<template>
  <div class="list">
  <div class="listheader">
    <p class="list-title">{{ title }}</p>
    <!-- 件数表示 -->
    <p class="list-counter">total:{{ totalCardInList}}</p>
    <div class="deletelist" @click="removeList">X</div>
  </div>
  <!-- カードの内容 -->
  <!-- ドラッグで移動 -->
  <draggable group="cards" :list="cards" @end="$emit('change')">
  <card v-for="(item,index) in cards"
        :body="item.body"
        :key="item.id"
        :cardIndex="index"
        :listIndex="listIndex"></card>
  </draggable>
  <!-- カード追加ボタン -->
  <card-add :listIndex="listIndex"></card-add>
</div>
</template>

<script>
import draggable from 'vuedraggable'
import CardAdd from './CardAdd.vue'
import Card from './Card.vue'

export default {
  components: { 
    CardAdd,
    Card,
    draggable
    },
  props:{
  title:{
    type: String,
    required: true,
  },

  cards:{
    type: Array,
    required:true
  },

  listIndex:{
  type: Number,
  required: true,
  }
  },
  computed:{
    totalCardInList(){
      return this.cards.length
    }
  },
  methods: {
  removeList: function(){
  if(confirm('本当にこのリストを削除しますか？')){
    this.$store.dispatch('removelist',{ listIndex: this.listIndex})
  }
  },
  },
  }
</script>