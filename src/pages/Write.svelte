<h2>내 물건 팔기</h2>
<form id="write-form">
  <div class="write-img__label">
    <label for="image">이미지</label>
    <div>
      <input type="file" id="image" name="image" />
    </div>
  </div>
  <div class="write-title__label">
    <label for="title">제목</label>
    <div>
      <input type="text" id="title" name="title" placeholder="제목" />
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
      />
    </div>
  </div>
  <div class="write-place__label">
    <label for="place">장소</label>
    <div>
      <input type="text" id="place" name="place" placeholder="거래 희망 장소" />
    </div>
  </div>
  <div id="write-btn">
    <button type="submit">작성 완료</button>
  </div>
</form>
