<script>
  export let chatsRef
  export let user
  let message =''

  async function appendMessage() {
    if(!message) return
    await chatsRef.add({
      message, 
      displayName: user.displayName,
      uid: user.uid, 
      date: Date.now(),
    })
    message =''
  }
</script>
<form class="chat-bar" on:submit|preventDefault={appendMessage}>
  <div class="field has-addons box">
    <div class="control is-expanded message-form">
      <input type="text" class="input message-bar" bind:value={message}/>
    </div>
    <div class="control message-form">
      <input type="submit" class="is-info send" value="⌲ Send"/>
    </div>
  </div>
</form>