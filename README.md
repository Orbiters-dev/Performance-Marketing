# Performance Marketing — ORBI

Amazon PPC 자동화 도구 모음. DataKeeper 기반 데이터 수집부터 대시보드, 입찰 최적화, 시뮬레이터까지 포함.

## 구조

```
tools/                    Python 실행 스크립트
  amazon_ppc_executor.py  입찰/예산/키워드 제안 + 실행 (3개 브랜드)
  amazon_ppc_simulator.py 낭비절감 백테스트 시뮬레이터
  run_amazon_ppc_daily.py 일일 PPC 분석 리포트
  generate_dashboard_data.py 대시보드 data.js 생성
  data_keeper.py          DataKeeper 수집기
  data_keeper_client.py   DataKeeper 조회 클라이언트

.github/workflows/        GitHub Actions 자동화
  amazon_ppc_daily.yml    매일 KST 08:00 분석 실행
  ppc_dashboard_action.yml 대시보드 Propose / Execute
  data_keeper.yml         DataKeeper 2x daily 수집

docs/ppc-dashboard/       GitHub Pages 대시보드 (정적 HTML)

workflows/                에이전트 SOP (마크다운)

.claude/skills/amazon-ppc-agent/  Claude 스킬 정의 + 참고 문서
```

## 브랜드

| 브랜드 | Seller | 일 예산 | ACOS 목표 |
|--------|--------|---------|-----------|
| Grosmimi | GROSMIMI USA | $3,000 | 20% |
| Naeiae | Fleeters Inc | $120 | 25% |
| CHA&MOM | Orbitool | $150 | 30% |

## 대시보드

GitHub Pages: `https://orbiters-dev.github.io/Performance-Marketing/ppc-dashboard/`

## 시작하기

```bash
# 의존성 설치
pip install requests google-auth google-auth-oauthlib google-api-python-client anthropic

# .env 설정 (AMZ_ADS_CLIENT_ID, AMZ_ADS_REFRESH_TOKEN, ANTHROPIC_API_KEY 등)
cp .env.example .env

# 일일 분석 실행
python tools/run_amazon_ppc_daily.py

# 제안 생성 (전체 브랜드)
python tools/amazon_ppc_executor.py --propose

# 백테스트 시뮬레이터
python tools/amazon_ppc_simulator.py --brand grosmimi --days 90
```

## 필요 Secrets (GitHub Actions)

`AMZ_ADS_CLIENT_ID`, `AMZ_ADS_CLIENT_SECRET`, `AMZ_ADS_REFRESH_TOKEN`,
`AMZ_SP_CLIENT_ID`, `AMZ_SP_CLIENT_SECRET`, `AMZ_SP_REFRESH_TOKEN_FLEETERS`,
`AMZ_SP_REFRESH_TOKEN_GROSMIMI`, `AMZ_SP_REFRESH_TOKEN_ORBITOOL`,
`ANTHROPIC_API_KEY`, `PPC_REPORT_RECIPIENT`,
`GMAIL_OAUTH_CREDENTIALS_JSON`, `GMAIL_TOKEN_JSON`,
`ORBITOOLS_USER`, `ORBITOOLS_PASS`
