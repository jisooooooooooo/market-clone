<script>
  import { getAuth, signInWithPopup, GoogleAuthProvider } from "firebase/auth";
  import { user$ } from "../store";

  const provider = new GoogleAuthProvider();
  const auth = getAuth();

  const loginWithGoogle = async () => {
    try {
      const result = await signInWithPopup(auth, provider);
      const credential = GoogleAuthProvider.credentialFromResult(result);
      const token = credential.accessToken;
      const user = result.user;
      user$.set(user);
      localStorage.setItem("token", token);
    } catch (error) {
      console.error(error);
    }
  };
</script>

<div>
  <div>로그인하기</div>
  <button class="login-btn" on:click={loginWithGoogle}>
    <img
      class="google-img"
      src="https://www.google.com/imgres?imgurl=https%3A%2F%2Fw7.pngwing.com%2Fpngs%2F326%2F85%2Fpng-transparent-google-logo-google-text-trademark-logo.png&tbnid=C9E-hMMdtZ9C1M&vet=12ahUKEwiZgNPuw_v_AhXYlFYBHXhhB0wQMygAegUIARDDAQ..i&imgrefurl=https%3A%2F%2Fwww.pngwing.com%2Fen%2Fsearch%3Fq%3Dgoogle&docid=x9RjsNPWmgLssM&w=920&h=900&q=googlepng&ved=2ahUKEwiZgNPuw_v_AhXYlFYBHXhhB0wQMygAegUIARDDAQ"
      alt=""
    />
    <div>Google로 시작하기</div>
  </button>
</div>

<style>
  .login-btn {
    width: 200px;
    height: 50px;
    border: 1px solid gray;
    display: flex;
    justify-content: space-between;
    align-items: center;
    cursor: pointer;
    border-radius: 3px;
  }

  .google-img {
    width: 20px;
  }
</style>
