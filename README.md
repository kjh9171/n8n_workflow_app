# n8n Workflow App

이 저장소는 **n8n을 Docker 기반으로 실행**하고, 이를 활용해
외부 API 연동 자동화(예: 네이버 뉴스 → 텔레그램 알림)를 구현하기 위한
**실습 및 운영용 베이스 프로젝트**입니다.

RSS 기반 자동화는 외부 정책 변화로 인해 불안정할 수 있으므로,
본 프로젝트에서는 **네이버 Open API (뉴스 검색 API)** 기반의
안정적인 자동화를 기본 전략으로 사용합니다.

---

## 전체 구성 개요

* n8n : 워크플로우 자동화 플랫폼
* PostgreSQL : n8n 워크플로우 및 설정 저장소
* Docker / Docker Compose : 실행 환경
* Telegram Bot API : 알림 전송
* Naver Open API (News Search) : 뉴스 수집

```
[ Naver Open API ]
        ↓
      n8n (Cron / HTTP Request / Function)
        ↓
[ Telegram Bot ]
```

---

## 디렉토리 구조

```
n8n_workflow_app/
├─ docker-compose.yml
├─ .env               # 실행 환경 변수 (git ignore 권장)
├─ .env.example       # 환경 변수 예시
└─ README.md
```

---

## 실행 환경

* Docker
* Docker Compose
* Node.js (직접 실행 시에만 필요)

권장 환경:

* Docker Desktop (Windows / macOS)
* Linux Docker Engine

---

## 1. 환경 변수 설정

`.env` 파일을 생성하고 아래 값을 설정합니다.

```env
# PostgreSQL
POSTGRES_DB=n8n
POSTGRES_USER=n8n
POSTGRES_PASSWORD=n8n1!

# n8n 로그인 계정
N8N_USER=admin
N8N_PASSWORD=n8n1!

# Telegram Bot
TELEGRAM_BOT_TOKEN=YOUR_TELEGRAM_BOT_TOKEN
TELEGRAM_CHAT_ID=YOUR_CHAT_ID

# Naver Open API
NAVER_CLIENT_ID=YOUR_NAVER_CLIENT_ID
NAVER_CLIENT_SECRET=YOUR_NAVER_CLIENT_SECRET
```

※ `.env` 파일은 **외부 공개 금지**를 권장합니다.

---

## 2. Docker 컨테이너 실행

```bash
docker compose up -d
```

실행 후 컨테이너 확인:

```bash
docker ps
```

기본적으로 n8n은 아래 주소에서 접근 가능합니다.

```
http://localhost:5678
```

---

## 3. n8n 로그인

* ID : `N8N_USER`
* Password : `N8N_PASSWORD`

`.env`에 설정한 값을 사용합니다.

---

## 4. 워크플로우 구성 개요

### 네이버 속보 → 텔레그램 알림

워크플로우 흐름:

1. **Cron** : 5분마다 실행
2. **HTTP Request** : 네이버 Open API 뉴스 검색
3. **Function** : 데이터 정규화 (HTML 태그 제거)
4. **Function** : 중복 기사 제거
5. **Function** : 텔레그램 메시지 포맷
6. **HTTP Request** : Telegram Bot API 전송

이 방식은 RSS 차단, User-Agent 문제, 404 오류를 회피할 수 있어
**운영 환경에 적합**합니다.

---

## 5. 워크플로우 Import 방법

1. n8n UI 접속
2. `Workflows` → `Import`
3. JSON 파일 업로드 또는 클립보드 붙여넣기
4. 환경 변수 확인 후 `Active` 활성화

---

## 6. 문제 해결 가이드

### 네이버 RSS 404 오류

* 서버/컨테이너 환경에서 RSS 접근이 차단됨
* 정상적인 동작이 아님
* **네이버 Open API 사용 권장**

### Telegram 메시지가 오지 않을 때

* `TELEGRAM_CHAT_ID` 확인 (그룹은 `-` 포함)
* Bot이 채팅방에 추가되어 있는지 확인
* Workflow 활성화 여부 확인

---

## 7. 확장 아이디어

* 키워드 다중 검색 (보안, 장애, 침해사고)
* 시간대별 요약 알림
* Slack / Email / Webhook 연동
* 로그 수집 및 보안 이벤트 자동화

---

## 정리

이 프로젝트는 단순한 뉴스 봇이 아니라,
**API 기반 정보 수집 자동화 파이프라인의 출발점**입니다.

RSS에 의존하지 않고,
정책 변화에도 안정적으로 동작하는 구조를 목표로 합니다.

---


