<script>
  import {Collection} from 'sveltefire'
  import AppendMessage from './AppendMessage.svelte'
  import {tick} from 'svelte'
  import * as animateScroll from 'svelte-scrollto'
  import marked from 'marked'
  import firebase from 'firebase/app'
  export let user

  
  async function newMessageScroll() {
    await tick()
    animateScroll.scrollToBottom()
  }
  let chatBox 
  let currentUser = firebase.auth().currentUser
  
  
  
</script>
<Collection path={'/chat'} let:ref={chatsRef} let:data={messages}  on:data={newMessageScroll}>
  <div class="box chat-box" id="chat-box" bind:this={chatBox}>
    {#each messages.sort((a,b) => a.date - b.date) as {message, uid, displayName}}

      <div class="notification {uid === currentUser.uid ? 'rgt' : 'lft'}">
        <div class="sender">
        {displayName}:
      </div> 
      <div class="message-content">
        {@html marked(message)}
      </div>
      </div>
    {/each}
  </div>
  <AppendMessage {chatsRef} {user} />
</Collection>