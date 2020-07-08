<script>
import At from "vue-at";

export default {
  components: { At },

  data () {
    return {
      text: Node,
      users: [
  {
    value: '123',
    firstName: 'Bjarte Amadeus',
  },
  {
    value: '431',
    firstName: 'Konstanse Beatrix',
  },
  {
    value: '527',
    firstName: 'Sébastien',
  },
],
    }
  },

  methods: {  
    onInsert(e) {
      console.log("item", e);
    },
    onMentions(e) {
      console.log("onMentions", e);
    },
    transform() {
      console.log(this.$refs.editor.innerText);
      this.$refs.editor.querySelectorAll('span.tagged').forEach(el => {             
        el.textContent = "{{"+el.getAttribute('data-id')+"}}"
      })

    }
  }
}
</script>

<template>
  <div>
  <h1>lol123</h1>
  <at v-model="text" :members="users" name-key="firstName" @at="onMentions" @insert="onInsert" @input="onChange">
    <template slot="embeddedItem" slot-scope="s">
      <span class="tag">
        <span :data-id="s.current.value" class="tagged">@{{s.current.firstName}}</span>
      </span>
    </template>

    <button @click="transform">SEND</button>

    <div ref="editor" id="lol" class="message" contenteditable></div>
  </at>
  </div>
</template>

  

<style scoped>
.demo {
  margin: 24px 0;
}

.tagged {
  color: #127dac;
  font-weight: 600;
}

.message {
  width: 100%;
  border: #ccc 1px solid;
  border-radius: 6px;
  resize: vertical;
  min-height: 42px;
  padding: 12px;
  box-sizing: border-box;
  line-height: 1.2em;
  font-size: inherit;
}

.user,
.issue {
  padding: 4px 6px;
  border-radius: 4px;
  cursor: pointer;
}

.mention-selected .user {
  background: rgb(192, 250, 153);
}

.mention-selected .issue {
  background: rgb(139, 212, 255);
}

.issue .number {
  font-family: monospace;
}

.dim {
  color: #666;
}

.preview {
  font-family: monospace;
  white-space: pre-wrap;
  margin-top: 12px;
  padding: 12px;
  background: #f8f8f8;
  border-radius: 6px;
}
</style>
