<template>
  <v-flex xs12>
    <v-text-field
      label="Введите сообщение"
      outline
      v-model="text"
      @keydown.enter="send"
    ></v-text-field>
  </v-flex>
</template>

<script>
import {mapState} from 'vuex';
export default {
  data: () => ({
    text: ''
  }),
  computed: mapState(['user']),
  methods: {
    send() {
      console.log(this.$store.state)
      this.$socket.emit('createMessage', {
        
        text: this.text,
        id: this.$store.state.user.id
      }, data => {
        if (typeof data === 'string') {
          console.error(data)
        } else {
          this.text = ''
        }
      })
    }
  }
}
</script>
