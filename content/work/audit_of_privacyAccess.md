﻿---
title: "개인정보처리시스템 접속기록 검토"
date: 2020-03-19T17:53:18+09:00
---
# 개인정보처리시스템의 접속기록은 어떻게 검토하고 있는가?

## 논의안건 

개인정보처리시스템의 접속기록은 매월 1회 검토하여야 하며, 반드시 포함되어야 하는 항목이 기록되어야 한다. 각사의 개인정보접근권한 검토는 어떤 방식으로 진행되고 있는지, 어느 방안이 효율적인지, 작성된 의견들과 재직중인 회사와 비교 시 고도화 시킬 수 있는 부분이 있다면 고려해보도록 하자
※ 회사명은 오픈하지 않도록 한다.
※ 안건에 대한 의견은 댓글에 기재한다.

<br>
  
**ISMS 2.9.4**
개인정보처리시스템에 대한 접속기록은 법적 요구사항을 준수할 수 있도록 필요한 항목을 모두 포함하여 일정기간 안전하게 보관하고 있는가?

개인정보처리시스템 접속기록에 반드시 포함되어야 할 항목
- 계정 또는 식별자: 개인정보취급자 아이디 등
- 접속일시: 접속날짜 및 시분초  
- 접속지 정보: 접속자 IP주소 등  
- 수행업무: 개인정보 조회, 변경, 입력, 삭제, 다운로드 등

개인정보 접속기록 보존기간
- 개인정보처리자 및 정보통신서비스 제공자: 최소 1년 이상  
- 단 전기통신사업법에 따른 기간통신사업자는 최소 2년 이상 보존 필요  

개인정보 접속기록이 위/변조, 도난, 분실되지 않도록 안전하게 보관 필요  
접속기록의 안전한 보관방법 (예시) 
- 물리적으로 분리된 별도의 저장장치에 백업 보관  
- DVD, WORK Disk등 덮어쓰기가 방지된 저장매체에 보존 등

<br>

**ISMS 2.9.5**
개인정보처리시스템의 접속기록은 관련 법령에서 정한 주기에 따라 정기적으로 점검하고 있는가?
- 법령에 따른 개인정보 접속기록 점검 주기: 월 1회



## 이하 기존 위키독 댓글
**borylee**
모든 개인정보처리시스템의 로깅 및 접속기록 검토는 아래와 같이 수행되고 있음  
1. 로깅: SystemName, Date, ID, IP, Action(로그인, 로그아웃, 다운로드, 삭제, 추가, 조회 등), Parameter  
2. 수집: ELK  
3. 조회: 시스템별 Action값의 로그인 부분 조회 후 이상유무 검토  
4. 이상유무 기준: 야근을 고려한 업무시간+@ 외에 기타 시간에 접속한 외부인  
  
아쉬운점: 접속기록 검토를 한다면 어떤 기준으로 체크 및 운영이 되어야 정말 효과적인 방법일까 고민하고 있음

<br> 

**noname003**
구형 시스템의 연동 한계점으로 인하여 개인정보처리시스템이 여러개로 분산되어 있으며, 별도의 접속기록 관리 솔루션을 이용하지 않음  
1. 로깅 : (웹) 사용자ID, 접근IP, 접근메뉴, 실행명령, 처리시각, 정보주체ID 로 구분됨. (모든 시스템이 그렇진 않음)  
(DB) DB Safer 연동으로 기록, 정책 설정 후 임계 값 초과 시 알람 전송  
2. 조회 : (웹) 로그 데이터 Table 호출(엑셀 변환 옵션 제공)  
(DB) DB Safer 리포팅 조회  
3. 이상유무 기준 : (웹)가용 업무시간 범위(09:00~22:00) 외 시스템 접속, 다운로드 시 허가받지 않은 매칭코드 입력/매칭코드의 중복사용, 권한의 오/남용(점검자인 PM이 자가판단), 인쇄기록 발생  
(DB) DB Safer 임계치 초과한 로그 분석(업무시간 외 처리, 평상시에 비해 과도한 처리, 업무범위 외 DB 접근)  
  
아쉬운점 : 통합로그솔루션을 이용하고 싶으나, 네트워킹 성능도 좋지 않고 예산 인가 나지 않음. 구형 시스템을 구축한 개발자들이 줄 퇴사하여 통합 DB로 마이그레이션하는 작업을 하려면 공수가 많이 든다고... 개발부서에서 격렬하게(?) 반대, 접속기록을 전문적으로 분석할 요원 부족으로 PM의 양심에 맡기는 사용자 단 자체점검 프로세스 구성(1년 1회 정기 감사시 로그 싹 뽑아서 PM이 제출한 내역과 비교 검사 하는 수순에서 대응)

<br>

**ahdtnpf**
개인정보처리시스템별 담당자가 상이하며, 취합에 어려움이 있음.  
로깅 및 접속기록 검토/백업은 아래와 같이 수행하고 있음  
1. 로깅 : id, 접속ip, 시간, 접근메뉴, 개인정보 다운로드 여부(+사유), 슈퍼관리자의 권한 부여 이력  
2. 조회 : 담당자가 웹으로 조회할 수 없음. 개발자에게 로그 요청  
3. 이상유무 기준 : 접속 시간, 다량 다운로드, 권한 차등화 안됨  
  
아쉬운점 : 로그에 대한 백업이 잘되고 있는지 확인하기 어려우며, 이상유무의 확인이 실제적으로 꼼꼼히 이루어지지 않고, 보고서 제출용도로 복붙하는 의미없는 행위로 보여짐.. 어떻게 해야 법적으로 요구하는 상황의 목적에 맞게 운영할 수 있을까 고민됨..
