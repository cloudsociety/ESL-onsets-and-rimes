<template>
        <div class="word" :style="styleObject" v-drag>{{word}}</div>
</template>

<script>
import _ from 'lodash';
import $ from 'jquery';
import "jquery-ui/ui/widgets/draggable"; // this works directly, but need to include each widget separately
import "jquery-ui-touch-punch-c/jquery.ui.touch-punch.min.js";


  export default {
    data: function() {
      return {
        // someKey: someItem
        styleObject: {
          top: 0,
          left: 0,
          'z-index': 0
        }
      }
    },
    props: ['word'],
    directives: {
      drag: {
        bind(el, binding, vnode) {
          $(document).ready(function() {
            $(el).draggable({
              snap: true,
              stack: ".word",
              distance: 0});
          });
        }
      }
    },
    created(){
      this.styleObject.top = `${_.random(20,50)}vh`;
      this.styleObject.left = `${_.random(30,60)}vw`;
      this.styleObject['z-index'] = _.random(1,10);
    }
  }
</script>

<style lang="scss">
.word {
  background-color: fade_out(#BCBCBC, .3);
  border: 10px solid #3299BB;
  cursor: move;
  // display: inline-block;
  font-size: 4em;
  font-weight: bold;
  min-width: 100px;
  padding: 10px 5px;

  position: absolute;

  &__onset {
    border-right: 0;
    border-top-left-radius: 30px;
    border-bottom-left-radius: 30px;
    padding-left: 30px;
    text-align: right;
  }

  &__rime {
    border-left: 0;
    border-top-right-radius: 30px;
    border-bottom-right-radius: 30px;
    padding-right: 30px;
  }


}
</style>
