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
  <div>로그인 하기</div>
  <button class="login-btn" on:click={loginWithGoogle}>
    <img
      class="google-img"
      src="https://img1.daumcdn.net/thumb/R1280x0.fjpg/?fname=http://t1.daumcdn.net/brunch/service/user/5rH/image/aFrEyVpANu07FvoBZQbIB4aF_uc"
      alt=""
    />
    <div>Google로 시작하기</div>
    <div />
  </button>
</div>

<style>
  .login-btn {
    margin-top: 10px;
    width: 200px;
    height: 30px;
    border: 1px solid gray;
    border-radius: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }

  .google-img {
    widows: 20px;
    height: 20px;
  }
</style>
