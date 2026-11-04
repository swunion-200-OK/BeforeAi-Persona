
# 노스브리지시스템즈코리아 유한회사 (Northbridge Systems Korea Ltd.)

경기도 화성시 동탄 (가상 주소) / 대표전화 031-000-0000 / Procurement procurement.kr@northbridge.example
미국 Northbridge Systems, Inc.의 한국 법인입니다. 본 공문은 한국어 본문을 정본으로 하며, 당사 본사 공유용 영문 요약(English Summary)을 붙임 3으로 함께 보냅니다.

---

| 항목 | 내용 |
| --- | --- |
| 문서번호 | NBK-PROC-2026-1106-01 |
| 시행일자 | 2026. 11. 6. (금) |
| 수신 | BeforeAI 서비스 개발 담당 |
| 참조 | BeforeAI 영업 담당, 기술 지원 담당 |
| 발신 | 노스브리지시스템즈코리아 유한회사 Finance & Admin 본부 Procurement |
| 당사 내부 참조 | APAC Procurement Lead, Global Vendor Risk Management(VRM), APAC Engineering Director |
| 제목 | AI 작업 통제 서비스(BeforeAI) 도입 검토 결과 통보 및 Limited Pilot 착수 자료·기능 요청 |

---

1. 귀사의 무궁한 발전을 기원합니다.

2. 관련
   - 가. 귀사 서비스 소개 미팅 및 데모 (2026. 10. 마지막 주)
   - 나. 귀사 제공 「API 명세서(기능 명세서 결정 사항 반영본)」 (이하 "명세")
   - 다. 당사 내부 도입 검토 회의 (2026. 11. 4.(수))
   - 라. 당사 구매 담당 메일 「설치형 배포 가능 여부 질의」 (2026. 11. 4.(수))

3. 결론

   | 구분 | 내용 |
   | --- | --- |
   | 결론 | **조건부 도입** |
   | 범위 | **한국 법인 한정 Limited Pilot. 정식 채택이 아님** |
   | 착수 조건 | **① 파일럿 범위에 대한 당사 본사 VRM 승인 ② 당사 Pilot Agreement 체결 ③ 당사 IT·보안 예외 승인(로컬 계정, Tailscale) ④ 필요 시 당사 Architecture Review Board(ARB) 예외 승인. 네 가지가 모두 끝나기 전에는 설치·연결을 시작하지 않음** |
   | 성격 | **본 공문은 구매 약정(purchase commitment)이 아니며, 정식 계약과 글로벌 확대(당사 싱가포르·미국 등 타 법인 사용)는 파일럿 결과와 6항의 조건 충족 여부를 보고 별도로 결정함** |

   - 귀사 영업 담당께서 알려 오신 "2026. 11. 16. 설치 시작" 일정은 **당사 확정 일정이 아닙니다.** 당사 목표 일정은 붙임 1과 같으며, 이 또한 착수 조건 충족을 전제로 한 목표일입니다.
   - "조건부 도입"이 파일럿 단계를 뜻한다는 점을 귀사 회신 담당자께서 메일로 확인해 주시기 바랍니다.

