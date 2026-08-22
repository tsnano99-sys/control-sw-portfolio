# Kim Taeseung — Control Software Engineer Portfolio

반도체·디스플레이 장비의 통신·모션 제어 SW를 개발하는 엔지니어입니다. 약 5년간 TCP/IP·RS-232/485·SECS/GEM 기반 장비-호스트 통신과 다축 정밀 모션 제어 시스템을 설계·구현해왔습니다.

📧 tsnano99@gmail.com

---

## Core Competencies

- **다축 정밀 모션 제어** — 30축 이상 동기 제어, 1μm 이하 정밀 위치 제어 시스템 설계·구현
- **통신 프로토콜 기반 장비 제어 SW** — TCP/IP·RS-232/485, 재시도·타임아웃 로직으로 통신 안정성 확보
- **SECS/GEM·MES 표준 연동** — 장비-호스트 통신 안정화, 알람 체계 개선
- **생산성 개선** — 시퀀스 최적화를 통한 처리량(UPH) 향상
- **해외 현장 대응** — 클린룸 장비 셋업·양산 대응 경험
- **자기주도적 도구 개발** — 현장 문제를 직접 발굴해 단독 기획·구현

## Tech Stack

| 분류 | 내용 |
|---|---|
| Languages | C++, C#(.NET), Python |
| Communication | TCP/IP, RS-232, RS-485, SECS/GEM, SCPI |
| Data | MySQL, SQLite |
| Tools | Git, SVN, Bitbucket, Jira, Visual Studio |
| Others | OpenGL, XML 기반 레시피 관리, 비동기 처리(async/await), LLM API 연동(OpenAI/Claude) |

## Experience Summary

| 기간 | 회사 | 주요 업무 |
|---|---|---|
| 2026.03 ~ 현재 | 에이피텍 | 자동화 장비 제어 SW — 통신 안정화, 시퀀스 최적화, 자체 진단 도구 개발 |
| 2024.02 ~ 2026.02 | 코세스 | 레이저·스캐너 제어 응용 애플리케이션 개발 |
| 2022.01 ~ 2023.03 | 이오테크닉스 | 레이저 드릴링 장비 다축 모션 제어, 해외 클린룸 셋업 |
| 2020.07 ~ 2021.09 | 테크윙 | 메모리 핸들러 장비 제어 로직 개발·트러블슈팅 |

---

## Projects

### 1. Automatic Serial Device Discovery Tool

**Context**: 다종 시리얼 장비가 혼재된 현장에서, 어떤 COM 포트에 어떤 장비가 연결됐는지 수작업으로 확인하며 발생하던 휴먼에러를 해결하기 위해 단독 기획·설계·구현

**Approach**
- COM 포트 × Baudrate 조합을 이차 순회하며 장비별 식별 커맨드를 송수신(cmd → response → validate)해 자동으로 연결 장비를 판별
- 프로브(Probe) 패턴으로 장비별 인식 로직을 모듈화 → 재컴파일 없이 현장에서 신규 장비 통신 규격 등록 가능하도록 설계
- 비동기(async/await) 처리로 다중 포트를 동시에 스캔하면서도 UI 응답성 확보

**Conceptual flow** *(개념 설명용 의사코드, 실제 구현 아님)*
```
for each COM port:
    for each candidate baudrate:
        open connection
        send identify_command
        response = read_response(timeout)
        if validate(response) matches known device signature:
            register device(port, baudrate, device_type)
```

**Result**: 신규 장비 도입 시에도 코드 수정 없이 현장에서 바로 대응 가능한 구조 확보, 수작업 확인 과정에서 발생하던 인식 오류 제거

---

### 2. Log Analysis Tool with AI-assisted Diagnostics

**Context**: 대용량 장비 로그를 사람이 직접 열어 검색하며 에러 원인을 찾던 방식의 비효율을 해결하기 위해 단독 기획·설계·구현

**Approach**
- 로그 파일을 구조화된 DB로 파싱·저장, 시간/레벨/모듈/키워드 기반 검색·필터링 지원
- 로그 레벨별 자동 탭 분리, 실시간 모니터링(파일 변경 감지 시 알림)
- LLM API(OpenAI/Claude)를 연동해 에러 로그의 원인을 자동으로 요약·진단하는 기능 추가
- 별도 스크립트로 통계 리포트를 자동 생성해 트렌드 파악 지원

**Result**: 로그 분석에 걸리던 수작업 시간을 크게 단축, AI 기반 1차 진단으로 초기 원인 파악 속도 향상

---

### 3. Precision Pin-Placement Visualization Tool

**Context**: 가공 시 고정핀 배치 데이터를 시각적으로 표현하고, 배치 간 간섭(Overlap)을 자동으로 검증할 수단이 없어 발생하던 수작업 오류를 줄이기 위해 개발

**Approach**
- 2D 그래픽 라이브러리 기반으로 레이어별 핀·기준점·리드·컴포넌트를 시각화
- 배치 간 Overlap 발생 시 자동으로 색상 경고 표시
- 업계 표준 설계 파일 포맷(DXF, Gerber) Import/Export 지원

**Result**: 수작업 검증 시간과 초기 설정 오류율을 큰 폭으로 감소

---

### 4. Sensor Signal Stabilization (Load Cell)

**Context**: 로드셀 측정값이 헌팅(hunting) 현상을 보이며 출력 신뢰도가 떨어지는 문제 발생

**Approach**
- 시그마 필터링으로 이상치(outlier)를 1차 제거
- 선형회귀 기반 보정 로직을 추가해 출력값을 안정화

**Result**: 노이즈가 심하던 원시 센서 데이터를 신뢰할 수 있는 수준으로 안정화

---

### 5. Equipment Communication Reliability Improvement

**Context**: 다품종 장비 운용 현장에서 바코드·레이저 통신이 불안정해지는 이슈가 반복적으로 발생

**Approach**
- 통신 실패 시 재시도(retry) 로직과, 연결 종료 시점의 예외 상황을 로그로 남기는 추적 체계 구축
- MES SECS/GEM 통신 이슈는 시나리오 분석을 통해 보고 시점을 조정하고, 문제 상황별로 알람을 분기 처리

**Result**: 통신 장애 발생 시 원인 추적이 가능해지고, 상황별 대응 체계 확보

---

## Note

- 위 프로젝트는 실제 재직 중 수행한 업무를 기반으로 하되, 소스코드는 회사 자산이라 공개하지 않으며 접근 방식과 결과 중심으로 정리했습니다.
- 코드 예시는 실제 구현이 아닌 개념 설명을 위한 일반화된 의사코드입니다.
