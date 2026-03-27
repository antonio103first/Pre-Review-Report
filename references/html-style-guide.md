# HTML 스타일 가이드 — K-Run Ventures 예비심사보고서

## 기본 설정

| 항목 | 값 |
|---|---|
| 폰트 | `'MalgunGothic', '맑은 고딕', sans-serif` |
| 기본 글자 크기 | `11px` |
| 줄간격 | `1.5` |
| 페이지 여백 | `padding: 20mm 18mm` (A4 기준) |
| 최대 너비 | `max-width: 210mm` |

---

## 색상 체계

| 용도 | 값 |
|---|---|
| 주색 (네이비) | `#1a3a5c` |
| 보조색 (블루) | `#2c5282` |
| 테이블 헤더 배경 | `#1a3a5c` / 글자 흰색 |
| 홀수 행 배경 | `#ffffff` |
| 짝수 행 배경 | `#f5f8fc` |
| 테두리 | `1px solid #d0d7e3` |
| 경고 박스 배경 | `#fff8e1` / 좌측 `3px solid #f0c000` |
| 경고 박스 글자 | `#7a5f00` |

---

## 타이포그래피

| 요소 | 스타일 |
|---|---|
| `h1` (보고서 제목) | `18px`, bold, 가운데 정렬, `#1a3a5c` |
| `.subtitle` | `11px`, 가운데 정렬, `#666` |
| `h2` (섹션 제목) | `13px`, bold, `#1a3a5c`, 하단 `2px solid #1a3a5c` |
| `h3` (소제목) | `12px`, bold, `#2c5282` |
| `thead th` | `padding: 7px 10px`, bold |
| `tbody td` | `padding: 7px 10px`, `border: 1px solid #d0d7e3`, `vertical-align: top` |

---

## 강조 클래스

```css
.red    { color: #c0392b; font-weight: 700; }   /* 🔴 필수 */
.orange { color: #e67e22; font-weight: 700; }   /* 🟡 중요 */
.green  { color: #27ae60; font-weight: 700; }   /* 🟢 참고 */
.warn   { background: #fff8e1; border-left: 3px solid #f0c000;
          padding: 6px 10px; margin: 6px 0 10px; font-size: 11px; color: #7a5f00; }
.badge-ok { background: #e8f5e9; color: #27ae60; border: 1px solid #27ae60;
            border-radius: 3px; padding: 1px 7px; font-size: 10px; font-weight: 700; }
.center { text-align: center; }
.right  { text-align: right; }
.nowrap { white-space: nowrap; }
```

---

## 테이블 기본 구조

```html
<table>
  <colgroup>
    <col style="width: XX%">
    ...
  </colgroup>
  <thead><tr><th>헤더</th>...</tr></thead>
  <tbody>
    <tr><td>내용</td>...</tr>
  </tbody>
</table>
```

- `table-layout: fixed` 기본 적용
- 모든 `td`는 `white-space: normal; word-break: keep-all; overflow-wrap: break-word;` 적용
- 긴 텍스트는 자동 줄바꿈 처리

---

## 섹션별 컬럼 너비 기준

### 주주명부
| 컬럼 | 너비 |
|---|---|
| # | `28px` |
| 주주명 | `22%` |
| 구분 | `16%` |
| 주식 수 | `16%` |
| 지분율 | `12%` |
| 비고 | 나머지 |

### 핵심인력
| 컬럼 | 너비 |
|---|---|
| 구분 | `12%` |
| 성명 | `10%` |
| 역할 | `10%` |
| 주요 경력 | 나머지 (줄바꿈) |

### 주요 제품
| 컬럼 | 너비 |
|---|---|
| 제품명 | `18%` |
| 유형 | `13%` |
| 설명 | `34.5%` (줄바꿈) |
| 주요 고객군 | `34.5%` (줄바꿈) |

### 주요 기술 테이블
| 컬럼 | 너비 |
|---|---|
| 기술명 | `22%` |
| 내용 | 나머지 (줄바꿈) |
| 기술 수준 | `12%` |

### 시장 규모
| 컬럼 | 너비 |
|---|---|
| 구분 | `28%` |
| 2024년 | `13%` |
| 전망 | `16%` |
| 연평균 성장률 | `13%` |
| 출처 | `30%` (줄바꿈) |

### 경쟁 우위 요약
| 컬럼 | 너비 |
|---|---|
| 항목 | `18%` |
| 내용 | 나머지 (줄바꿈) |

### 주요 고객
| 컬럼 | 너비 |
|---|---|
| # | `28px` |
| 고객사명 | `22%` (줄바꿈) |
| 유형 | `12%` |
| 계약 상태 | `12%` |
| 주요 계약 내용 | 나머지 (줄바꿈) |
| 연간 규모 | `12%` |