4. 검토 사유 (귀사 서비스를 파일럿 대상으로 정한 이유)

   | 번호 | 기능 | 명세 근거 | 당사 평가 |
   | --- | --- | --- | --- |
   | 1 | 실행기가 Plan 해시를 직접 만들고 웹 서비스가 보낸 해시를 쓰지 않음 | 2.3, 5장 | 웹 서비스가 침해되어도 승인받지 않은 Plan이 실행되지 않는 구조로, 당사가 막으려는 사고 유형(엔지니어 자격 증명으로 AI 에이전트가 직접 실행)에 맞음 |
   | 2 | 승인자 기기 키(Ed25519)로 서명하고 실행기 공개키로 HPKE 암호화해 전달 | 2.4, 4.5 | 중간 경로에서 서명을 위조·교체할 수 없음 |
   | 3 | 서명별 1회용 nonce 소진 | 2.4, 5.1 | 같은 승인으로 두 번 실행되지 않음 |
   | 4 | 실행기 검증 6단계와 실패 사유 코드(`failedChecks`) | 5.1 | 실패 원인을 코드로 받아 당사 경보 체계에 연결 가능 |
   | 5 | 킬 스위치와 전사 일괄 중단이 서명 없이 즉시 동작 | 4.6, 3.2 | 장애 확산을 짧은 시간 안에 멈출 수 있음 |
   | 6 | 외부망에서는 CODE_MINOR·CODE_FEATURE만 승인 가능 | 3.6, 4.4 | 원격 근무 중 스테이징 배포 승인을 막음 |
   | 7 | 웹 코드 에디터 변경도 승인·서명 절차를 거침 | 3.8, 4.7 | 우회 경로가 없음 |
   | 8 | 금지 규칙 해제는 실행기 로컬 콘솔에서만 반영 | 3.4, 5장 | 원격에서 안전장치를 해제할 수 없음 |
   | 9 | 실행기 연결 실패 시 `502 EXECUTOR_UNAVAILABLE`, 요청 상태 유지 | 4.3 | 연결 장애가 승인 우회로 이어지지 않음 |
   | 10 | 시각 ISO 8601(UTC) 기록, Slack 알림 연동 | 1.1, 3.1, 3.2 | 당사 글로벌 표준(Slack Enterprise Grid)과 시차가 있는 조직에 맞음 |

5. 정식 도입 보류 사유 (현재 충족되지 않아 정식 계약을 할 수 없는 항목)

   당사는 미국 본사 정책에 따라, 소스코드 저장소와 스테이징 환경에 접근하는 업체를 VRM **Tier 1**으로 분류합니다. Tier 1 업체는 계약 금액과 관계없이 본사 Global VRM 승인이 필요하며, 아래 항목이 확인되지 않으면 정식 계약을 할 수 없습니다.

   | 번호 | 항목 | 현재 상태 | 사유 |
   | --- | --- | --- | --- |
   | 1 | SOC 2 Type II 또는 ISO 27001 | 확인 불가 | 보유 여부 자료를 받지 못함. 미보유 시 보완 패키지(SOC 2 Type I 일정 확약 + 외부 모의해킹 보고서)는 당사 Global VRM의 서면 예외 승인 대상이며, 당사가 수용을 약속할 수 없음 |
   | 2 | 데이터 처리 계약(DPA)과 데이터 저장 위치 | 확인 불가 | 웹 서비스·DB·감사 로그·백업의 위치, AI 분석 시 소스코드·프롬프트의 전송 경로와 보관·학습 정책이 명세에 없음. 일부 당사 기술 데이터는 미국 수출관리규정(EAR) 대상이라 외부 전송 여부 확인이 필수 |
   | 3 | 기업 SSO (Okta, SAML 2.0 또는 OIDC) | 미충족 | 명세 3.1 `POST /auth/login`은 사번·비밀번호 로그인만 정의 |
   | 4 | 감사 로그의 회사 보관 (파일 내보내기, SIEM 전송) | 미충족 | 명세 3.9 `GET /audit-logs`는 검색만 제공 |
   | 5 | 본사 계약 양식(MSA) 수용, USD 송장, 사이버 보험 USD 5M, 재무 안정성 | 확인 불가 | 관련 자료 미수령 |

