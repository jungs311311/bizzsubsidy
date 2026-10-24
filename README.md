# bizzsubsidy · 내 사업장 지원 찾기

업종·매출·직원 수를 넣으면 소상공인·소기업·중기업을 판정하고, 받을 수 있는 정부 지원과 지원 제외 업종을 보여주는 사이트입니다.
기업마당 API로 소상공인·개인사업자용 새 공고를 매일 아침 자동으로 가져옵니다.

- 사이트 주소: https://jungs311311.github.io/bizzsubsidy

## 파일 구성

| 파일 | 하는 일 |
|---|---|
| `index.html` | 사이트 화면 (규모 판정, 지원 목록, 제외 업종, 새 공고) |
| `data/notices.json` | 기업마당에서 받아 온 공고. 매일 자동으로 바뀜 |
| `scripts/fetch_bizinfo.py` | 기업마당 API를 불러 소상공인·개인사업자용 공고만 걸러 저장 |
| `.github/workflows/update.yml` | 매일 오전 5시 52분(한국시간)에 위 스크립트를 실행 |

## 처음 한 번만 할 일

1. **인증키 등록**: 저장소 `Settings` → `Secrets and variables` → `Actions` → `New repository secret`
   - Name: `BIZINFO_KEY`
   - Secret: 기업마당에서 받은 인증키
2. **사이트 켜기**: `Settings` → `Pages` → Source를 `Deploy from a branch`, Branch를 `main` / `(root)`로 두고 `Save`
3. **첫 실행**: `Actions` 탭 → `기업마당 공고 매일 갱신` → `Run workflow`

이후에는 매일 자동으로 갱신됩니다.

## 판정 기준

- 규모: 중소기업기본법 시행령 업종별 매출 기준, 소상공인기본법 상시근로자 기준
- 지원 제외 업종: 소상공인시장진흥공단 정책자금 지원 제외 업종 목록
- 금액·조건: 2026년 공개 공고 기준. 공고가 바뀌면 `index.html`의 지원 목록을 고칩니다.
