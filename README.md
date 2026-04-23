# GitHub Actions Runner Infrastructure

운영/개발 환경을 위한 GitHub Actions Self-Hosted Runner 환경입니다.
Docker-out-of-Docker (DooD) 방식을 채택하여 러너 컨테이너 내부에서 호스트의 Docker 데몬을 제어할 수 있으며, CI/CD 파이프라인(빌드 및 배포) 구축에 최적화되어 있습니다.

## 🛠 아키텍처 및 특징 (Features & Architecture)

- **Docker-out-of-Docker (DooD)**: 러너 내부에서 Docker 명령어를 실행할 때 호스트의 자원을 직접 사용하므로, 무거운 이미지 빌드 시 성능 저하가 없습니다.
- **볼륨 영속성**: 러너가 작업을 수행하는 워크스페이스(`/tmp/runner/work`)를 볼륨으로 마운트하여 컨테이너 재시작 시에도 데이터를 유지합니다.
- **리소스 제한**: 컨테이너의 메모리 사용량을 4GB로 제한하여 호스트 서버의 안정성을 보장합니다.

## 🚀 시작하기 (Quick Start)

### 1. 환경 변수 설정
프로젝트 최상단에 `.env` 파일을 생성하고 아래 내용을 입력합니다. (보안을 위해 `.env` 파일은 Git 추적에서 제외되어야 합니다.)
```env
# GitHub Repository 또는 Organization 연결을 위한 액세스 토큰 (필수)
ACCESS_TOKEN=your_github_personal_access_token