6. 우려 사항

   | 번호 | 내용 | 명세 근거 | 당사 우려 |
   | --- | --- | --- | --- |
   | 1 | 내부망 로그인은 OTP 없이 비밀번호만 | 1.1, 3.1 | 파일럿 로컬 계정에도 OTP를 강제할 수 있어야 함 |
   | 2 | 접속 환경을 출발지 IP로 판별 | 1.1 | 당사는 ZTNA(Zscaler)를 쓰므로 원격 접속의 출발지 IP가 공용 egress로 보임. 이를 회사 대역에 넣으면 외부망 제한이 무력화되고, 넣지 않으면 지역 사무소도 외부망으로 판별됨 |
   | 3 | 실행기 연결에 Tailscale 사용 | 1.1, 5장 | Tailscale은 당사 표준 도구가 아니어서 예외 승인이 필요함. 대체 구성 가능 여부 확인 필요 |
   | 4 | 작업 요청 생성이 내부망 전용 | 3.5 `POST /requests` | 지역이 다른 엔지니어가 원격에서 요청을 만들 수 없음 (`403 INTERNAL_NETWORK_ONLY`) |
   | 5 | 승인 서명에 만료 없음, 필요한 서명이 모이면 자동 실행 | 2.4, 3.6 | 승인 시점과 실행 시점이 떨어져 변경 허용 시간대를 벗어날 수 있음 |
   | 6 | 변경 티켓(ServiceNow CHG)·PR 참조 없음 | 2.1, 2.3 | 승인한 변경과 변경 관리 기록을 연결할 수 없음 |
   | 7 | 실행기의 GitHub 접근 방식 미정의 | 2.2 `repository` | 당사는 GitHub Enterprise Cloud 사용. 보호 브랜치와 필수 리뷰를 우회하는지 알 수 없음 |
   | 8 | 오류 메시지·화면이 한국어 | 1.2 | 한국 외 법인 직원이 사용할 수 없음 |
   | 9 | 계정 생성·비활성화가 수동 | 3.2 `POST /admin/users`, `PATCH /admin/users/{userId}` | 퇴사자 계정과 서명 키(`DELETE /admin/signing-keys/{keyId}`)가 남을 위험 |
   | 10 | Plan 수정 시 기존 서명 전부 무효 | 4.2 | 보안상 타당하나, 시차가 있는 조직은 재승인 한 바퀴가 하루 이상 걸림 |
   | 11 | 실행기 단일 구성 | 5장, 4.3 | 실행기 장애 시 승인된 작업도 실행 불가 |
   | 12 | 킬 스위치는 실행 중단만 수행 | 4.6 | 이미 반영된 배포의 복구 범위 확인 필요 |

7. 요청 기능

   **가. 한국 법인 확대 필수 (정식 계약 전 납품 일정 서면 확약, 당사 acceptance test 통과 필요)**

   | 번호 | 요청 기능 | 구체적 요청 내용 |
   | --- | --- | --- |
   | 1 | 기업 SSO | SAML 2.0 또는 OIDC로 Okta 로그인. 예: `GET /auth/sso/{connectionId}/start`, `POST /auth/sso/saml/acs` 또는 `GET /auth/sso/oidc/callback`. SSO 사용 시 비밀번호 로그인 비활성화 설정 |
   | 2 | 감사 로그 내보내기·SIEM 전송 | `GET /audit-logs`와 같은 검색 조건으로 CSV·JSON 파일 내보내기(예: `POST /admin/audit-logs/exports`, `GET /admin/audit-logs/exports/{exportId}`). Splunk HTTP Event Collector 또는 syslog 실시간 전송(예: `PUT /admin/integrations/siem`). 전송 지연 측정과 누락 시 재전송(순번 기반) 포함 |
   | 3 | 변경 티켓·실행 시간 창 | Request에 외부 참조 필드(예: `changeTicket: { "system": "SERVICENOW", "number": "CHG..." }`)와 실행 가능 시간 창(`executionWindow: { "notBefore", "notAfter" }`)을 두고, 2.3 해시 대상과 2.4 서명 payload에 포함. **실행기가 실행 직전에 CHG 승인 유효성과 실행 창을 검사해 벗어나면 거부하고 5.1 `failedChecks`에 사유(예: `CHANGE_NOT_APPROVED`, `OUTSIDE_EXECUTION_WINDOW`)를 남길 것** |
   | 4 | GitHub 접근 방식 공개 | 실행기가 GitHub Enterprise Cloud에 접근하는 자격(GitHub App, deploy key 등), 쓰는 브랜치, PR 생성 여부를 문서로 제출. 보호 브랜치·필수 리뷰를 우회하지 않음을 당사 시험으로 확인 |

   **나. 한국 법인 확대 후 90일 이내**

   | 번호 | 요청 기능 | 구체적 요청 내용 |
   | --- | --- | --- |
   | 1 | SCIM 2.0 프로비저닝 | `/scim/v2/Users`, `/scim/v2/Groups` (생성·수정·비활성화). 사용자 비활성화 시 해당 사용자의 서명 키를 자동 폐기하고 감사 로그(`KEY_*`)에 기록 |

   - 확대 후 90일 안에 납품되지 않으면 당사는 추가 사용자 확대를 멈추고 계속 사용 여부를 다시 심사합니다.

   **다. 글로벌 확대 조건 (로드맵과 분기 단위 일정 회신)**

   | 번호 | 요청 기능 | 구체적 요청 내용 |
   | --- | --- | --- |
   | 1 | 영어 UI·오류 메시지 | `Accept-Language`에 따라 1.2 `message`와 화면을 영어로 제공. `code`는 지금처럼 고정 |
   | 2 | 지역 사무소별 네트워크 대역 | 회사 대역을 사무소 단위로 등록하고 감사 로그에 사무소 표시. ZTNA 환경 설정 가이드 |
   | 3 | 실행기 이중화 | 실행기 2대 이상 구성과 nonce 소진 처리의 일관성 보장 방안 |
   | 4 | 시차 승인 (follow-the-sun) | 부서가 다른 지역 담당자의 `PROJECT_OWNER` 승인 시험 방안 |
   | 5 | SOC 2 Type II | 감사 기관과 관찰 기간 일정 |

   **라. 파일럿 기간 시험 협조**

   당사는 파일럿 기간에 붙임 2의 시험을 진행합니다. 귀사 기술 담당자는 동탄 격리 랩 현장에서 당사 담당자 입회하에 참여해 주시기 바랍니다. 원격 접속 지원은 받지 않습니다.

