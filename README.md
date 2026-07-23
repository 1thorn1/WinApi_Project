# 유피의 소원 (Yupi's Wish)

Win32 API(GDI+)와 자체 제작 2D 게임 엔진으로 만든 스토리 기반 플랫포머 게임입니다.

## 프로젝트 구조

```
WinApi_Project/
├── WinAPIMiniProject/        # 소스 코드 (Visual Studio 프로젝트)
│   ├── Engine/                # 자체 제작 게임 엔진
│   │   ├── Components/        # Transform, Collider, SpriteRenderer, Animator, Camera, TextRenderer, Script
│   │   ├── Manager/            # Scene, Render, Resource, Game, Input, Sound, Dialog, Tile, Effect, Event 매니저
│   │   ├── Object/             # GameObject
│   │   ├── Resource/           # Animation, Sprite, TileMap 등 리소스
│   │   ├── Scene/               # GameScene 기반 클래스
│   │   ├── Math/                # Vector2, Vector3
│   │   ├── Utilities/           # Singleton, Time, 열거형/구조체 정의 등
│   │   ├── FMOD/                 # FMOD 사운드 라이브러리
│   │   └── CollisionSystem.*    # 충돌 판정 시스템
│   ├── Scene/                  # 실제 게임 씬 (타이틀, 인트로, 각 스테이지, 엔딩 등)
│   ├── Script/                 # 플레이어, UI, 오브젝트 등 게임 로직 스크립트
│   ├── Asset/                   # Sprite, Sound, Font, Tile/Collider 데이터
│   └── WinAPIMiniProject.cpp   # 진입점 (WinMain, 게임 루프)
├── Build_Project/              # 실행 가능한 빌드 결과물 (exe + 리소스)
├── WinAPIMiniProject.sln       # Visual Studio 솔루션 파일
└── ReadMe.txt                   # 패치 노트 / 알려진 버그 목록
```

## 실행 방법

### 바로 실행하기
`Build_Project` 폴더의 `유피의 소원.exe`를 실행하면 됩니다. (`fmod.dll`, `Asset` 폴더가 같은 경로에 있어야 합니다.)

### 직접 빌드하기
1. `WinAPIMiniProject.sln`을 Visual Studio로 엽니다.
2. `WinAPIMiniProject`를 시작 프로젝트로 두고 빌드/실행합니다.
3. Windows 전용 프로젝트이며 GDI+ (`gdiplus.lib`)와 FMOD 사운드 라이브러리를 사용합니다.

## 조작법

| 키 | 동작 |
| --- | --- |
| ← / → | 좌우 이동 (벽 등반 시에도 사용) |
| ↑ / ↓ | 로프 등반 등 상하 이동 |
| Space | 점프 / 벽점프 |
| Shift | 대쉬 |
| Z | 우산 펼치기 / 접기 |

## 게임 엔진 구조

WinAPI(GDI+) 위에 컴포넌트 기반 구조로 직접 작성된 미니 게임 엔진입니다.

- **GameObject / Component**: Unity와 유사하게 `GameObject`에 `Transform`, `Collider`, `SpriteRenderer`, `Animator`, `Camera`, `Script` 등의 컴포넌트를 붙여서 동작합니다.
- **Scene**: `GameScene`을 상속받아 각 스테이지(저택 지역, 지하, 상층부 등)와 타이틀/인트로/엔딩 씬을 구성합니다.
- **Manager (싱글톤)**: `SceneManager`, `RenderManager`, `ResourceManager`, `InputManager`, `SoundManager`, `TileManager`, `EffectManager`, `DialogManager`, `EventManager` 등이 각자의 역할을 담당합니다.
- **게임 루프**: `WinAPIMiniProject.cpp`의 `wWinMain`에서 메시지 펌프를 돌며 `FixedUpdate → Update → LateUpdate → Render` 순서로 매 프레임 갱신합니다.

## 게임 진행 흐름 (Scene)

`Title → Intro → 저택 지역(Residential Area) → 지하(Underground) → 상층부(Upper Area) → 컷씬 → 엔딩(선택지 1/2)` 순서로 이어지는 스토리 기반 플랫포머입니다.

## 알려진 이슈 / 패치 노트

세부 버그 수정 및 변경 이력은 [`ReadMe.txt`](./ReadMe.txt)를 참고하세요.

## 참고 사항

- 소스 코드 파일은 EUC-KR(CP949)로 인코딩되어 있습니다. Visual Studio(한국어 로캘) 환경에서 여는 것을 권장합니다.
- `Y_` 접두사가 붙은 씬/스크립트 파일은 이 프로젝트에서 직접 작성한 게임 로직이며, `Engine/` 폴더는 재사용 가능한 엔진 코드입니다.
