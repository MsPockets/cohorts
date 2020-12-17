<script>
  import {Collection} from 'sveltefire'
  import AppendMessage from './AppendMessage.svelte'
  import {tick} from 'svelte'
  import * as animateScroll from 'svelte-scrollto'
  export let user

  async function newMessageScroll() {
    console.log('data received')
    await tick()
    animateScroll.scrollToBottom()
  
  }
  let chatBox 
</script>
<Collection path={'/chat'} let:ref={chatsRef} let:data={messages}  on:data={newMessageScroll}>
<div class="box chat-box" id="chat-box" bind:this={chatBox}>
    {#each messages.sort((a,b) => a.date - b.date) as {message}}
      <div class="notification">
        {user.name}:{message}
      </div>
    {/each}
  </div>
  <AppendMessage {chatsRef} {user} />
</Collection>