8. 제출 요청 자료

   | 번호 | 자료 | 기한 |
   | --- | --- | --- |
   | 1 | 데이터 흐름 문서: 웹 서비스·DB·감사 로그·백업 위치(클라우드 사업자, 리전), AI 분석 호출 경로와 제3자 AI 제공사, 보관 기간, 학습 사용 여부 | 2026. 11. 10.(화) 18:00 KST |
   | 2 | 설치형 배포 가능 여부(웹 서비스 포함). 불가 시 국내 리전 전용 테넌트 구성과 귀사 운영자 접근 권한 범위 | 2026. 11. 10.(화) 18:00 KST |
   | 3 | 내부망 로그인 OTP 강제 가능 여부와 적용 증빙 | 2026. 11. 10.(화) 18:00 KST |
   | 4 | 당사 Limited Pilot 보안 질문지 (영문, 별도 송부) 회신 | 2026. 11. 10.(화) 18:00 KST |
   | 5 | 아키텍처 문서, 실행기·웹 서비스 권장 사양, 설치 절차서, 예상 설치 소요 시간, 업데이트·장애 지원 방식 | 2026. 11. 10.(화) 18:00 KST |
   | 6 | Tailscale 없이 실행기를 연결하는 대체 구성 가능 여부 | 2026. 11. 10.(화) 18:00 KST |
   | 7 | 당사 Mutual NDA·Pilot Agreement(영문 양식) 수정 요청 여부. 영문이 정본이며 한국어 번역본은 참고용 | 2026. 11. 10.(화) 18:00 KST |
   | 8 | 최근 3개년 재무제표 | 2026. 11. 10.(화) 18:00 KST |
   | 9 | 7항 가·나의 납품 일정, acceptance test 기준, 라이선스 포함 여부 | 2026. 12. 11.(금) |
   | 10 | 3년 견적: 라이선스, 별도 개발비, 실행기 비용을 나누어 원화·USD 병기. 부가세 별도 여부와 유효 기간 표기. USD 송장 발행 가능 여부 | 2026. 12. 11.(금) |
   | 11 | 보안 인증 보유 현황(SOC 2, ISO 27001, ISMS)과 미보유 시 취득 계획, 최근 외부 모의해킹 보고서 | 2026. 12. 11.(금) |
   | 12 | 사이버 보험 가입 여부와 보상 한도, 당사 MSA·DPA 양식 검토 의견 | 2026. 12. 11.(금) |

   - 1~8번이 기한까지 오지 않으면 당사 본사 VRM 접수(목표 11. 11.)를 할 수 없어 붙임 1의 목표 일정이 성립하지 않습니다.
   - 9~12번은 당사 파일럿 결과 보고서(2027. 1. 8. 제출 예정)에 반영합니다.

