# Vampire Survivors 클론 — 웹 빌드

**플레이: https://vibe-coding-team-study.github.io/vampire-survivors-web/**

WASD 로 이동. 무기는 자동 발사. 레벨업 시 3지선다.

---

## ⚠️ 이 저장소는 산출물 전용이다

Godot 웹 export 결과만 들어 있다. **직접 편집하지 말 것** — 다음 배포에서 통째로 덮어써진다.

소스는 **비공개 저장소**에 있고, 배포는 그쪽 `tools/deploy_web.sh` 가 한다.

## 왜 저장소가 두 개인가

GitHub Pages 는 **Free 플랜에서 public 저장소만** 지원한다(Pro/Team 이면 private 도 가능).
소스 저장소는 private 이고 조직 플랜이 free 라 그쪽으로는 Pages 를 켤 수 없다.

그래서 소스는 비공개로 두고 **산출물만** 이 public 저장소에 커밋한다. 게임을 공개하는 것이
어차피 목적이므로 산출물 공개는 문제가 되지 않는다.

## 빌드 구성

| | |
|---|---|
| 엔진 | Godot 4.7 stable (비-mono) |
| 언어 | GDScript |
| 스레드 | **싱글스레드** (`variant/thread_support=false`) |

싱글스레드인 이유: 멀티스레드 wasm 은 `SharedArrayBuffer` 를 쓰고, 그러려면 서버가
**cross-origin isolation 헤더**(COOP/COEP)를 보내야 한다. **GitHub Pages 는 커스텀 헤더를
설정할 수 없다.** Godot 4.3 에서 복원된 싱글스레드 빌드를 쓰면 헤더가 아예 불필요하다.
대가는 성능이며, 2D 게임이라 받아들였다.

`.nojekyll` 이 있는 이유: Jekyll 이 `_` 로 시작하는 파일을 무시하기 때문이다.
현재 산출물에는 해당 파일이 없지만 비용이 0 이고 함정이 크다.
