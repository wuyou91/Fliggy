<template>
  <div class="destination">
    <letter-list @change="letterChange"></letter-list>
    <destination-header></destination-header>
    <destination-list :letter="letter"></destination-list>
  </div>
</template>

<script>
import DestinationHeader from './components/Header'
import DestinationList from './components/DestinationList'
import LetterList from './components/LetterList'
import axios from 'axios'
import { mapMutations } from 'vuex'

export default {
  name: 'Destination',
  components: {
    DestinationHeader,
    DestinationList,
    LetterList
  },
  data () {
    return {
      letter: ''
    }
  },
  methods: {
    getDestinationInfo () {
      axios.get('https://www.easy-mock.com/mock/5b2372e2b541690d6ed33b65/api/destination').then(this.getDestinationInfoDate)
    },
    getDestinationInfoDate (res) {
      let info = res.data
      if (info.ret && info.data) {
        let data = info.data
        this.puInStore(data)
      }
    },
    letterChange (letter) {
      this.letter = letter
    },
    ...mapMutations(['puInStore'])
  },
  mounted () {
    this.getDestinationInfo()
  }
}
</script>
