
# 노스브리지시스템즈코리아 유한회사 (Northbridge Systems Korea Ltd.)

경기도 화성시 동탄 (가상 주소) / 대표전화 031-000-0000 / Procurement procurement.kr@northbridge.example
미국 Northbridge Systems, Inc.의 한국 법인입니다. 본 공문은 한국어 본문을 정본으로 하며, 당사 본사 공유용 영문 요약(English Summary)을 붙임 2로 함께 보냅니다.

---

| 항목 | 내용 |
| --- | --- |
| 문서번호 | NBK-PROC-2026-1112-02 |
| 시행일자 | 2026. 11. 12. (목) |
| 수신 | BeforeAI 서비스 개발 담당 |
| 참조 | BeforeAI 영업 담당, 기술 지원 담당 |
| 발신 | 노스브리지시스템즈코리아 유한회사 Finance & Admin 본부 Procurement |
| 당사 내부 참조 | APAC Procurement Lead, Global Vendor Risk Management(VRM), APAC Engineering Director, IT Manager |
| 선행 공문 | NBK-PROC-2026-1106-01 (2026. 11. 6.) |
| 제목 | 귀사 보완 설명(실행기 성격·Tailscale) 검토 결과 통보 및 완화·유지 항목 구분 |

---

1. 귀사의 무궁한 발전을 기원합니다.

2. 관련
   - 가. 당사 선행 공문 「AI 작업 통제 서비스(BeforeAI) 도입 검토 결과 통보 및 Limited Pilot 착수 자료·기능 요청」 (NBK-PROC-2026-1106-01, 2026. 11. 6.)
   - 나. 귀사 1차 자료 회신 및 보완 설명 2건 (메일 본문 및 「아키텍처 문서 rev B」, 2026. 11. 10.(화))
   - 다. 당사 내부 보완 설명 검토 회의 (2026. 11. 11.(수))

3. 총괄
   - 본 공문은 귀사가 1차 자료와 함께 보내 주신 **두 가지 보완 설명**을 당사가 검토한 결과, **완화되는 항목**과 **그대로 유지되는 필수·본사 요구**를 구분해 통보하기 위한 것입니다.
   - **결론 틀은 선행 공문과 동일합니다. 즉 「조건부 도입 — 한국 법인 한정 Limited Pilot, 당사 본사 VRM 승인 후 착수」이며, 정식 채택·구매 약정·글로벌 확대 약속이 아닙니다.** 보완 설명으로 이 틀은 바뀌지 않습니다.
   - 보완 설명은 당사 **명세(API 명세서)를 대체하지 않습니다.** 명세 본문과 보완 설명이 다른 부분은 9항과 같이 계약 기준 문서를 서면으로 확정해 주시기 바랍니다.

4. 귀사 보완 설명의 요지 (당사가 이해한 내용)

   | 번호 | 보완 설명 | 당사가 이해한 요지 |
   | --- | --- | --- |
   | 1 | 실행기의 성격 | 실행기는 무거운 별도 인프라 러너가 아니라 **경량 컴포넌트**이다. ① Plan 해시를 실행기가 자체 생성하고 Ed25519 서명·nonce를 검증하는 "서명 검증기", ② 승인 envelope을 비대칭키 종단간 암호화(E2EE)로 받아 **실행기 공개키로만 복호화**(웹 서비스는 열지 못함), ③ 검증 6단계 통과 시 웹쉘 세션으로 로컬 작업을 수행 |
   | 2 | Tailscale | 명세 1.1·5장의 **Tailscale은 개발·테스트 단계의 임시 구성**이며, 운영 배포는 고객사 내부망 연결이다. 웹 서비스↔실행기 구간은 **mTLS**, 내부망 대역은 고객사(당사) 관리자가 설정하며, 사무소별 대역 등록이 가능 |