9. 회신 방법
   - 모든 회신은 메일 또는 공문으로 해 주시기 바랍니다. 구두·메신저 답변과 "다음 버전 제공 예정"처럼 일정이 확정되지 않은 답변은 검토에 반영하지 않습니다.
   - **계약 체결 전까지 일정·비용·계약 조건은 당사 Procurement(차유나 매니저) 창구로만 협의합니다.** 당사 엔지니어링 담당자와 합의한 일정이나 조건이 있더라도 이 창구를 통해 서면으로 확인되지 않은 것은 당사 약속이 아닙니다.
   - 기술 문의는 당사 APAC Engineering(권대현 Director) 팀과 메일로 하시고, Procurement를 참조에 넣어 주시기 바랍니다.
   - 계약 체결 전까지 당사 고객사 이름과 당사 내부 사고 내용은 외부에 언급하지 말아 주시기 바랍니다.
   - 기한은 한국 시간(KST) 기준입니다.

붙임
1. Limited Pilot 범위 및 목표 일정 1부.
2. 필수 시험 항목표 1부.
3. English Summary 1부.  끝.

---

## 노스브리지시스템즈코리아 유한회사 대표이사 (직인 생략)

| 기안 | 검토 | 협조 | 협조 | 승인 |
| --- | --- | --- | --- | --- |
| Procurement Manager 차유나 | Finance & Admin Director 류지혜 | APAC Engineering Director 권대현 | IT Manager 남기훈 | 법인장(Country Manager) 함석진 |

- 본사 사전 협의: APAC Procurement Lead Priya Raman, Global VRM Program Manager Rachel Stein (Limited Pilot 사전 상담 2026. 11. 5.)

---

## 붙임 1. Limited Pilot 범위 및 목표 일정

| 항목 | 내용 |
| --- | --- |
| 계약 당사자 | 노스브리지시스템즈코리아 유한회사 단독 |
| 참여자 | 당사 한국 법인 직원 15명 (타 법인 직원 접속 없음) |
| 저장소 | 랩 전용 합성 저장소 3개 (당사 제품 코드 미포함, 당사 수출통제 검토 완료분) |
| 데이터 | 합성 데이터만. 당사 기밀·고객사 데이터 없음 |
| 대상 환경 | 당사 동탄 격리 랩의 장비 시뮬레이터 스테이징. 고객사 환경 제외 |
| 설치 위치 | 1안: 실행기와 웹 서비스 모두 당사 격리 랩 / 2안: 국내 리전 전용 테넌트 (당사 VRM 별도 확인, 일정 별도) |
| 귀사 지원 | 현장 방문, 당사 담당자 입회. 원격 접근 없음 |
| 계정 | 로컬 계정 15개 (파일럿 한정 예외). 이탈 당일 비활성화와 서명 키 폐기, 종료일 전원 정리 |
| 규모 프리셋 | `MEDIUM` |

| 일자 | 내용 |
| --- | --- |
| 2026. 11. 10.(화) | 귀사 1차 자료 회신 기한 (8항 1~8번) |
| 2026. 11. 11.(수) | 당사 본사 VRM Limited Pilot 접수 |
| 2026. 11. 13.(금) | 당사 네트워크·보안 예외 판단 |
| 2026. 11. 18.(수) | 당사 VRM 판정 목표 |
| 2026. 11. 19.(목) ~ 11. 20.(금) | 설치 (당사 DevOps, 귀사 현장 지원) |
| 2026. 11. 23.(월) ~ 12. 18.(금) | 파일럿 4주 (1주차 안정화, 2주차 이후 공격 시험) |
| 2026. 12. 11.(금) | 귀사 2차 자료 회신 기한 (8항 9~12번) |
| 2027. 1. 8.(금) | 당사 내부 결과 보고 |

