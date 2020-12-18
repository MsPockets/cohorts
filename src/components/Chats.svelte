<script>
  import {Collection} from 'sveltefire'
  import AppendMessage from './AppendMessage.svelte'
  import {tick} from 'svelte'
  import * as animateScroll from 'svelte-scrollto'
  import marked from 'marked'
  export let user

  
  async function newMessageScroll() {
    await tick()
    animateScroll.scrollToBottom()
  }
  let chatBox 
  
      
</script>
<Collection path={'/chat'} let:ref={chatsRef} let:data={messages}  on:data={newMessageScroll}>
<div class="box chat-box" id="chat-box" bind:this={chatBox}>
    {#each messages.sort((a,b) => a.date - b.date) as {displayName, message}}
    
      <div class="notification">
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