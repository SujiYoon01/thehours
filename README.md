document.getElementById('weekendStat').innerHTML = `
    <div class="weekend-row" data-wd="토" style="cursor:pointer;"><div><div class="wname">토요일 근무</div><div class="wsub">이번 달 평균 ${fmt1(satAvg)}시간 · 클릭 시 명단</div></div><div class="wnum">${sat.length}명</div></div>
    <div class="weekend-row" data-wd="일" style="cursor:pointer;"><div><div class="wname">일요일 근무</div><div class="wsub">이번 달 평균 ${fmt1(sunAvg)}시간 · 클릭 시 명단</div></div><div class="wnum">${sun.length}명</div></div>
    <div id="weekendDetail"></div>`;