- 위 일정은 모두 목표일입니다. 11. 13.까지 당사 네트워크·보안 예외 판단이 나오지 않으면 11. 23. 시작 목표는 철회하고, 승인 완료 후 다시 정해 통보합니다. 시작이 늦어져도 시험 기간을 줄이지 않습니다.
- 2026. 12. 24.~2027. 1. 1.은 당사 변경 동결 기간입니다.

## 붙임 2. 필수 시험 항목표

| 번호 | 시험 | 기대 결과 | 관련 명세 | 판정 |
| --- | --- | --- | --- | --- |
| 1 | 승인 없이 실행 시도 | 실행되지 않음 | 3.6, 5.1 `MISSING_REQUIRED_APPROVER` | 1건이라도 실행되면 파일럿 즉시 중단 |
| 2 | 웹 서비스 측 Plan 변조 후 실행 요청 | `403 VERIFICATION_FAILED`, `PLAN_HASH_MISMATCH`, 경보 발송 | 5.1 | 통과되면 즉시 중단 |
| 3 | 소진된 승인 envelope 재전송 | `NONCE_ALREADY_USED` | 2.4, 5.1 | 통과되면 즉시 중단 |
| 4 | 참여자 노트북 스테이징 키 점검 | 유효한 키 0개, 노트북 직접 실행 경로 차단 증빙 | - | 키 발견 시 즉시 중단 |
| 5 | 실행 중 킬 스위치 (외부망 포함) | 서명 없이 `KILLED`, 10초 이내, 실제 작업 정지 확인 | 4.6 | 10초 초과 시 해당 시험 중단, 확대 불가 |
| 6 | 외부망에서 DEPLOY 승인 | `403 INTERNAL_NETWORK_ONLY`, `blockedTaskIds` 표시 | 3.6, 4.4, 4.5 | - |
| 7 | 접속 환경 판별 | 승인된 랩 경로는 `X-Network: INTERNAL`, ZTNA 원격 접속은 `EXTERNAL` | 1.1 | - |
| 8 | 실행기 연결 차단 후 제출 | `502 EXECUTOR_UNAVAILABLE`, 요청 상태 유지, 복구 시간 기록 | 4.3 | - |
| 9 | LOW 작업 처리 시간 | 요청~실행 중앙값 5분 이내 (근무 시간) | - | 미달 시 개선 요청 |
| 10 | DEPLOY 승인 대기 | 중앙값 30분 이내 | - | 1시간 초과 시 한국 확대 보류 |
| 11 | 이탈자 처리 | 당일 `PATCH /admin/users/{userId}` 비활성화, `DELETE /admin/signing-keys/{keyId}` 폐기 | 3.2 | - |

## 붙임 3. English Summary

- **Decision**: Conditional adoption, limited to a Korea-entity Limited Pilot. This is not a vendor selection or a purchase commitment. Production contract and any global rollout will be decided separately.
- **Start conditions**: Global VRM approval for the pilot scope, signed Pilot Agreement, IT/security exceptions (local accounts, Tailscale), and ARB exception if required.
- **Scope**: 15 Korea-entity employees, 3 synthetic lab repositories, synthetic data only, isolated Dongtan lab, no customer environment, no remote vendor access. Follow-the-sun approval is out of scope and will be reported as not validated.
- **Target dates (KST)**: Vendor documents Nov 10 (Tue), VRM intake Nov 11 (Wed), VRM decision target Nov 18 (Wed), pilot Nov 23 (Mon) to Dec 18 (Fri), internal report Jan 8, 2027 (Fri). The Nov 16 date previously discussed with the vendor is not a company commitment.
- **Must-haves before Korea expansion**: Okta SSO (SAML/OIDC); audit log export and Splunk/syslog streaming; ServiceNow change number and execution window bound into the plan hash and checked by the executor right before execution; documented GitHub access model with protected-branch test. SCIM within 90 days after expansion.
- **Global conditions**: SOC 2 Type II, English UI and error messages, executor high availability, regional office network ranges, follow-the-sun approval validation.
