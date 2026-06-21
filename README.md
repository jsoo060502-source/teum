# 틈 — 충동과 행동 사이

> 숏폼 충동·할 일 회피·스트레스가 치솟는 **그 순간** 바로 개입해, 30초 안에 작은 대응을 시작하도록 돕는 개인용 웹앱(PWA).

기존의 “기분 일기”가 지나간 감정을 적는 데 그친다면, **틈**은 감정과 충동이 *일어나는 순간*에 개입하는 것이 핵심입니다.

## 핵심 기능 (PRD 3개 모듈)

| 모듈 | 하는 일 |
| --- | --- |
| **시청 관리** | 플랫폼 선택 → 목표 시간 설정 → 세션 시작/종료(시간 자동 계산) → 목표 초과 시 알림과 “한 번 더 볼까?” 재확인 → 예상 vs 실제 비교 + 기분(1~5) + 메모 |
| **정서 조절** *(핵심)* | 상황 선택(회피·스트레스·숏폼 충동) → 감정 강도(1~5) → 대응 도구 실행 → 효과(1~5)·실제 행동(했다/회피)·메모 기록 |
| **패턴 보기** | 오늘/이번 주 요약(시청 시간·대응 횟수·성공률), 기분–시청 연결 그래프, 트리거 빈도, 도구 효과 비교 |

**대응 도구 4종**
- 🌿 5-4-3-2-1 그라운딩 — 호흡과 함께 주변 감각을 차례로 찾기
- 🏷️ 감정에 이름 붙이기 — 지금 감정을 한두 단어로 적어 거리 두기
- ⏱️ 딱 2분만 시작하기 — 할 일의 작은 첫 행동만, 2분 타이머
- ⏳ 5분만 미루고 다시 보기 — 충동을 흘려보낸 뒤 다시 판단

## 기술

- 서버 없는 단일 페이지 웹앱 — 순수 HTML/CSS/JavaScript
- 데이터는 전부 **브라우저 localStorage**에 저장 (서버 전송 없음)
- 세션·대응 타이머: `setInterval` + `Date`
- 알림: 브라우저 Notification API + 화면 내 배너
- 그래프: 의존성 없는 자체 SVG/CSS 차트
- **PWA**: `manifest.json` + 서비스워커로 설치·오프라인 지원

## 파일 구성

```
index.html              앱 본체 (HTML/CSS/JS 한 파일)
manifest.json           PWA 매니페스트
sw.js                   서비스워커 (오프라인 캐시)
icon-192.png            앱 아이콘
icon-512.png
icon-512-maskable.png
```

## GitHub Pages로 배포하기

### 방법 1 — 웹에서 바로 (가장 쉬움)
1. GitHub에서 **New repository** 생성 (예: `teum`), Public 선택
2. **Add file → Upload files** 로 이 폴더의 모든 파일 업로드 → Commit
3. **Settings → Pages** 이동
4. *Build and deployment* 의 Source를 **Deploy from a branch**, Branch를 **main / (root)** 로 선택하고 Save
5. 1~2분 뒤 `https://<아이디>.github.io/teum/` 에서 열립니다

### 방법 2 — git 명령어로
```bash
git init
git add .
git commit -m "틈: 충동제어 PWA"
git branch -M main
git remote add origin https://github.com/<아이디>/teum.git
git push -u origin main
# 이후 Settings → Pages 에서 main/(root) 지정
```

> 모바일 크롬·사파리에서 열어 **홈 화면에 추가**하면 앱처럼 설치됩니다.
> 모든 기록은 그 기기에만 저장되며 서버로 전송되지 않습니다.
