<script>
  import { getDatabase, ref, push } from "firebase/database";
  import {
    getStorage,
    ref as refImage,
    uploadBytes,
    getDownloadURL,
  } from "firebase/storage";
  import Nav from "../components/Nav.svelte";

  let title;
  let price;
  let description;
  let place;
  let files;

  const storage = getStorage();
  const db = getDatabase();

  async function writeUserData(imgUrl) {
    push(ref(db, "items/"), {
      title,
      price,
      description,
      place,
      insertAt: new Date().getTime(),
      imgUrl,
    });
    alert("게시물 등록완료!");
    window.location.hash = "/";
  }

  const uploadFile = async () => {
    const file = files[0];
    const name = file.name;
    const imgRef = refImage(storage, name);
    await uploadBytes(imgRef, file);
    const url = await getDownloadURL(imgRef);
    return url;
  };

  const handleSubmit = async () => {
    const url = await uploadFile();
    writeUserData(url);
  };
</script>

<h2>내 물건 팔기</h2>
<form id="write-form" on:submit|preventDefault={handleSubmit}>
  <div class="write-img__label">
    <label for="image">이미지</label>
    <div>
      <input type="file" bind:files id="image" name="image" />
    </div>
  </div>
  <div class="write-title__label">
    <label for="title">제목</label>
    <div>
      <input
        type="text"
        id="title"
        name="title"
        placeholder="제목"
        bind:value={title}
      />
    </div>
  </div>
  <div class="write-price__label">
    <label for="price">가격</label>
    <div>
      <input
        type="number"
        id="price"
        name="price"
        placeholder="₩ 가격을 입력해주세요."
        bind:value={price}
      />
    </div>
  </div>
  <div class="write-description__label">
    <label for="description">자세한 설명</label>
    <div>
      <input
        type="text"
        id="description"
        name="description"
        placeholder="내용을 작성해주세요"
        bind:value={description}
      />
    </div>
  </div>
  <div class="write-place__label">
    <label for="place">장소</label>
    <div>
      <input
        type="text"
        id="place"
        name="place"
        placeholder="거래 희망 장소"
        bind:value={place}
      />
    </div>
  </div>
  <div id="write-btn">
    <button type="submit">작성 완료</button>
  </div>
</form>

<Nav location="write" />
