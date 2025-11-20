# Git Flow 전략 정리

## 브랜치 구조

* **main**: 배포용
* **dev**: 개발 통합
* **feature/**: 기능 개발
* **release/**: 릴리스 준비
* **hotfix/**: 운영 긴급 패치

---

## 1. feature 개발 후 dev 반영 → release에서 수정 없이 main 배포

```
feature → dev → release → main → dev
```

* 정상 릴리스 흐름
* release 브랜치에서 추가 작업 없음
* main 배포 후 dev와 동기화 필요(Fast-forward 가능)

---

## 2. feature 개발 후 dev 반영 → release에서 수정 발생 → main 배포

```
feature → dev → release(수정 필요) → feature 추가생성 → dev → release → main → dev
```

* release 단계에서 큰 수정이나 신규 수정이 필요할 경우
* release 브랜치에서 직접 수정하지 않고 **새로운 feature 브랜치 생성**해 처리
* 수정 브랜치를 dev에 병합 후 새로운 release 생성 또는 기존 release에 병합
* 최종 main 배포 후 dev와 main 동기화 유지

---

## 3. feature 개발 후 dev 반영 → main 배포했는데 hotfix 발생한 상황

```
feature → dev → release → main → hotfix → main → dev
```

* 운영 이슈 발생 시 hotfix 생성 후 main에 즉시 반영
* hotfix 변경사항도 dev에 재병합하여 코드베이스 동기화 유지
* dev에 병합 누락 시 이후 release 시 충돌 가능

## 핵심 정리

* release에서 수정 발생 시 **release -> feature 추가생성 -> dev** 병합 필수
* hotfix 발생 시 **hotfix -> main -> dev** 병합 필수
* dev를 항상 main과 동기화하여 충돌 최소화