5. 보완 설명으로 **완화·해소**되는 항목

   당사는 아래 항목을 선행 공문 대비 완화 또는 해소된 것으로 조정합니다. 단, 완화는 **당사 파일럿 시험으로 실증함을 전제**로 하며, 서면 설명만으로 통과 처리하지 않습니다.

   | 선행 공문 위치 | 조정 내용 | 근거 |
   | --- | --- | --- |
   | 3항 착수 조건 ③ "(로컬 계정, **Tailscale**)" | **"(로컬 계정)"으로 축소.** Tailscale 상시 예외 승인을 착수 조건에서 제외 | 운영 배포가 내부망 mTLS이면 당사 표준 외 네트워크 도구(Tailscale)의 **상시 사용**이 아니므로, 당사 Zscaler/ZTNA 표준에 대한 예외 승인 대상이 아님 |
   | 6항 3번 "실행기 연결에 Tailscale 사용 → 예외 승인 필요" | **우려 완화.** 개발·테스트 한정 구성으로 보고, 배포는 내부망 mTLS·사무소별 대역 등록으로 재서술 | 보완 설명 2 |
   | 6항 11번 "실행기 단일 구성" | **"서버 대수"에서 "컴포넌트 다중화·페일오버"로 재서술**하고 한국 확대 가치평가 우선순위 하향 | 실행기가 무거운 러너가 아니라 경량 검증·E2EE 복호화·웹쉘 실행 컴포넌트라면, 가용성은 물리 서버 대수가 아니라 컴포넌트 다중화·페일오버로 다룰 수 있음 |
   | 8항 6번 "Tailscale 없이 연결하는 대체 구성 질의" | **해소.** 배포 기준이 mTLS임이 확인되어 별도 대체 구성 질의 불요 | 보완 설명 2 |

   - **당사 핵심 요구와의 정합**: 보완 설명 1(실행기가 Plan 해시를 자체 생성하고, envelope을 실행기 공개키로만 복호화하는 경량 컴포넌트)은 당사 핵심 요구인 **"엔지니어 노트북에 스테이징 접속 키가 없고 키는 실행기만 보유"**와 잘 맞으며, 선행 공문 4항 1·2번을 강화합니다. 당사가 막으려는 사고 유형(엔지니어 자격 증명으로 AI 에이전트가 직접 실행)에 더 정확히 부합합니다.
   - **실증 전제**: 위 정합은 붙임 1의 시험 2(Plan 변조 거부 `PLAN_HASH_MISMATCH`), 3(소진된 envelope 재전송 거부 `NONCE_ALREADY_USED`), 4(노트북 스테이징 키 0개)로 당사 파일럿에서 확인합니다.
   - **가용성 검증 유지**: 재서술에도 불구하고 명세 4.3 `502 EXECUTOR_UNAVAILABLE` 시 요청 상태 유지와 복구 시간은 파일럿에서 검증합니다.

