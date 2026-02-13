# Jenkins CI/CD Pipeline 구축

GitLab 기반 형상관리 체계 운영 구조  
Jenkins 기반 CI/CD 파이프라인 구성 구조  
빌드와 배포 단계 분리 설계 구조  

---

## 목표

수동 빌드 및 배포 과정 자동화 구조  
인적 오류 최소화 구조  
배포 일관성 및 재현성 확보 구조  
운영 안정성 향상 구조  

- 형상관리 기반 소스 코드 관리 체계 확립
- CI/CD 자동화 체계 구축
- WAR 기반 배포 표준 수립
- 운영 환경 안정성 확보

---

## 전체 구성

| 구분 | 내용 |
|------|------|
| 형상관리 | GitLab |
| CI | Jenkins |
| 빌드 산출물 | WAR |
| 아티팩트 저장소 | Nexus Repository |
| CD | Jenkins |
| 배포 대상 | WAS 서버 |

---

## CI 단계 (Continuous Integration)

소스 코드 빌드 및 패키징 전담 구조  

### CI 흐름

1. 개발자 GitLab 코드 Push  
2. Jenkins CI 소스 Checkout  
3. Maven 빌드 수행  
   - 컴파일  
   - 테스트  
   - WAR 패키징  
4. Nexus Repository 업로드  

### CI 역할

- 소스 코드 컴파일 구조  
- 단일 WAR 산출물 생성 구조  
- 중앙 저장소 기반 산출물 관리 구조  

CI 단계에서만 빌드 수행  
CD 단계에서는 빌드 과정 미포함 구조  

---

## CD 단계 (Continuous Deployment)

사전 생성 WAR 파일 기반 배포 전담 구조  

### CD 흐름

1. Nexus Repository WAR 다운로드  
2. 대상 WAS 서버 배포  
3. 서비스 중지  
4. WAR 교체  
5. 서비스 재기동  

### CD 역할

- 소스 코드 미접근 구조  
- 빌드 미수행 구조  
- 단일 WAR 기반 배포 구조  
- 배포 재현성 확보 구조  

---

## CI/CD 분리 설계

| 항목 | 설계 목적 |
|------|-----------|
| 책임 분리 | 빌드와 배포 역할 분리 구조 |
| 환경 격리 | 빌드 환경과 운영 환경 분리 구조 |
| 안정성 | 빌드 실패와 운영 영향 분리 구조 |
| 재현성 | 동일 WAR 기반 다중 환경 배포 구조 |
| 확장성 | 배포 대상 증가 시 확장 용이 구조 |

---

## 구성 특징

- CI/CD 단계 분리 구조  
- Repository 기반 Artifact 관리 구조  
- 단일 빌드 산출물 표준화 구조  
- 중앙 저장소 기반 배포 관리 구조  

---

## 아키텍처 다이어그램

```
Developer → GitLab → Jenkins CI
                         ↓
                       Nexus
                         ↓
                   Jenkins CD → WAS
```