### 수주 현황 및 계획
| 컬럼 | 너비 |
|---|---|
| 구분 | `14%` |
| 내용 | 나머지 (줄바꿈) |
| 금액 | `16%` |
| 시기 | `14%` |

### DD 체크리스트
| 컬럼 | 너비 |
|---|---|
| # | `28px` |
| 확인 항목 | 나머지 |
| 중요도 | `70px` |
| 현황 | `60px` |
| 담당 | `70px` |

### 종합 의견
| 컬럼 | 너비 |
|---|---|
| 항목 | `120px` (`.col-label`) |
| 평점 | `center` |
| 세부 의견 | 나머지 (줄바꿈) |

---

## 개요 테이블 (.overview-table)

```css
.overview-table td:first-child {
  font-weight: 700;
  width: 140px;
  white-space: nowrap;
}
```

---

## 푸터

```html
<footer>
  <span>K-Run Ventures | 케이런7호 | 내부 검토용 기밀 문서</span>
  <span>작성일: YYYY.MM.DD</span>
</footer>
```

```css
footer {
  margin-top: 30px;
  padding-top: 8px;
  border-top: 1px solid #ccc;
  font-size: 10px;
  color: #888;
  display: flex;
  justify-content: space-between;
}
```

---

## 전체 CSS 템플릿

```html
<style>
  @font-face {
    font-family: 'MalgunGothic';
    src: url('fonts/MALGUN.TTF') format('truetype');
    font-weight: 400;
  }
  @font-face {
    font-family: 'MalgunGothic';
    src: url('fonts/MALGUNBD.TTF') format('truetype');
    font-weight: 700;
  }
  @font-face {
    font-family: 'MalgunGothic';
    src: url('fonts/MALGUNSL.TTF') format('truetype');
    font-weight: 300;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: 'MalgunGothic', '맑은 고딕', sans-serif;
    font-size: 11px; line-height: 1.5; color: #222;
    padding: 20mm 18mm; max-width: 210mm; margin: 0 auto;
  }
  h1 { font-size: 18px; font-weight: 700; text-align: center;
       margin-bottom: 6px; color: #1a3a5c; }
  .subtitle { text-align: center; font-size: 11px; color: #666; margin-bottom: 20px; }
  h2 { font-size: 13px; font-weight: 700; color: #1a3a5c;
       border-bottom: 2px solid #1a3a5c; padding-bottom: 4px; margin: 22px 0 10px; }
  h3 { font-size: 12px; font-weight: 700; color: #2c5282; margin: 14px 0 6px; }
  table { width: 100%; border-collapse: collapse; font-size: 11px;
          margin-bottom: 10px; table-layout: fixed; }
  thead tr { background-color: #1a3a5c; color: #fff; }
  thead th { padding: 7px 10px; text-align: left; font-weight: 700;
             white-space: normal; word-break: keep-all; }
  tbody tr:nth-child(odd)  { background-color: #ffffff; }
  tbody tr:nth-child(even) { background-color: #f5f8fc; }
  tbody td { padding: 7px 10px; border: 1px solid #d0d7e3; vertical-align: top;
             white-space: normal; word-break: keep-all; overflow-wrap: break-word; }
  .center { text-align: center; } .right { text-align: right; }
  .nowrap { white-space: nowrap; }
  .warn { background: #fff8e1; border-left: 3px solid #f0c000;
          padding: 6px 10px; margin: 6px 0 10px; font-size: 11px; color: #7a5f00; }
  .red    { color: #c0392b; font-weight: 700; }
  .orange { color: #e67e22; font-weight: 700; }
  .green  { color: #27ae60; font-weight: 700; }
  .desc { font-size: 11px; line-height: 1.6; margin-bottom: 8px; color: #333; }
  pre { background: #f4f6f9; border: 1px solid #d0d7e3; border-radius: 4px;
        padding: 10px 14px; font-family: 'Courier New', monospace; font-size: 10px;
        line-height: 1.6; margin-bottom: 10px; white-space: pre; overflow-x: auto; }
  .overview-table td:first-child { font-weight: 700; width: 140px; white-space: nowrap; }
  .source-note { font-size: 10px; color: #555; margin: -6px 0 10px; padding-left: 4px; }
  .badge-ok { display: inline-block; background: #e8f5e9; color: #27ae60;
              border: 1px solid #27ae60; border-radius: 3px; padding: 1px 7px;
              font-size: 10px; font-weight: 700; }
  footer { margin-top: 30px; padding-top: 8px; border-top: 1px solid #ccc;
           font-size: 10px; color: #888; display: flex; justify-content: space-between; }
</style>
```
