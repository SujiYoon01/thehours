=IF(A2="","",
IF(SUMPRODUCT(--ISNUMBER(SEARCH({"우주","항공","천문","위성"},A2)))>0,"A",
IF(SUMPRODUCT(--ISNUMBER(SEARCH({"기계","재료","신소재","금속","바이오","생명","제어","계측","로봇"},A2)))>0,"B",
IF(SUMPRODUCT(--ISNUMBER(SEARCH({"통신","전파","무선"},A2)))>0,"C",
IF(SUMPRODUCT(--ISNUMBER(SEARCH({"전기","전자","컴퓨터","전산","통계","소프트웨어","반도체"},A2)))>0,"D","E")))))
