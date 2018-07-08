<template>
  <div class="wrapper">
    <div class="container">
        <div class="left">
            <div class="top">
                <input type="text" />
                <a href="javascript:;" class="search"></a>
            </div>
            <ul class="people">
                <li class="person active">
                    <img src="../assets/img/profile.jpg" alt="" />
                    <span class="name">Thomas Bangalter</span>
                    <span class="time">{{ this.messages[this.messages.length - 1].date | moment('hh:mm a') }}</span>
                    <span class="preview">{{ this.messages[this.messages.length - 1].text }}</span>
                </li>
            </ul>
        </div>
        <div class="right">
            <div class="top">
                <span>To:
                    <span class="name">Thomas Bangalter</span>
                </span>
            </div>
            <div class="chat active-chat">
                <div class="conversation-start">
                    <span>Today, {{ now | moment('hh:mm a') }}</span>
                </div>
                <div v-for="(message, index) in messages" :key="index" class="bubble" :class="message.sender">
                    {{ message.text }}
                </div>
            </div>
            <div class="write">
                <a href="javascript:;" class="write-link attach"></a>
                <input id="txtNewMsg" autofocus v-model.trim="newMessage.text" @keypress.enter="sendMsg()" type="text" placeholder="Your message here" />
                <a href="javascript:;" class="write-link smiley"></a>
                <a @click="sendMsg()" href="javascript:;" class="write-link send"></a>
            </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
  name: 'Chat',
  data () {
    return {
      now: new Date(),
      timer: window.setTimeout,
      messages: [{
        text: 'Hello',
        sender: 'me',
        date: new Date()
      },
      {
        text: 'How are you',
        sender: 'me',
        date: new Date()
      }],
      newMessage: {
        text: '',
        sender: 'me'
      }
    }
  },
  methods: {
    sendMsg () {
      if (this.newMessage.text !== '') {
        this.newMessage.date = new Date()
        this.messages.push(this.newMessage)
        this.newMessage = {
          text: '',
          sender: 'me'
        }
        document.getElementById('txtNewMsg').focus()
        this.autoResponse()
      }
    },

    autoResponse () {
      window.clearTimeout(this.timer)
      this.timer = setTimeout(() => {
        let autoResponseMsg = {
          text: 'Thank you for your message',
          sender: 'you',
          date: new Date()
        }
        this.messages.push(autoResponseMsg)
      }, 5000)
    }
  }
}
</script>

<style>

</style>
