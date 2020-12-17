<script>
  import { FirebaseApp, User } from 'sveltefire'
  import firebase from 'firebase/app'
  import 'firebase/firestorm'
  import 'firebase/firestore'
  import 'firebase/auth'
  import AuthForm from './components/AuthForm.svelte'
  import Chats from './components/Chats.svelte'
  const firebaseConfig = {
    apiKey: "AIzaSyCtQlZvurYwe_UvrcXrueYZdmgJn30iDlY",
    authDomain: "cohorts-78505.firebaseapp.com",
    projectId: "cohorts-78505",
    storageBucket: "cohorts-78505.appspot.com",
    messagingSenderId: "365130822291",
    appId: "1:365130822291:web:5fd3202ae42ee4f4c49366",
    measurementId: "G-E8H2BML7FQ"
  };
  firebase.initializeApp(firebaseConfig);
</script>

<style>
  .app {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    max-height: 100vh;
  }
</style>
<main class="containter section app">
	<FirebaseApp {firebase} >
    <User let:user let:auth>
      <Chats {user} />
        <button style="top: 0px; right: 0px; position: fixed;" class="button" on:click={() => auth.signOut()}>Sign Out</button>
      <div slot="signed-out">
      <AuthForm {auth} />
      </div>
    </User>
  </FirebaseApp>
</main>