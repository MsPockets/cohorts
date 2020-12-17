<script>
  export let chatsRef
  export let user
  let message =''

  async function appendMessage() {
    if(!message) return
    await chatsRef.add({
      message, 
      uid: user.uid, 
      date: Date.now(),
    })
    message =''
  }
</script>
<form class="chat-bar" on:submit|preventDefault={appendMessage}>
  <div class="field has-addons box">
    <div class="control is-expanded message-form">
      <input type="text" class="input" bind:value={message}/>
    </div>
    <div class="control message-form">
      <input type="submit" class="is-info" value="⌲ Send"/>
    </div>
  </div>
</form>