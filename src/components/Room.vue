<template>
<b-card no-body>
  <b-card-header><b-col class='mb-3 mt-3'><h3>{{sectorName}} - {{roomName}}</h3></b-col></b-card-header>
  <b-tabs pills card>
    <b-tab title='Temps réel' active>
  <b-row>
    <b-col cols='4'><signals-grid :room='room' :signalConf='signalConf'></signals-grid></b-col>
    <b-col cols='4'><trends-grid :room='room' :signalConf='signalConf'></trends-grid></b-col>
    <b-col cols='4'><indices-grid :room='room' :signalConf='signalConf'></indices-grid></b-col>
  </b-row>
    </b-tab>
    <b-tab title='Pancarte'>
      <pancarte-grid></pancarte-grid>
    </b-tab>
  </b-tabs>
</b-card>
</template>

<script>
import moment from 'moment'
import sectors from '../roomsdata.js'
import signalConf from '../signalsdata.js'
import SignalsGrid from '@/components/SignalsGrid'
import TrendsGrid from '@/components/TrendsGrid'
import IndicesGrid from '@/components/IndicesGrid'
import PancarteGrid from '@/components/PancarteGrid'

moment.locale('fr')
export default {
  name: 'Room',
  components: {
    SignalsGrid,
    TrendsGrid,
    IndicesGrid,
    PancarteGrid
  },
  data () {
    return {
      msg: 'Vue par chambre',
      signalConf: signalConf.signalConf,
      sectors: sectors.sectors,
      sectorName: '',
      roomName: '',
      sector: '',
      room: '',
      nextRoomName: '',
      index: ''
    }
  },

  created () {
    this.sectorName = this.$route.params.sector
    this.roomName = this.$route.params.room
    var sectorName = this.sectorName
    var roomName = this.roomName
    this.sector = this.sectors.find(function (sector) {
      return sector.name === sectorName
    })
    this.room = this.sector.rooms.find(function (room) {
      return room.name === roomName
    })
    var index = sectors.indexOf('Hégoa')
    this.nextRoomName = this.sector.rooms.find(function (room) {
      return room.name === room.name[index + 1]
    })
  },

  filters: {
    moment: function (value) {
      return moment(value).format('DD/MM/YY')
    },
    sincedays: function (value) {
      return moment().diff(value, 'days')
    },
    ageinyears: function (value) {
      return moment(value).fromNow(true)
    }
  }
}
</script>

<style scoped>
.patient-header {
  color: #373a3c;
  width: 100%;
  margin-bottom: 0;
  background-color: rgba(0, 0, 0, 0.03);
  border-bottom: 1px solid rgba(0, 0, 0, 0.125);
  padding: 0.3rem;
}
.patient-header-line {
  font-weight: bold;
  margin-bottom: 0rem;
}
.patient-body {
  padding: 0.3rem;
  font-size: 0.8em;
}
.patient {
  display: block;
  word-wrap: break-word;
  background-color: #fff;
  background-clip: border-box;
  border: 1px solid rgba(0, 0, 0, 0.125);
  margin-right: 1em;
  margin-bottom: 1em;
}
.patient-signals {
  text-align: right;
  text-shadow: -0.5px -0.5px 0.5px #e5e5e5;
}
.patient-signals-header {
  padding-bottom: 0.5rem;
}
</style>
