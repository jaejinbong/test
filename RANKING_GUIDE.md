# 🏆 가을하늘 맞추기 게임 - 글로벌 랭킹 시스템 가이드

## 📊 글로벌 랭킹 시스템 소개
이 게임은 모든 사용자의 점수를 GitHub Pages를 통해 공유하는 글로벌 랭킹 시스템을 제공합니다.

## 🎮 사용자를 위한 안내
- 게임을 플레이하면 자동으로 로컬에 점수가 저장됩니다
- 게임 시작 시 자동으로 전 세계 사용자들의 랭킹을 불러옵니다
- 결과 페이지에서 나의 순위와 전체 랭킹을 확인할 수 있습니다

## 🛠️ 관리자를 위한 랭킹 업데이트 방법

### 방법 1: 랭킹 업데이트 도구 사용 (권장)
1. 브라우저에서 `update_rankings.html` 파일을 엽니다
2. "로컬 랭킹 불러오기" 클릭 - 내 브라우저의 기록을 불러옵니다
3. "글로벌 랭킹 불러오기" 클릭 - 서버의 기존 랭킹을 가져옵니다
4. "랭킹 병합하기" 클릭 - 두 데이터를 합칩니다
5. "JSON 파일 다운로드" 클릭 - `rankings.json` 파일을 다운로드합니다
6. 다운로드한 파일을 GitHub 리포지토리에 커밋합니다:
   ```bash
   git add rankings.json
   git commit -m "Update global rankings"
   git push
   ```

### 방법 2: 수동 업데이트
1. 브라우저 개발자 도구 콘솔에서 다음 명령 실행:
   ```javascript
   // 로컬 랭킹 데이터 추출
   const localScores = JSON.parse(localStorage.getItem('all_scores') || '[]');
   const globalCache = JSON.parse(localStorage.getItem('global_rankings') || '[]');
   const allRankings = [...localScores, ...globalCache];
   console.log(JSON.stringify(allRankings, null, 2));
   ```
2. 출력된 JSON을 복사하여 `rankings.json` 파일에 저장
3. GitHub에 커밋 및 푸시

### 방법 3: GitHub Actions 자동화 (향후 구현 예정)
- 자동으로 랭킹 데이터를 수집하고 업데이트하는 시스템
- 현재는 수동 업데이트가 필요합니다

## 📁 파일 구조
- `twin-guess-game.html` - 메인 게임 파일
- `rankings.json` - 글로벌 랭킹 데이터 저장 파일
- `update_rankings.html` - 랭킹 업데이트 도구

## 🔄 랭킹 동기화 흐름
1. 사용자가 게임 완료 → 로컬 스토리지에 저장
2. 게임 시작 시 → GitHub Pages에서 글로벌 랭킹 로드
3. 결과 페이지 → 로컬 + 글로벌 랭킹 병합하여 표시
4. 관리자가 정기적으로 → 랭킹 데이터 수집 및 GitHub 업데이트

## ⚠️ 주의사항
- `rankings.json` 파일은 GitHub Pages를 통해 공개됩니다
- 최대 500개의 기록만 유지됩니다 (성능 최적화)
- 중복 기록은 자동으로 제거됩니다

## 🌐 GitHub Pages URL
- 게임: https://jaejinbong.github.io/test/twin-guess-game.html
- 랭킹 데이터: https://jaejinbong.github.io/test/rankings.json

## 💡 문제 해결
- 랭킹이 표시되지 않는 경우: 브라우저 콘솔에서 오류 확인
- 랭킹 업데이트 후 반영이 안 되는 경우: GitHub Pages 캐시 때문일 수 있으니 5-10분 대기
- CORS 오류 발생 시: 로컬 파일로 직접 실행하지 말고 웹 서버를 통해 접속

## 📞 지원
문제가 있으시면 GitHub Issues에 문의해주세요.