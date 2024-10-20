# 🎮 Korean Tightrope - 전통 외줄타기 tvOS 게임

**Korean Tightrope**는 한국 전통놀이인 외줄타기를 테마로 한 tvOS용 게임입니다. 외줄 위에서 캐릭터를 조종하여 균형을 잡고, 장애물을 피하며, 목표에 도달하는 도전적인 게임을 제공합니다. 캐릭터의 움직임과 점프 동작을 통해 외줄타기 고유의 긴장감과 재미를 느껴보세요.

## 📱 시뮬레이션
| 게임 화면 | 점프 동작 | 장애물 피하기 |
|---------------|---------------|---------------|
| <img src="https://github.com/user-attachments/assets/gameplay1.png" width="200" /> | <img src="https://github.com/user-attachments/assets/gameplay2.png" width="200" /> | <img src="https://github.com/user-attachments/assets/gameplay3.png" width="200" /> |

## ⚙️ 주요 기능
- **외줄타기 동작 구현**: 캐릭터가 외줄 위에서 균형을 잡고 움직임
- **장애물 피하기**: 캐릭터가 장애물을 피하면서 목표에 도달
- **점프 액션**: 장애물이나 간격을 뛰어넘는 점프 기능
- **점수 시스템**: 플레이어의 성과에 따른 점수 기록

## 💻 개발 환경
- **개발 기간**: 2024년 6월 1일 ~ 2024년 6월 15일
- **개발 인원**: 1명
- **개발 도구**:
    - **IDE**: Xcode 15.3
    - **버전 관리**: Git
 
## 🛠️ 기술 스택
- **UI**: UIKit – 게임 UI 및 캐릭터 제어 구현
- **애니메이션**: SpriteKit – 캐릭터 움직임과 장애물 피하기 애니메이션
- **게임 로직**: Swift – 외줄타기 게임 규칙 및 점수 계산 로직

## 📁 디렉토리 구조
```
KoreanTightrope
├── Application
│   ├── AppDelegate.swift
│   └── SceneDelegate.swift
├── Resources
│   ├── Characters
│   ├── Obstacles
│   └── Sounds
├── GameLogic
│   ├── GameScene.swift
│   ├── Character.swift
│   └── Obstacle.swift
└── UI
    ├── GameViewController.swift
    ├── MainMenuViewController.swift
    └── ScoreViewController.swift
```


## 🤔 고민한 부분
- **균형 잡기**: 외줄 위에서 캐릭터가 자연스럽게 균형을 잡는 물리적 동작 구현
- **게임 난이도 조정**: 초보자와 숙련자를 위한 난이도 조절 기능 추가

## 😨 트러블 슈팅
- **장애물 랜덤 생성 문제**: 일정한 규칙 없이 장애물이 랜덤하게 생성되는 문제를 해결해 게임의 재미 요소를 극대화
- **캐릭터 점프 반응 속도 개선**: 점프 타이밍이 늦어지는 문제를 해결하여 사용자의 반응 속도에 맞는 게임 진행 가능

## 🧑‍⚖️ GitHub Convention
- **Commit**: `[FEAT/#33] 점프 동작 추가`
- **Branch** : `feat/#33-gameplay-jump`
- **Issue** : `[FEAT] 게임플레이 점프 기능 구현`
- **PR** : `[PR/#33] 게임플레이 점프 기능 구현`
- **Merge** : `[MERGE/#33(이슈 번호)] -> develop`

