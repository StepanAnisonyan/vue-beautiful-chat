<template>
  <div class="sc-message--text" :style="messageColors">
    <p v-html="messageText"></p>
    <p class="message-time">{{convertDateStamp(data.createdAt)}}</p>
    <p v-if="data.meta" class='sc-message--meta' :style="{color: messageColors.color}">{{data.meta}}</p>
  </div>
</template>

<script>
import escapeGoat from 'escape-goat'
import Autolinker from 'autolinker'
const fmt = require('msgdown')

export default {
  props: {
    data: {
      type: Object,
      required: true
    },
    messageColors: {
      type: Object,
      required: true
    },
    messageStyling: {
      type: Boolean,
      required: true
    }
  },
  computed: {
    messageText() {
      const escaped = escapeGoat.escape(this.data.text)

      return Autolinker.link(this.messageStyling ? fmt(escaped) : escaped, {
        className: 'chatLink',
        truncate: { length: 50, location: 'smart' }
      })
    }
  },
    methods:{
        convertDateStamp(date){

            var date = new Date(date);
            var year = date.getFullYear();
            var mounth = ("0" + (date.getMonth()+1)).slice(-2);
            var day = ("0" + date.getDate()).slice(-2);
            var hours = ("0" + date.getHours()).slice(-2);
            var minutes = ("0" + date.getMinutes()).slice(-2);


            return hours + ':' + minutes + ' ' + day + '.' + mounth + '.' + year;
        },
    }
}
</script>

<style scoped>
a.chatLink {
  color: inherit !important;
}
.message-time{
    margin: 0;
    font-size: 10px;
  }
</style>
