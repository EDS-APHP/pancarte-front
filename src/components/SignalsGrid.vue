<template>
    <b-container fluid>
      <b-row class='mt-3'><b-col><h4>{{msg}}</h4></b-col></b-row>
      <b-row>
      <b-col class='grid-stack'>
          <b-row v-for='signal in room.available_signals' v-bind:key='signal.id' class='grid-stack-item'
            data-gs-x='0' data-gs-y='0'
            data-gs-width='12' data-gs-height='1'>
            <div class='grid-stack-item-content'>
              <div><b>{{signal}}</b></div>
              <signal :signal='signal' :signalConf='signalConf'></signal>
            </div>
          </b-row>
    </b-col>
    </b-row>
    </b-container>
</template>


<script>
import moment from 'moment'
moment.locale('fr')
import 'gridstack/dist/gridstack.jQueryUI'
import $ from 'jquery'
import Signal from '@/components/Signal'

export default {
  name: 'SignalsGrid',
  components: {
    Signal: Signal
  },
  data () {
    return {
      msg: 'Temps réel'
    }
  },
  props: ['room', 'signalConf'],
  methods: {
    enableGrid: function () {
      var options = {
        cellHeight: 180,
        verticalMargin: 0,
        resizable: {
          handles: 'se, s, e, sw, w'
        },
        animate: true,
        removable: true
      }

      $('.grid-stack').gridstack(options)
    }
  },

  mounted: function () {
    this.enableGrid()
  }
}
</script>
