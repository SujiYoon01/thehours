<button class="load-btn" id="empSearchBtn">검색</button>
<button class="load-btn steel" id="empSearchResetBtn" style="background:var(--muted);">초기화</button>



document.getElementById('empSearchResetBtn').addEventListener('click', ()=>{
  document.getElementById('empSearchInput').value = '';
  document.getElementById('empSearchResult').innerHTML = '';
});
