# v6 테스트: AI 비서실장 배포 안내

이 안내는 **테스트 프로젝트 전용**입니다. 운영용 v5 또는 운영 Supabase 프로젝트에는 적용하지 마세요.

## 준비물
- Supabase 테스트 프로젝트 관리자 접근 권한
- Google AI Studio에서 발급한 Gemini API 키
- Supabase CLI (로컬 PC에서 실행)

## 배포 절차

1. 테스트 프로젝트의 Supabase 대시보드에서 **Project Settings → General → Project ID**를 확인합니다.
2. PC 터미널에서 저장소를 내려받고 다음 명령을 실행합니다.

```powershell
npx supabase login
npx supabase link --project-ref <테스트_프로젝트_ID>
npx supabase secrets set GEMINI_API_KEY="<본인의_Gemini_API_키>"
npx supabase functions deploy ai-chief
```

**주의:** API 키는 GitHub, config.js, index.html에 절대 넣지 마세요. 터미널 명령 기록에 남지 않도록 비밀키 입력 방식에도 주의하세요. SUPABASE_URL 및 SUPABASE_ANON_KEY는 Supabase Edge Functions의 기본 환경변수입니다.

3. Supabase 대시보드 **Edge Functions → ai-chief**에서 함수 배포 상태를 확인합니다.
4. 테스트 웹사이트에서 로그인하고 업무 지시 화면의 **AI 비서실장 분석 요청**을 눌러봅니다. 추천된 팀과 이유가 표시되면 성공입니다.

## 문제 해결
- 401: 로그인 세션 및 함수 JWT 검증 설정 확인
- 403: 허용된 GitHub Pages 주소에서 요청했는지 확인
- 503: 서버의 Gemini 비밀키 설정 확인
- 502: Gemini 모델/API 사용 권한, 할당량, 응답 형식 확인
- 함수 미배포: 기존 키워드 추천 기능은 계속 사용 가능

## 운영 전 필수 작업
현재 코드는 **시험용**입니다. 여러 사용자가 이용하기 전에 서버 측 사용자별 요청량 제한, 비용 상한, 호출 기록, 예외 처리, 접근 권한 정책을 추가하세요. 브라우저 버튼 비활성화만으로 비용을 제한할 수 없습니다.
