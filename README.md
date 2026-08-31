const EMBEDDED_CSV = ``; // 완성파일/필터저장 시 실제 데이터로 교체됨
const EMBEDDED_PREV_CSV = ``; // 전월 비교 데이터 임베딩용


let CURRENT_CSV_TEXT = '';
let PREV_CSV_TEXT = '';



PREV_RAW_ROWS = parsed.data.filter(r=>r['사번']);
PREV_CSV_TEXT = text;



  if(PREV_CSV_TEXT){
    const escPrev = PREV_CSV_TEXT.replace(/\\/g,'\\\\').replace(/`/g,'\\`').replace(/\$\{/g,'\\${');
    const markerPrev = 'const EMBEDDED_PREV_CSV = `';
    const startPrev = html.indexOf(markerPrev);
    if(startPrev!==-1){
      const closeIdxPrev = html.indexOf('`;', startPrev+markerPrev.length);
      html = html.slice(0,startPrev) + markerPrev + escPrev + html.slice(closeIdxPrev);
    }
  }
  downloadHtml(html, '우주사업총괄_근무실적현황.html');


if(EMBEDDED_CSV.trim()){ loadFromText(EMBEDDED_CSV, '내장된 데이터'); }
if(EMBEDDED_PREV_CSV.trim()){
  const parsedPrev = parseCSV(EMBEDDED_PREV_CSV);
  PREV_RAW_ROWS = parsedPrev.data.filter(r=>r['사번']);
  PREV_RAW_ROWS.forEach(r=>{ if(DEPT_MERGE[r['부서명']]) r['부서명']=DEPT_MERGE[r['부서명']]; });
  PREV_CSV_TEXT = EMBEDDED_PREV_CSV;
  document.getElementById('prevDataStatus').textContent = '전월 비교 데이터: 내장된 데이터';
  render();
}
