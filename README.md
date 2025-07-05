# **OnCare**
 **OnCare 👩‍⚕️: 돌봄(care)을 항상 키고있겠다(On)는 의미의 OnCare.**<br>
> 요양보호사와 사회복지사의 업무를 자동화하여 효율성을 높이는 서비스.
> 1) 음성 기반 상담 일지 초안 작성(STT)
> 2) AI 프롬프트 기반 상담 일지 및 주간 보고서 작성<br>

## 백엔드 소개
 | [김현희](https://github.com/Kim-Hyunhee) | [김난영](https://github.com/Algoruu) |
| -- | -- |
| <img src="https://avatars.githubusercontent.com/u/96518301?v=4" width="120" />  | <img src="https://avatars.githubusercontent.com/u/126838925?v=4" width="120" />  |
| <p align="center">BE</p> | <p align="center">BE</p> |

## 목차
1. [실행 환경](#실행-환경)  
   1-1. [환경 변수](#환경-변수)  
2. [기술 스택](#기술-스택)  
3. [폴더 구조](#폴더-구조)  
4. [ERD](#erd)   
5. [기능 구현 목록](#기능-구현-목록)
6. [Swagger 문서](#swagger-문서)

<br>

## 실행 환경
### 환경 변수
- 아래 항목들이 `.env` 파일에 반드시 존재해야 합니다:
  - `AWS_ACCESS_KEY_ID`: AWS 서비스에 접근하기 위한 액세스 키 ID

  - `AWS_SECRET_ACCESS_KEY`: AWS 서비스에 접근하기 위한 비밀 키

  - `AWS_DEFAULT_REGION`: AWS 리소스가 위치한 기본 리전(예: ap-northeast-2)

  - `DATABASE_URL`: 데이터베이스 연결에 사용되는 URL (DB 종류, 사용자, 비밀번호, 호스트, 포트 등 포함)

  - `AWS_S3_BUCKET_NAME`: 파일 업로드/다운로드에 사용할 S3 버킷 이름

  - `OPENAI_API_KEY`: OpenAI API 호출을 위한 인증 키 (예: Whisper, GPT 등 사용 시)

  - `KAKAO_CLIENT_ID`: 카카오 OAuth 인증을 위한 REST API 키

  - `KAKAO_REDIRECT_URI`: 카카오 로그인 이후 리다이렉트될 URI

  - `JWT_SECRET`: JWT 토큰 생성 시 서명에 사용할 비밀 키

  - `JWT_ACCESS_EXPIRATION`: 액세스 토큰 만료 시간 (예: 1h, 15m 등)

  - `JWT_REFRESH_EXPIRATION`: 리프레시 토큰 만료 시간 (예: 7d, 30d 등)

  - `FRONTEND_URL`: 백엔드에서 허용할 프론트엔드 도메인 주소 (CORS 설정 등에 사용)


<br>



## 기술 스택
### 백엔드
![NestJS](https://img.shields.io/badge/nestjs-%23E0234E.svg?style=for-the-badge&logo=nestjs&logoColor=white) ![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white) ![postgresql](https://img.shields.io/badge/postgresql-4169E1.svg?style=for-the-badge&logo=mysql&logoColor=white) ![Prisma](https://img.shields.io/badge/Prisma-3982CE?style=for-the-badge&logo=Prisma&logoColor=white) ![Swagger](https://img.shields.io/badge/-Swagger-85EA2D?style=for-the-badge&logo=swagger&logoColor=white)

### AWS
![AWS](https://img.shields.io/badge/AWS-232F3E.svg?style=for-the-badge&logo=amazonwebservices&logoColor=white) ![AWS RDS](https://img.shields.io/badge/AWS%20RDS-527FFF.svg?style=for-the-badge&logo=amazonrds&logoColor=white) ![AWS S3](https://img.shields.io/badge/AWS%20S3-569A31.svg?style=for-the-badge&logo=amazons3&logoColor=white)

### CI/CD
![AWS ECS](https://img.shields.io/badge/AWS%20ECS-FF9900.svg?style=for-the-badge&logo=amazonec2&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF.svg?style=for-the-badge&logo=githubactions&logoColor=white)


<br>

## 폴더 구조

<details>
<summary><strong>✨폴더 구조✨</strong></summary>
<div markdown="1">
 
```bash
nestjs-oncare-project/
├── eslint.config.mjs                # ESLint 설정 파일
├── nest-cli.json                    # NestJS CLI 설정 파일
├── package.json                     # 프로젝트 의존성 및 스크립트 정의
├── README.md                        # 프로젝트 소개 및 설명 문서
├── test.html                        # 테스트용 HTML 파일
├── tsconfig.build.json              # 빌드용 TypeScript 설정
├── tsconfig.json                    # 전체 TypeScript 설정
├── prisma/                          # Prisma 관련 폴더
│   └── schema.prisma                # Prisma 스키마 파일
├── python/                          # Python 관련 기능 폴더
│   ├── main.py                      # Python 진입점(main)
│   ├── requirements.txt             # Python 패키지 목록
│   ├── 상담일지양식.docx             # 상담일지 워드 양식
│   ├── 주간보고서양식.docx           # 주간보고서 워드 양식
│   ├── report/                      # 보고서 생성 관련 Python 코드
│   │   └── service.py
│   ├── stt/                         # 음성(STT) 관련 Python 코드
│   │   └── service.py
│   └── weekly_report/               # 주간보고서 생성 Python 코드
│       └── service.py
├── src/                             # NestJS 백엔드 소스 코드
│   ├── app.controller.spec.ts        # App 컨트롤러 테스트
│   ├── app.controller.ts             # App 컨트롤러
│   ├── app.module.ts                 # App 모듈
│   ├── app.service.ts                # App 서비스
│   ├── main.ts                       # 서버 실행 진입점
│   ├── auth/                        # 인증/인가 관련 코드
│   │   ├── auth.controller.ts
│   │   ├── auth.module.ts
│   │   ├── auth.service.ts
│   │   ├── decorators/              # 커스텀 데코레이터
│   │   │   └── current-user.decorator.ts
│   │   ├── dto/                     # 데이터 전송 객체(인증)
│   │   │   ├── complete-signup.dto.ts
│   │   │   ├── login-response.dto.ts
│   │   │   ├── refresh-token.dto.ts
│   │   ├── guards/                  # 인증 가드
│   │   │   ├── jwt-auth.guard.ts
│   │   │   └── kakao-auth.guard.ts
│   │   └── strategies/              # 인증 전략(JWT, 카카오)
│   │       ├── jwt.strategy.ts
│   │       └── kakao.strategy.ts
│   ├── careworker/                  # 요양보호사 관련 기능
│   │   ├── careworker.controller.ts
│   │   ├── careworker.module.ts
│   │   ├── careworker.service.ts
│   │   └── dto/
│   │       ├── get-careworkers.dto.ts
│   │       └── get-works.dto.ts
│   ├── client/                      # 내담자(클라이언트) 관련 기능
│   │   ├── client.controller.ts
│   │   ├── client.module.ts
│   │   ├── client.service.ts
│   │   └── dto/
│   │       ├── create-client.dto.ts
│   │       └── update-client.dto.ts
│   ├── journal/                     # 상담일지 관련 기능
│   │   ├── journal.controller.ts
│   │   ├── journal.gateway.ts       # 실시간 통신(Gateway)
│   │   ├── journal.module.ts
│   │   ├── journal.service.ts
│   │   ├── normalize-string-fields.ts
│   │   └── dto/
│   │       ├── download-url-response.dto.ts
│   │       ├── file-upload.dto.ts
│   │       ├── generate-journal-docx-response.dto.ts
│   │       ├── journal-list-item.dto.ts
│   │       ├── journal-summary-response.dto.ts
│   │       ├── journal-updated.dto.ts
│   │       └── update-transcript.dto.ts
│   ├── prisma/                      # Prisma 서비스 모듈
│   │   ├── prisma.module.ts
│   │   └── prisma.service.ts
│   ├── report/                      # 보고서 관련 기능
│   │   ├── report.controller.ts
│   │   ├── report.module.ts
│   │   ├── report.service.ts
│   │   └── dto/
│   │       ├── create-report.dto.ts
│   │       ├── create-weekly-report-flexible.dto.ts
│   │       ├── create-weekly-report-response.dto.ts
│   │       ├── create-weekly-report.dto.ts
│   │       └── journal-summary-item.dto.ts
│   ├── s3/                          # AWS S3 연동 모듈
│   │   ├── s3.module.ts
│   │   └── s3.service.ts
│   ├── users/                       # 사용자(유저) 관련 기능
│   │   ├── users.controller.ts
│   │   ├── users.module.ts
│   │   └── users.service.ts
│   └── work/                        # 근무(Work) 관련 기능
│       ├── work.controller.ts
│       ├── work.module.ts
│       ├── work.service.ts
│       └── dto/
│           └── create-work.dto.ts
├── test/                            # 테스트 코드
│   ├── app.e2e-spec.ts
│   └── jest-e2e.json
```
</div>
</details>

<br>

## **ERD**

<details>
<summary><strong>✨ERD 이미지 보기✨</strong></summary>
<div markdown="1">

![ERD 이미지](https://github.com/user-attachments/assets/2a551efa-9dda-447e-b411-3ea2dce10733)

</div>
</details>

<br>

## 기능 구현 목록

### **1️⃣ 요양보호사 (Careworker)**
- **요양보호사 목록 조회** (`GET /careworker`)
- **이번 주 근무 현황 조회** (`GET /careworker/works/this-week`)
- **기간별 근무 이력 조회** (`GET /careworker/works/date-range`)
<br>

### **2️⃣ 회원가입 & 인증 (Auth)**
- **카카오 로그인 시작** (`GET /auth/kakao`)
- **카카오 로그인 콜백** (`GET /auth/kakao/callback`)
- **로그아웃** (`GET /auth/logout`)
- **회원 정보 조회/탈퇴** (`GET, DELETE /auth/me`)
- **액세스 토큰 갱신** (`POST /auth/refresh`)
- **회원가입 완료(요양보호사/사회복지사 역할 선택)** (`POST /auth/complete-signup`)
<br>

### **3️⃣ 노인 관리 (Client)**
- **노인 정보 목록 조회** (`GET /client`)
- **노인 정보 상세 조회** (`GET /client/{id}`)
- **특정 노인 상담일지 목록 조회** (`GET /client/{clientId}/journal`)
- **특정 노인 담당 요양보호사 수정** (`PATCH /client/{id}/care-worker`)
- **노인 정보 생성** (`POST /client`)
- **노인 정보 수정** (`PUT /client/{id}`)
<br>

### **4️⃣ 상담일지 관리 (Journal)**
- **일지 목록 조회(기간별)** (`GET /journal/list/date-range`)
- **상담일지 문서 상세 조회** (`GET /journal/{id}`)
- **원본 음성 파일 듣기** (`GET /journal/{id}/raw-audio`)
- **STT 결과 수정** (`PATCH /journal/{id}/edit-transcript`)
- **상담일지 요약 및 문서 생성** (`POST /journal/{id}/summary`)
- **상담일지 PDF 변환** (`POST /journal/{id}/convert-pdf`)
- **상담일지 DOCX presigned url 반환** (`POST /journal/{id}/download-docx`)
- **상담일지 PDF presigned url 반환** (`POST /journal/{id}/download-pdf`)
<br>

### **5️⃣ 보고서 관리 (Report)**
- **주간보고서 상세 조회** (`GET /report/{id}`)
- **주간보고서 생성(선택한 일지 그룹 지정)** (`POST /report`)
- **주간보고서 DOCX presigned url 반환** (`POST /report/{id}/download-docx`)
- **주간보고서 PDF presigned url 반환** (`POST /report/{id}/download-pdf`)
<br>

### **6️⃣ 근무 관리 (Work)**
- **근무 시작** (`POST /work/start`)
- **근무 종료** (`POST /work/end`)
<br>

## **Swagger 문서**
Swagger를 통해 API 목록을 확인할 수 있습니다.<br>
아래 링크를 클릭하여 Swagger 문서로 이동하세요.<br>


**[📄 Swagger 문서 보러 가기](https://github.com/user-attachments/assets/967322a1-de60-4c2b-8048-363489511866)**



---
[👆 맨 위로 올라가기](#oncare)