# 멍BTI - 반려견 성격 유형 & AI 코칭 앱

강아지 성격을 MBTI처럼 8가지 유형으로 분류하고, AI가 맞춤 훈련을 코칭해주는 반려견 교육 앱.

## 기술 스택

| 영역 | 기술 |
|------|------|
| 프론트엔드 | Next.js 15 (App Router), TypeScript, Tailwind CSS |
| 백엔드/DB | Supabase (PostgreSQL + Auth + Realtime) |
| 엣지 함수 | Cloudflare Workers |
| AI | Claude API (`claude-sonnet-4-20250514`) |

## 프로젝트 구조

```
src/
├── app/           # Next.js App Router 페이지
├── components/    # 공통 UI 컴포넌트
├── lib/           # 유틸리티, API 클라이언트
└── types/         # TypeScript 타입 정의
```

## 멍BTI 8가지 유형 체계

유형 코드는 3축으로 구성됩니다:
- **S/A**: Social(사교적) / Aloof(독립적)
- **E/C**: Energetic(활발) / Calm(차분)
- **B/N**: Bold(대담) / Nervous(불안)

| 유형 코드 | 이름 | 특징 |
|-----------|------|------|
| **SEB** | 에너지 넘치는 사교왕 | 사교적이고 활발하며 대담함 |
| **SEN** | 밝지만 불안한 에너지볼 | 사교적이고 활발하지만 불안감이 있음 |
| **SCB** | 조용한 애교쟁이 | 사교적이고 차분하며 대담함 |
| **SCN** | 소심한 애교쟁이 | 사교적이고 차분하지만 소심함 |
| **AEB** | 독립적 에너자이저 | 독립적이고 활발하며 대담함 |
| **AEN** | 반응형 독립군 | 독립적이고 활발하지만 불안감이 있음 |
| **ACB** | 차분한 철학자 | 독립적이고 차분하며 대담함 |
| **ACN** | 예민한 은둔자 | 독립적이고 차분하며 예민함 |

## 핵심 기능 플로우

```
9문항 성격 테스트 → 유형 도출 → AI 코치 채팅
```

1. **성격 테스트**: 9개 질문으로 S/A, E/C, B/N 3축 측정
2. **유형 도출**: 답변 집계 → 8가지 유형 중 하나 매핑
3. **AI 코치 채팅**: Claude API로 유형별 맞춤 훈련 방법 코칭

## 타겟 사용자

- **환경**: 한국 아파트 거주 반려견 보호자
- **경험**: 초보 반려견 보호자 (훈련 지식이 적음)
- **니즈**: 내 강아지 성격에 맞는 구체적인 훈련 방법

## 환경 변수

`.env.local` 파일에 설정 (절대 커밋 금지):

```
NEXT_PUBLIC_SUPABASE_URL=      # Supabase 프로젝트 URL
NEXT_PUBLIC_SUPABASE_ANON_KEY= # Supabase anon/public key
ANTHROPIC_API_KEY=             # Claude API 키
```

## 개발 시작

```bash
npm run dev     # 개발 서버 실행 (http://localhost:3000)
npm run build   # 프로덕션 빌드
npm run lint    # 린트 검사
```

## 주의사항

- Claude API 호출은 반드시 서버 사이드(Route Handler 또는 Cloudflare Workers)에서 수행
- `ANTHROPIC_API_KEY`는 절대 클라이언트에 노출 금지 (`NEXT_PUBLIC_` 접두사 사용 불가)
- Supabase RLS(Row Level Security) 정책 반드시 적용
