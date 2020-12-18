<script>
  export let auth
  let mode = "signIn"
  let email = ''
  let password = ''
  let displayName = ''

  async function handleSubmit() {
    if(mode == 'signIn') {
      await auth.signInWithEmailAndPassword(email, password)
    } else{
      await auth.createUserWithEmailAndPassword(email, password).then(function(result) {
  return result.user.updateProfile({
    displayName: displayName
  })
}).catch(function(error){})
    }
    email = ''
    password = ''
    displayName = ''
  }
</script>

<h1 class="title has-text-info has-text-centered">Cohorts</h1>
<h2 class="title">{mode === 'signIn' ? 'Sign In' : 'Sign Up'}</h2>
<form on:submit|preventDefault={handleSubmit} class="auth-form">
  <div class="field">
    <label for="" class="label">Email</label>
    <input type="email" class="input" required bind:value={email}/>
  </div>
  <div class="field {mode === 'signIn' ? 'sign-in' : 'sign up'}">
    <label for="" class="label" placeholder="What would you like us to call you?">Display Name</label>
    <input type="displayName" class="input" bind:value={displayName}/>
  </div>
  <div class="field">
    <label for="" class="label">Password</label>
    <input type="password" class="input" minlength="6" required bind:value={password}/>
  </div>
  <div class="field">
    <button type="submit">Enter Chat</button>
  </div>
</form>
<hr>
{#if mode === 'signIn'}
  <p >
    If you dont have an account yet, 
    <span class="has-text-link" on:click={() => (mode = 'signUp')}>Sign Up!</span>
  </p>
{:else}
  <p>
    Already have an account? 
    <span style="color: white;" class="has-text-link" on:click={() => (mode = 'signIn')}>Sign In!</span>
  </p>
{/if}