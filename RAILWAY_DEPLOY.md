# Railway 배포 가이드

## 📋 배포 준비

### 1. Railway 프로젝트 생성
1. [Railway](https://railway.app) 웹사이트 접속
2. GitHub 계정으로 로그인
3. "New Project" 클릭
4. "Deploy from GitHub repo" 선택
5. `cmhblue1225/gamehub-portver` 저장소 선택

### 2. 환경 변수 설정
Railway 대시보드에서 다음 환경 변수를 설정해야 합니다:

#### 필수 환경 변수
```
NODE_ENV=production
PORT=3000
```

#### Supabase 환경 변수
```
SUPABASE_URL=your_supabase_url
SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
```

#### AI API 키 (선택사항, AI 게임 생성 기능에 필요)
```
CLAUDE_API_KEY=your_claude_api_key
OPENAI_API_KEY=your_openai_api_key
```

### 3. 빌드 설정
Railway는 자동으로 다음 설정을 사용합니다:
- **빌드 명령어**: `npm install`
- **시작 명령어**: `npm start`
- **Node.js 버전**: 18.x (nixpacks.toml에 정의됨)

### 4. 배포 실행
1. 모든 환경 변수를 설정한 후 "Deploy" 버튼 클릭
2. 배포 로그를 확인하여 성공적으로 배포되었는지 확인
3. Railway가 제공하는 URL로 접속하여 애플리케이션 확인

## 🚀 자동 배포
- GitHub의 `main` 브랜치에 푸시하면 자동으로 Railway에 배포됩니다
- 배포 상태는 Railway 대시보드에서 확인할 수 있습니다

## 🔍 배포 확인
배포가 완료되면 다음 엔드포인트들을 확인하세요:
- `/` - 메인 페이지
- `/api/health` - 헬스체크 (선택사항)
- `/games` - 게임 목록

## ⚙️ 주요 설정 파일
- `railway.json` - Railway 배포 설정
- `nixpacks.toml` - Nixpacks 빌드 설정
- `package.json` - Node.js 프로젝트 설정

## 🐛 트러블슈팅

### 포트 문제
Railway는 자동으로 `PORT` 환경 변수를 설정합니다.
`server/index.js`에서 다음과 같이 포트를 설정해야 합니다:
```javascript
const PORT = process.env.PORT || 3000;
```

### 환경 변수 누락
배포 로그에서 환경 변수 관련 오류가 발생하면:
1. Railway 대시보드의 Variables 탭 확인
2. 모든 필수 환경 변수가 설정되어 있는지 확인
3. 환경 변수 업데이트 후 재배포

### 빌드 실패
- `package.json`의 dependencies가 올바른지 확인
- Node.js 버전 호환성 확인 (18.x 권장)
- 빌드 로그를 확인하여 구체적인 오류 메시지 파악

## 📊 모니터링
Railway 대시보드에서 다음을 모니터링할 수 있습니다:
- CPU 및 메모리 사용량
- 배포 로그
- 네트워크 트래픽
- 애플리케이션 메트릭

## 💰 비용
- Railway는 무료 티어를 제공합니다
- 월 $5 크레딧 포함
- 사용량에 따라 추가 요금 발생 가능

## 🔗 유용한 링크
- [Railway 공식 문서](https://docs.railway.app)
- [Nixpacks 문서](https://nixpacks.com)
- [GitHub 저장소](https://github.com/cmhblue1225/gamehub-portver)
