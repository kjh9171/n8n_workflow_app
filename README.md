

# 📦 n8n Workflow App

n8n_workflow_app은 **n8n 기반의 노코드(코드 없는) 워크플로우 자동화 플랫폼**을 위한 환경 구성 및 예제입니다.

이 프로젝트는 n8n을 빠르게 실행하고, 워크플로우를 작성/확장/배포하는 데 필요한 설정 및 Docker 기반 구동 구성을 포함합니다.

---

## 📌 주요 기능

* **n8n 자동화 플랫폼 구성**
  n8n을 Docker Compose로 실행할 수 있는 기본 설정 제공

* **워크플로우 데이터 저장**
  n8n에서 생성한 워크플로우를 PostgreSQL 등에 저장할 수 있는 환경

* **개발용/테스트용 환경 제공**
  로컬에서 자동화 테스트 및 워크플로우 수정/확인 가능

---

## 🚀 시작하기

아래 명령으로 필요한 구성 요소를 바로 실행하세요.

### 1. 저장소 클론

```bash
git clone https://github.com/kjh9171/n8n_workflow_app.git
cd n8n_workflow_app
```

### 2. 환경 설정

`.env` 파일을 프로젝트 루트에 생성하고 다음과 같이 설정합니다:

```bash
# 기본 n8n 환경값
N8N_HOST=localhost
N8N_PORT=5678
N8N_PROTOCOL=http

# DB 설정
POSTGRES_USER=your_user
POSTGRES_PASSWORD=your_password
POSTGRES_DB=n8n

# 기타 필요 인증 키 등
```

> `.env`는 민감 정보가 포함될 수 있으므로 절대 공개 저장소에 올리지 마세요.

---

## 📦 Docker Compose 실행

```bash
docker-compose up -d
```

이 명령으로 구성된 서비스들이 실행됩니다:

* n8n Node 기반 워크플로우 자동화 서버
* PostgreSQL 데이터베이스
* (필요 시) 추가 서비스들

실행 후 브라우저에서 **[http://localhost:5678**로](http://localhost:5678**로) 접속하면 n8n UI가 나타납니다.

---

## 🧠 n8n 소개 (배경)

n8n은 시각적 워크플로우 빌더 기반의 **노코드 + 코드 자동화 도구**입니다. 400개 이상의 서비스 통합을 제공하며, 복잡한 자동화 과정을 드래그·드롭으로 구성할 수 있습니다. ([GitHub][2])

n8n의 장점은 다음과 같아요:

* 시각적 편집을 통한 자동화 흐름 구성
* 필요하면 JavaScript/Python 코드 삽입 가능
* 자체 호스팅 가능(완전 제어)
* 다양한 트리거(웹훅, 일정, 이벤트 등) 지원

---

## 📌 활용 예시

* GitHub 이벤트를 받아 자동 이슈 생성
* 이메일 알림 및 보고서 자동 발송
* 데이터베이스 간 데이터 동기화
* AI 기반 자동 요약/분석 워크플로우 실행

(실제 예시들은 워크플로우 JSON 파일로 저장하여 n8n UI에 **Import → 실행** 형태로 적용할 수 있음)

---

## 📘 리소스

n8n 공식 문서 및 참고 링크

* n8n 공식 홈페이지: [https://n8n.io](https://n8n.io)
* n8n GitHub: [https://github.com/n8n-io/n8n](https://github.com/n8n-io/n8n)
* GitHub 통합 자동화 예시(워크플로우 템플릿) 참고 자료

---

[1]: https://github.com/kjh9171/n8n_workflow_app "GitHub - kjh9171/n8n_workflow_app: n8n, 노코드 자동화 플랫폼"
[2]: https://github.com/n8n-io?utm_source=chatgpt.com "n8n - Workflow Automation - GitHub"
