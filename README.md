function renderTeamLoadSummary(latestRows, currentRows){
  const riskMap = computeRiskIdSet(currentRows);
  const riskByTeam = {};
  riskMap.forEach(p=>{ riskByTeam[p.team] = (riskByTeam[p.team]||0) + 1; });

  const byTeam = {};
  latestRows.forEach(r=>{ const t=r['부서명']; if(!t) return; (byTeam[t]=byTeam[t]||[]).push(r); });

  const teams = sortByOrgOrder(Object.keys(byTeam));
  document.getElementById('teamLoadBody').innerHTML = teams.map(t=>{
    const arr = byTeam[t];
    const avg = arr.reduce((s,r)=>s+r._Q,0)/arr.length;
    const overCount = arr.filter(r=>r._Q>=52).length;
    const overRatio = arr.length ? overCount/arr.length*100 : 0;
    const weekendCount = arr.filter(r=>numH(r['토'])>0 || numH(r['일'])>0).length;
    const riskCount = riskByTeam[t] || 0;
    const color = colorForHourStep(avg);
    return `<tr>
      <td>${t}</td>
      <td style="color:${color};font-weight:800;">${fmt1(avg)}</td>
      <td>${fmt1(overRatio)}% (${overCount}명)</td>
      <td>${riskCount>0?`<span class="tag w3">${riskCount}명</span>`:'0명'}</td>
      <td>${weekendCount}명</td>
    </tr>`;
  }).join('') || '<tr><td colspan="5" style="color:var(--muted);">데이터가 없습니다.</td></tr>';
}