6. 보완 설명으로 **바뀌지 않고 그대로 남는** 필수·본사 요구

   보완 설명 2건은 **네트워크 구성과 실행기 구조**에 관한 것으로, 아래 항목은 조정하지 않습니다. 특히 보완 설명 1의 E2EE·실행기 공개키 복호화는 **승인 envelope의 전달 경로 보안**을 뜻하며, **AI 분석 시 소스코드·프롬프트가 외부로 전송되는지**의 문제를 대체하지 않습니다. ("암호화하여 전달한다"와 "코드가 외부 AI로 나가지 않는다"는 별개의 사실입니다.)

   | 번호 | 유지 항목 | 선행 공문 위치 | 유지 사유 |
   | --- | --- | --- | --- |
   | 1 | **당사 본사 VRM Tier 1 승인** (파일럿 범위 VRM 승인) | 3항 착수 조건 ①, 5항 | 소스코드 저장소·스테이징 접근 업체는 금액과 무관하게 Tier 1. 네트워크 구조 변경과 무관 |
   | 2 | SOC 2 Type II 또는 ISO 27001 (미보유 시 보완 패키지는 Global VRM 서면 예외 승인 대상) | 5항 1번 | 보완 설명과 무관 |
   | 3 | DPA와 데이터 저장 위치(웹 서비스·DB·감사 로그·백업 리전), **AI 분석 시 소스코드·프롬프트 전송 경로·제3자 AI 제공사·보관/학습 정책** | 5항 2번, 8항 1번 | E2EE는 envelope 전달 경로 보안일 뿐, AI 분석 입력의 외부 전송 여부를 보장하지 않음. 감사 로그에 당사 직원 이름·사번·IP가 남는 점도 그대로 |
   | 4 | 기업 SSO (Okta, SAML 2.0 또는 OIDC)와 SCIM 2.0 | 5항 3번, 7항 | 명세 3.1은 여전히 사번·비밀번호 로그인. 인증 구조는 네트워크 보완 설명과 무관 |
   | 5 | 감사 로그의 회사 보관 (파일 내보내기·SIEM 전송) | 5항 4번, 7항 가 2번 | 명세 3.9는 검색만 제공 |
   | 6 | ServiceNow 변경 티켓(CHG)·실행 가능 시간 창을 Plan 해시 대상에 포함하고, **실행기가 실행 직전에 CHG 승인 유효성과 실행 창을 검사**해 벗어나면 거부·`failedChecks` 기록 | 7항 가 3번 | 한국 확대 필수. 실행기가 경량이라도 실행 직전 검사 항목은 그대로 요구 |
   | 7 | 실행기의 GitHub Enterprise Cloud 접근 방식 공개와 보호 브랜치·필수 리뷰 우회 금지 시험 | 7항 가 4번 | 보완 설명과 무관 |
   | 8 | 영어 UI·영어 오류 메시지 (글로벌 확대 조건) | 7항 다 1번 | 명세 1.2 `message`가 한국어. 보완 설명과 무관 |
   | 9 | **EAR 수출통제 기술 데이터의 외부(AI 분석) 전송 금지** | 5항 2번, 선행 공문 9항 | 보완 설명과 무관. E2EE로 전달되는 것은 승인 envelope이지 AI 분석 입력이 아님. 파일럿은 EAR99 합성 저장소만 사용 |
   | 10 | 본사 계약 양식(MSA)·DPA 수용, USD 송장, 사이버 보험 USD 5M, 재무 안정성 | 5항 5번 | 보완 설명과 무관 |
   | 11 | 내부망 로그인 OTP 강제 가능 여부 (로컬 계정에도 적용) | 6항 1번, 8항 3번 | 로컬 계정 예외는 착수 조건에 그대로 남으며, 그에 대한 OTP 요구도 유지 |

7. 착수 조건 (갱신)

   선행 공문 3항의 착수 조건을 아래와 같이 갱신합니다. **네 가지가 모두 끝나기 전에는 설치·연결을 시작하지 않는다는 원칙은 동일**하며, ③에서 Tailscale만 제외됩니다.

   | 번호 | 착수 조건 | 선행 공문 대비 |
   | --- | --- | --- |
   | ① | 파일럿 범위에 대한 당사 본사 VRM 승인 | 유지 |
   | ② | 당사 Pilot Agreement 체결 | 유지 |
   | ③ | 당사 IT·보안 예외 승인 **(로컬 계정)** | **Tailscale 제외** (5항 참조) |
   | ④ | 필요 시 당사 Architecture Review Board(ARB) 예외 승인 | 유지 |

   - 로컬 계정 예외(명세 3.1 사번·비밀번호 로그인에 따른 Okta 미적용분)는 네트워크 보완 설명과 **별개로 그대로 남습니다.** Tailscale은 네트워크 구조 변경으로 빠지는 것이고, 로컬 계정은 인증 구조가 바뀌지 않아 유지됩니다.
   - 당사 2026. 11. 13.(금) 보안·네트워크 판단 항목은 **"Tailscale 예외 심사"에서 "웹 서비스↔실행기 mTLS 구성과 격리 랩 VLAN 분리 검토"로 교체**됩니다.

8. 추가 확인 요청 (2026. 11. 14.(금) 18:00 KST 회신)

   | 번호 | 요청 | 사유 |
   | --- | --- | --- |
   | 1 | 운영 배포 시 웹 서비스↔실행기 **mTLS 인증서 발급·갱신 주체**(귀사 또는 당사)와 절차 | 당사 격리 랩 운영 책임 구분 |
   | 2 | 당사 격리 랩 설치 시 **개발·테스트용 Tailscale을 사용하지 않고 처음부터 mTLS로 설치** 가능 여부. 불가 시 Tailscale 트래픽이 격리 랩 VLAN을 벗어나지 않음을 보장하는 방법 | 선행 공문 6항 2번 ZTNA egress 우려와 분리하여 확인 |
   | 3 | **실행기 "컴포넌트 다중화·페일오버" 구성**이 라이선스 기본 포함인지 추가 비용인지. 선행 공문 붙임의 "실행기 2대" 전제로 산출한 견적을 **컴포넌트 라이선스·HA 구성 기준으로 재산출** | 선행 공문 6항 11번 재서술에 따른 견적 정정 |
   | 4 | 사무소별 내부망 대역 등록 방식과, 당사 파일럿에서 **동탄 격리 랩 대역만 등록**하는 구성 지원 여부 | 사무소별 대역은 글로벌 확대(follow-the-sun) 조건으로 분리 |

