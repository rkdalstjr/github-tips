# Docker 사용법
WSL: Ubuntu가 설치되어 있지 않다면 api-test01의 README.md을 참고하여 환경을 세팅하세요.
본 문서는 api-test03을 기반으로 합니다.
## 새로운 환경 세팅
- docker desktop 설치
- setting > Resources > WSL integration

위 경로에서 Enable integration 설정을 on으로 하고 restart

VS code 확장앱 설치
- docker compose
- docker container

## 설치 플러그인 확인
```
docker compose version    # v5.1.x  — 멀티 컨테이너 오케스트레이션
docker buildx version     # v0.33.x — 멀티 플랫폼 빌드
docker model              # Docker Model Runner — sLLM 서빙
docker mcp                # MCP Plugin — AI 에이전트 툴 연동
docker scout version      # 이미지 취약점 스캔
docker ai version         # Docker AI Agent (Gordon)
```

## 공유 네트워크 생성
```
exec sudo su -l $USER
docker network create shared-net
docker network ls | grep shared-net
```

## daemon.json 권장 설정
Docker Desktop > Settings > Docker Engine
```
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "log-driver": "json-file",
  "log-opts": {
    "max-file": "3",
    "max-size": "10m"
  }
}
```
변경 후 restart

## WSL2 메모리 제한 설정
```
C:\Users\<username>\.wslconfig 파일 생성
```
```
[wsl2]
memory=4GB
processors=2
swap=2GB
localhostForwarding=true
```
wsl --shutdown 이후 재시작
본인 PC 세팅에 맞추어 하지 않으면 렉을 유발합니다.

## docker 로그인
```
docker version
docker login
```

## 로컬 LLM OLLAMA
### 이미지 pull
```
docker pull ollama/ollama:latest
```

### 컨테이너 실행
```
docker run -d \
  --name ollama \
  -p 11434:11434 \
  -v ollama-data:/root/.ollama \
  ollama/ollama:latest
```
백그라운드에서 컨테이너 생성 및 실행 > ollama라고 이름 생성 > 호스트의 11434 포트와 컨테이너의 11434 포트 연결 > 컨테이너가 삭제되어도 영구 보관 명령 > 이미지 실행

### 추론 API 테스트
```
curl -s http://localhost:11434/api/generate \
  -H "Content-Type: application/json" \
  -d '{"model":"llama3.2:1b","prompt":"hello","stream":false}'
```
실행시 시간이 조금 필요합니다.

### 실행 중인 모델 목록 확인
```
curl -s http://localhost:11434/api/tags | python3 -m json.tool
```

## Qdrant — 벡터 데이터베이스
### 이미지 pull
```
docker pull qdrant/qdrant:latest
```

### 컨테이너 실행
```
docker run -d \
  --name qdrant \
  -p 6333:6333 \
  -p 6334:6334 \
  -v qdrant-data:/qdrant/storage \
  qdrant/qdrant:latest
```
백그라운드에서 컨테이너 생성 및 실행 > qdrant라고 이름 생성 > 호스트의 6333/6334 포트와 컨테이너의 6333/6334 포트 연결 > 컨테이너가 삭제되어도 영구 보관 명령 > 이미지 실행
| 포트 | 용도 |
|---|---|
| `6333` | REST API / Web UI |
| `6334` | gRPC API |

### 헬스체크
```
curl -s http://localhost:6333/healthz
# 응답: {"title":"qdrant - vector search engine","version":"..."}
```

### Web UI 접속
브라우저에서 http://localhost:6333/dashboard 를 엽니다.

## 이미지, 컨테이너 상태 확인
```
# 이미지 목록
docker image ls

# 실행 중인 컨테이너
docker ps

# 전체 컨테이너(정지 포함)
docker ps -a
```

## 컨테이너 중지, 재시작, 삭제
```
# 중지
docker stop ollama qdrant

# 재시작
docker start ollama qdrant

# 삭제 (중지 후)
docker stop ollama qdrant
docker rm ollama qdrant

# 이미지 삭제
docker rmi ollama/ollama:latest qdrant/qdrant:latest
```

## Docker Compose로 한 번에 실행
위 두 서비스를 한 번에 실행하려면 docker-compose.yml을 사용합니다. 다른 사용자에게 공유하거나 컴퓨터 재부팅 후 실행할 때 사용하기 편리합니다.
```
# 파일 위치 확인
find . -name "*docker-compose.yml" -type f 2>/dev/null

# 디렉터리 이동
cd ~/docker-class/docker-basics/03-Pull-from-DockerHub-and-Run-Docker-Images

# 전체 스택 기동(이미 실행 중이면 오류 발생)
docker compose up -d

# 로그 확인(Ctrl C를 통해 로그 > 터미널 제어권 복구)
docker compose logs -f

# 전체 스택 종료 및 정리
docker compose down
```

# 추가 개념
## 이미지 ≠ 사진
위에서 사용한 이미지라는 단어는 사진이 아닙니다. 컴퓨터가 이해할 수 있는 특별한 압축 파일을 의미합니다. 

## 컨테이너 레지스트리
- docker hub : 세상 모든 사람이 쓰는 공개 앱스토어
- 컨테이너 레지스트리 : 회사 전용 사내 앱스토어 (비공개, 보안)

## 쿠버네티스
- docker : 한 대의 컴퓨터에서 컨테이너를 띄우는 도구
- 쿠버네티스 : 수백~수천 대의 컴퓨터(클러스터)에 컨테이너를 알아서 분배하고 관리

## 정리
```
[ 개발 환경 ]
    │
    ├── 1. Dockerfile (텍스트 설계도)
    │       │
    │       ▼
    ├── 2. Docker Image (이미지 파일)  ← 📦 컨테이너 레지스트리에 저장/공유
    │       │
    │       ▼
    ├── 3. Docker Container (단일 서버 실행) ← ⚙️ docker run / docker compose
    │       │
    │       ▼
    └── 4. Kubernetes (대규모 분산 실행) ← ☸️ 수백 대 서버에서 컨테이너 운영
```
