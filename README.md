# K-Run Ventures 예비심사보고서 자동 작성 스킬
**krun-prescreening-report**

K-Run Ventures 케이런7호 펀드용 예비심사보고서(Pre-screening Report)를  
IR자료(PDF/PPT/이미지)로부터 자동 생성하는 Claude 스킬입니다.

---

## 주요 기능

- IR자료 첨부 → 9개 섹션 예비심사보고서 자동 작성
- 시장 분석 섹션 한정 외부 자료 보완 (출처 필수 명기)
- 미확인 항목 자동 "확인 필요" 처리
- DD 체크리스트 자동 생성 (🔴 필수 / 🟡 중요 / 🟢 참고)
- HTML 파일 출력 → 브라우저 인쇄로 PDF 변환

---

## 파일 구조

```
krun-prescreening-report/
├── SKILL.md                        ← 핵심 지침 (트리거 조건 + 작성 규칙)
├── references/
│   └── html-style-guide.md         ← CSS/컬럼 너비 전체 기준
└── assets/
    └── sample_report.html          ← 모빌테크 보고서 (레이아웃 레퍼런스)
```

---

## 설치 방법

### PART 1 — GitHub에서 스킬 다운로드

#### ① 저장소 Fork

1. 아래 원본 저장소 주소로 접속합니다

   ```
   https://github.com/skkim4uni/krun-prescreening-report
   ```

2. 우측 상단 **Fork** 버튼 클릭 → **Create fork** 클릭
3. 내 계정 아래 복사본이 생성됩니다  
   예: `github.com/내아이디/krun-prescreening-report`

#### ② 내 컴퓨터에 다운로드

```bash
git clone https://github.com/내아이디/krun-prescreening-report.git
cd krun-prescreening-report
```

> ⚠️ Git이 없다면 [git-scm.com](https://git-scm.com)에서 먼저 설치하세요.

---

### PART 2 — Claude에 스킬 설치

#### ① .skill 파일 패키징

스킬 폴더 안에서 아래 명령어를 실행합니다.

```bash
# Python 스크립트로 패키징 (zip → .skill 확장자)
python3 -c "
import zipfile, os, pathlib

skill_dir = pathlib.Path('.')
output = pathlib.Path('krun-prescreening-report.skill')

with zipfile.ZipFile(output, 'w', zipfile.ZIP_DEFLATED) as zf:
    for f in skill_dir.rglob('*'):
        if f.is_file() and '.git' not in f.parts:
            zf.write(f, f.relative_to(skill_dir))

print(f'패키징 완료: {output} ({output.stat().st_size:,} bytes)')
"
```

생성된 `krun-prescreening-report.skill` 파일을 확인합니다.

#### ② Claude.ai에 스킬 설치

1. [claude.ai](https://claude.ai) 접속 후 로그인
2. 좌측 메뉴 → **Skills** (또는 설정) 탭 클릭
3. **Install Skill** 버튼 클릭
4. 생성된 `.skill` 파일 업로드
5. 설치 완료 확인

> 💡 Skills 메뉴가 보이지 않는 경우, Claude Pro 또는 Team 플랜이 필요할 수 있습니다.

---

## 사용 방법

### 기본 사용 — 보고서 신규 작성

IR자료(PDF 권장)를 첨부한 후 아래와 같이 입력합니다.

```
이 IR자료로 예비심사보고서 작성해줘
```

또는

```
[파일 첨부] 예비심사 보고서 만들어줘
```

**IR자료 형식별 지원 현황**

| 형식 | 지원 | 권장 방법 |
|---|---|---|
| PDF | ✅ 완벽 지원 | PPT → PDF 변환 후 업로드 권장 |
| PPT (.pptx) | ⚠️ 부분 지원 | 텍스트 인식 가능, 도표 누락 가능성 |
| 이미지 (PNG/JPG) | ✅ 지원 | 슬라이드 캡처 후 업로드 |

---

### 항목 수정

보고서 작성 후 특정 항목만 수정 요청합니다.

```
담당자를 홍길동으로 입력해줘
```

```
수주현황 3번 항목 계약 완료로 변경해줘
```

---

### PDF 저장

```
PDF로 저장해줘
```

또는

```
HTML로 변환해줘
```

HTML 파일이 제공되면:  
**Ctrl+P → 프린터 "PDF로 저장" → 여백 "없음" → 저장**

---

## 보고서 구성 (9개 섹션)

| # | 섹션 | 주요 내용 |
|---|---|---|
| 1 | 보고서 개요 | 작성일, 담당자(공란), 펀드명, 심사 단계, 검토 의견 |
| 2 | 기업 개요 | 기본 정보, 주주명부 |
| 3 | 핵심인력 | 주요 인물 프로필 |
| 4 | 사업 내용 | 주요 제품, 기술 구조도, 차별점 |
| 5 | 시장 분석 및 경쟁사 | 시장 규모, 경쟁사 비교, 경쟁 우위 |
| 6 | 영업 현황 | 주요 고객, 수주 현황 및 계획 |
| 7 | 재무 현황 및 전망 | 실적 3개년, 전망 3개년 |
| 8 | 투자 조건 및 밸류에이션 | 투자 조건, 밸류에이션 검토, 자금사용계획 |
| 9 | DD 체크리스트 | 미확인 항목, 중요도 분류 |
| 10 | 종합 의견 | 항목별 ⭐ 평점, 투자 검토 의견 |

---

## 데이터 출처 원칙

| 섹션 | 허용 소스 | 비고 |
|---|---|---|
| 시장 분석 / 경쟁사 분석 | IR자료 + **외부 공개자료 허용** | 출처(기관명, 연도) 필수 명기 |
| 그 외 모든 섹션 | **IR자료 + 첨부 보충자료만** | 외부 참조 및 임의 추정 절대 금지 |

확인 불가 항목 → **"확인 필요"** 표기 (공란·임의 기재 금지)

---

## 시스템 요구사항

- Claude Pro / Team / Enterprise 플랜
- 지원 브라우저: Chrome, Edge, Safari, Firefox (최신 버전)
- PDF 변환: 브라우저 인쇄 기능 사용 (별도 프로그램 불필요)

---

## 자주 묻는 질문

**Q. 한글이 깨져서 보여요**  
HTML 파일을 브라우저에서 열 때 인코딩이 UTF-8로 설정되어 있는지 확인하세요.  
브라우저에서 마우스 오른쪽 → "인코딩" → "UTF-8" 선택.

**Q. IR자료에 정보가 부족한데 어떻게 되나요?**  
확인되지 않는 항목은 모두 "확인 필요"로 자동 표기됩니다.  
DD 체크리스트에도 해당 항목이 자동 추가됩니다.

**Q. 보고서 양식을 변경하고 싶어요**  
`references/html-style-guide.md` 의 컬럼 너비 기준을 수정하거나,  
`assets/sample_report.html` 을 직접 편집하여 반영하세요.

**Q. 담당자란은 왜 항상 공란인가요?**  
보고서 작성 후 수동으로 입력하거나, "담당자를 [이름]으로 입력해줘" 라고 요청하면 자동 입력됩니다.

---

## 문의 및 지원

- GitHub Issues: `github.com/skkim4uni/krun-prescreening-report/issues`
- 운용사: K-Run Ventures
- 최종 수정일: 2026.03.27

---

> 본 스킬은 K-Run Ventures 내부 심사 기준에 따라 작성된 기밀 도구입니다.  
> 무단 배포 및 외부 공유를 금합니다.
