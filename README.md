  const detailEl = document.getElementById('weekendDetail');
  const dataMap = { '토':sat, '일':sun };
  document.querySelectorAll('#weekendStat .weekend-row').forEach(row=>{
    row.addEventListener('click', (e)=>{
      e.stopPropagation();
      const wd = row.dataset.wd;
      const alreadyOpen = detailEl.dataset.wd===wd;
      if(alreadyOpen){ detailEl.innerHTML=''; detailEl.removeAttribute('data-wd'); return; }
      detailEl.dataset.wd = wd;
      const list = dataMap[wd];
      if(!list.length){
        detailEl.innerHTML = `<p style="margin:10px 0 0;font-size:12px;color:var(--muted);">${wd}요일 근무 인원 없음</p>`;
      } else {
        const byTeam = {};
        list.forEach(r=>{ const t=r['부서명']||'기타'; (byTeam[t]=byTeam[t]||[]).push(r); });
        const teamBlocks = Object.keys(byTeam).sort().map(t=>{
          const rows = byTeam[t].map(r=>`${r['이름']}(${r['직급']})`).join('<br>');
          return `<p style="margin:0 0 4px;font-size:12px;font-weight:800;color:var(--navy);">${t}</p><p style="margin:0 0 8px;font-size:12px;color:var(--muted);">${rows}</p>`;
        }).join('');
        detailEl.innerHTML = `<div style="margin-top:12px;padding-top:12px;border-top:1px solid var(--border);"><p style="margin:0 0 8px;font-size:12.5px;font-weight:800;">${wd}요일 근무 (${list.length}명)</p>${teamBlocks}</div>`;
      }
    });
  });