9. 계약 기준 문서 확정 요청

   - 명세 1.1은 Tailscale 대역(100.64.0.0/10)을 내부망으로, 5장은 Tailscale 기반 연결을 기술하고 있어 **보완 설명 2(배포는 mTLS)와 어긋납니다.**
   - 귀사가 **계약 기준으로 삼을 문서(명세 개정판 rev 번호, 또는 아키텍처 문서)를 명시**하고, 명세 1.1·5장의 Tailscale 기술을 **운영 배포 기준(mTLS·내부망 대역·사무소별 등록)으로 갱신한 판**을 서면으로 제출해 주시기 바랍니다.
   - 서면으로 계약 기준 문서가 확정되지 않은 상태에서는, 명세 본문과 보완 설명이 다른 부분을 당사가 계약 근거로 인정하지 않습니다.

10. 변동 없는 사항 (선행 공문 유효)

   - 선행 공문 7항 요청 기능(한국 확대 필수 4개, 확대 후 90일 내 SCIM, 글로벌 확대 조건), 8항 제출 자료(특히 9~12번, 2026. 12. 11.(금) 기한), 붙임 1 Limited Pilot 범위·목표 일정은 **그대로 유효**합니다. 본 공문으로 변경되는 것은 5·7항의 Tailscale·실행기 가용성 관련 부분뿐입니다.
   - 당사 목표 일정(VRM 접수 11. 11., 판정 목표 11. 18., 파일럿 11. 23.~12. 18., 결과 보고 2027. 1. 8.)은 유지되며, 보완 설명으로 **시작일을 앞당기지 않습니다.** 모두 착수 조건 충족을 전제로 한 목표일입니다.

11. 회신 방법
   - 모든 회신은 메일 또는 공문으로 해 주시기 바랍니다. 구두·메신저 답변과 일정이 확정되지 않은 답변은 검토에 반영하지 않습니다.
   - **계약 체결 전까지 일정·비용·계약 조건은 당사 Procurement(차유나 매니저) 창구로만 협의합니다.** 기술 문의는 당사 APAC Engineering(권대현 Director) 팀과 메일로 하시고 Procurement를 참조에 넣어 주시기 바랍니다.
   - 계약 체결 전까지 당사 고객사 이름과 당사 내부 사고 내용은 외부에 언급하지 말아 주시기 바랍니다.
   - 기한은 한국 시간(KST) 기준입니다.

붙임
1. 완화·유지 항목 대비표 1부.
2. English Summary 1부.  끝.

---

## 노스브리지시스템즈코리아 유한회사 대표이사 (직인 생략)

| 기안 | 검토 | 협조 | 협조 | 승인 |
| --- | --- | --- | --- | --- |
| Procurement Manager 차유나 | Finance & Admin Director 류지혜 | APAC Engineering Director 권대현 | IT Manager 남기훈 | 법인장(Country Manager) 함석진 |

- 본사 사전 협의: Global VRM Program Manager Rachel Stein (VRM 접수 2026. 11. 11.), APAC Security Architect Wei Ling Tan (mTLS·격리 VLAN 검토 2026. 11. 13. 예정)

---

## 붙임 1. 완화·유지 항목 대비표

