<script>
  export let auth
  let mode = "signIn"
  let email = ''
  let password = ''

  async function handleSubmit() {
    if(mode == 'signIn') {
      await auth.signInWithEmailAndPassword(email, password)
    } else{
      await auth.createUserWithEmailAndPassword(email, password)
    }
    email = ''
    password = ''
  }
</script>

<h1 class="title has-text-info has-text-centered">Cohorts</h1>
<h2 class="title">{mode === 'signIn' ? 'Sign In' : 'Sign Up'}</h2>
<form on:submit|preventDefault={handleSubmit}>
  <div class="field">
    <label for="" class="label">Email</label>
    <input type="email" class="input" required bind:value={email}/>
  </div>
  <div class="field">
    <label for="" class="label">Password</label>
    <input type="password" class="input" required bind:value={password}/>
  </div>
  <div class="field">
    <button type="submit">Enter Chat</button>
  </div>
</form>
<hr>
{#if mode === 'signIn'}
  <p>
    If you dont have an account yet, 
    <span class="has-text-link" on:click={() => (mode = 'signUp')}>Sign Up!</span>
  </p>
{:else}
  <p>
    Already have an account? 
    <span class="has-text-link" on:click={() => (mode = 'signIn')}>Sign In!</span>
  </p>
{/if}