<template>
  <div class="container">
    <form v-if="!submitted">
      <label for="onsets">Onsets</label><br>
      <!-- Interpolation between <textarea>{{ test }}</textarea> doesn't work!-->
      <textarea id="onsets" rows="10" class="form-control" v-model.lazy.trim="onsets"></textarea>
      <br>
      <label for="rimes">Rimes</label><br>
      <!-- Interpolation between <textarea>{{ test }}</textarea> doesn't work!-->
      <textarea id="rimes" rows="10" class="form-control" v-model.lazy.trim="rimes"></textarea>


      <br><br>
      <button class="btn btn-primary" @click.prevent="submitted = !submitted">Start &rarr;</button>
    </form>
    <div class="words" v-else>
      <button class="btn btn--return" @click.prevent="submitted = !submitted">&larr;</button>
      <DragWord :word="onset" class="word__onset" v-for="(onset,index) in wordList('onsets')" :key="onset + index"></DragWord>
      <DragWord :word="rime" class="word__rime" v-for="(rime,index) in wordList('rimes')" :key="rime + index"></DragWord>
    </div>
  </div>
</template>

<script>
  import _ from 'lodash';

  import DraggableWord from './DraggableWord.vue';

  export default {
    data () {
      return {
        onsets: 'b\nc\nm',
        rimes: 'at\nan',
        submitted: false
      }
    },
    methods: {
      wordList(dataItem){
        return _.without(this[dataItem].split('\n'), '');
      },
      startGame(){

      }
    },
    components: {
      DragWord: DraggableWord
    }
  }
</script>

<style lang="scss">
body {
  background-color: #424242;
  color: #fff;
  font: 1em Arial,sans-serif;
}

.container {
  position: absolute;
  top: 0;left: 0;bottom: 0;right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.btn {
  background-color: #3299BB;
  border: none;
  border-radius: 5px;
  box-shadow: 0 0 5px #333;
  color: #fff;
  font-size: 1rem;
  font-weight: bold;
  padding: 10px;

  &--return {
    background-color: #BCBCBC;
    position: absolute;
    top: 5px;left: 5px;
  }
}

textarea {
  background-color: #BCBCBC;
  border-radius: 5px;
  font-size: 1rem;
  min-width: 300px;
  padding: 5px;
}


</style>