| 구분 | 항목 | 선행 공문 상태 | 본 공문 상태 |
| --- | --- | --- | --- |
| 완화 | 착수 조건 ③ Tailscale 예외 | 필요 | **제외** (배포 mTLS) |
| 완화 | 실행기 연결 Tailscale 우려 (6항 3번) | 예외 승인 필요 | **완화** (개발 test 한정) |
| 완화 | 실행기 단일 구성 (6항 11번) | 서버 대수 우려 | **컴포넌트 다중화·페일오버로 재서술, 우선순위 하향** |
| 해소 | Tailscale 없는 대체 구성 질의 (8항 6번) | 요청 | **해소** |
| 강화 | Plan 해시 자체 생성·E2EE (4항 1·2번) | 긍정 평가 | **핵심 요구 정합 확인, 파일럿 실증 전제** |
| 유지 | 본사 VRM Tier 1 승인 | 필수 | **유지** |
| 유지 | SOC 2 Type II / ISO 27001 | 필수 | **유지** |
| 유지 | DPA·데이터 리전·AI 분석 전송 경로 | 필수 | **유지** (E2EE로 대체 안 됨) |
| 유지 | Okta SSO·SCIM | 필수 | **유지** |
| 유지 | 영어 UI·오류 메시지 | 글로벌 조건 | **유지** |
| 유지 | ServiceNow CHG·실행 창 실행기 검사 | 한국 확대 필수 | **유지** |
| 유지 | GitHub 접근 방식·보호 브랜치 시험 | 한국 확대 필수 | **유지** |
| 유지 | EAR 외부(AI 분석) 전송 금지 | 필수 | **유지** |
| 유지 | 로컬 계정 예외·내부망 OTP | 착수 조건·우려 | **유지** (Tailscale과 별개) |

## 붙임 2. English Summary

- **Purpose**: Response to the vendor's two clarifications sent with the first document set (Nov 10). Separates what is **relaxed** from what **remains required**.
- **Decision framing unchanged**: Still "Conditional adoption — Korea-entity Limited Pilot, start only after Global VRM approval." Not a vendor selection, purchase commitment, or global rollout.
- **Relaxed by clarification 1 (executor nature)**: The executor is described as a **lightweight component** (self-generates the plan hash, verifies Ed25519 signature and nonce; decrypts the E2EE approval envelope with the executor's key only — the web service cannot open it; runs local work via web-shell after the 6-step check). The prior "single-executor / server count" concern is **re-framed as component redundancy / failover** and lowered in priority. This aligns with our core requirement — **no staging keys on engineer laptops; only the executor holds keys** — and reinforces letter-01 items 4.1/4.2. To be **proven in the pilot** (tests 2/3/4), not accepted on paper alone.
- **Relaxed by clarification 2 (Tailscale)**: Tailscale is a **dev/test-only** arrangement; production uses internal-network **mTLS** between web service and executor, with network ranges set by our admins and per-office range registration. Therefore **Tailscale standing exception is removed from the start conditions** (③ becomes "(local accounts)"), and letter-01 concern 6.3 and request 8.6 are relaxed/resolved. The Nov 13 security review item changes from "Tailscale exception" to "mTLS / isolated-lab VLAN review."
- **Still required (not changed by the clarifications)**: Global VRM Tier 1 approval; SOC 2 Type II or ISO 27001; DPA, data residency, and **the external transfer path of source code/prompts during AI analysis** (E2EE secures envelope delivery, **not** AI-analysis input); Okta SSO/SCIM; audit-log export/SIEM; ServiceNow CHG and execution window bound into the plan hash and checked by the executor just before execution; documented GitHub access model with protected-branch test; English UI/error messages; **EAR-controlled data must not be sent to external AI**; MSA/DPA, USD invoicing, USD 5M cyber insurance; local-account exception and internal-network OTP (separate from Tailscale).
- **Start conditions**: Four conditions unchanged except Tailscale removed from ③. Local-account exception stays. Target dates unchanged; the clarifications **do not advance** the start date.
- **Also requested (reply by Nov 14)**: mTLS certificate ownership; whether install can skip dev/test Tailscale and use mTLS from the start; whether component HA is licensed or extra, with executor quote recomputed off the HA basis; per-office range registration with Dongtan-lab-only registration for the pilot.
- **Contract baseline**: Spec 1.1/5 still describe Tailscale, conflicting with clarification 2. Vendor must state the controlling document (spec rev or architecture doc) and submit a version updating 1.1/5 to the mTLS production baseline.
