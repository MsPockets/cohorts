<script>
  import {Collection} from 'sveltefire'
  import AppendMessage from './AppendMessage.svelte'
  export let user
</script>
<Collection path={'/chat'} let:ref={chatsRef} let:data={messages}>
  <div class="box chat-box">
    {#each messages.sort((a,b) => a.date - b.date) as {message}}
      <div class="notification">
        {message}
      </div>
    {/each}
  </div>
  <AppendMessage {chatsRef} {user} />
</Collection>