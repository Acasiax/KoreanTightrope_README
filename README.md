# 🎮 Korean Tightrope - 전통 외줄타기 tvOS 게임

**Korean Tightrope**는 한국 전통놀이인 외줄타기를 테마로 한 tvOS용 게임입니다. 외줄 위에서 캐릭터를 조종하여 균형을 잡고, 장애물을 피하며, 목표에 도달하는 도전적인 게임을 제공합니다. 캐릭터의 움직임과 점프 동작을 통해 외줄타기 고유의 긴장감과 재미를 느껴보세요.

## 📱 시뮬레이션
| 점프 동작 | 장애물 피하기 & 출동 | 게임 화면 | 
|---------------|---------------|---------------|
| <img src="https://github.com/user-attachments/assets/dc25a38d-de30-4ad5-a470-9868c0fd10d4" width="300" /> | <img src="https://github.com/user-attachments/assets/af960008-0170-4612-984d-a69d8d6e1a51" width="300" /> |  <img src="https://github.com/user-attachments/assets/8deea044-41bf-43b0-8d81-f5090a5ef993" width="300" /> |

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
- **배포 대상**: tvOS 17.0

 
## 🛠️ 기술 스택
- **UI**: `UIKit` – 게임의 사용자 인터페이스 및 캐릭터 제어 기능 구현
- **애니메이션**: `SpriteKit` – 캐릭터의 움직임, 장애물 피하기, 배경 애니메이션 구현
- **게임 로직**: `Swift` – 외줄타기 게임의 규칙과 점수 계산 로직
- **사운드**: `AVFoundation` – 배경 음악 및 사운드 효과 처리
- **물리 엔진**: `GameplayKit` – 캐릭터와 장애물 간의 물리 상호작용 및 게임의 물리 효과 처리


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

### 1. **균형 잡기 구현**
캐릭터가 외줄 위에서 자연스럽게 균형을 잡을 수 있도록 물리 동작을 구현했습니다. 캐릭터의 `physicsBody`를 세부적으로 조정해, 충돌 시 튕기지 않도록 하고 회전도 방지했습니다. 중력도 조정하여 점프 시 자연스러운 상승과 하강을 구현했습니다.

```swift
let frontColliderSize = CGSizeMake(5, character.size.height * 0.80)
let frontCollider = SKPhysicsBody(rectangleOf: frontColliderSize, center: CGPointMake(25, 0))
frontCollider.collisionBitMask = GameManager.sharedInstance.COLLIDER_OBSTACLE

let bottomColliderSize = CGSizeMake(character.size.width / 2, 5)
let bottomCollider = SKPhysicsBody(rectangleOf: bottomColliderSize, center: CGPointMake(0, -(character.size.height / 2)))

character.physicsBody = SKPhysicsBody(bodies: [frontCollider, bottomCollider])
character.physicsBody?.restitution = 0 // 충돌 시 튕기지 않도록 설정
character.physicsBody?.linearDamping = 0.1 // 이동 시 서서히 감속하도록 설정
character.physicsBody?.allowsRotation = false // 회전 방지
character.physicsBody?.mass = 0.1 // 캐릭터 질량
```

###2. **점프 중복 방지**
점프 중인 동안에는 다시 점프하지 못하도록 플래그 isJumping을 사용해 방지했습니다. 점프가 완료되기 전까지는 추가 점프가 불가능합니다.
```swift
@objc func jump(_ gesture: UITapGestureRecognizer){
    if isJumping == false {
        isJumping = true
        let impulseY: CGFloat = 60.0
        character.physicsBody?.applyImpulse(CGVectorMake(0.0, impulseY))
    }
}

```

###3. **난이도 조정**
땅의 속도와 캐릭터가 밟는 지면의 크기, 간격을 조정하여 게임의 난이도를 조절했습니다. 더 빠른 속도와 좁은 지면을 통해 난이도를 높이고, 반대로 설정하면 초보자도 쉽게 플레이할 수 있도록 설정했습니다.
```swift
let groundSpeed: CGFloat = 8.5  // 난이도에 따라 속도 조절 가능
let ASP_PIECES = 15  // 지면의 개수를 통해 난이도 조절
```


## 😨 트러블 슈팅
1. 장애물 랜덤 생성 문제 해결
장애물이 일정한 간격으로만 생성되던 문제를 해결하기 위해, 장애물의 생성 간격을 랜덤하게 변경했습니다. 이로 인해 예측할 수 없는 난관을 제공하며, 게임의 재미 요소를 극대화했습니다.

```swift
let randomXPosition = CGFloat(arc4random_uniform(100)) // 장애물의 X 위치를 랜덤으로 설정
let randomYPosition = CGFloat(arc4random_uniform(50) + 100) // 장애물의 Y 위치를 약간의 범위 내에서 랜덤하게 설정
obstacle.position = CGPoint(x: randomXPosition, y: randomYPosition)
```

2. 캐릭터 점프 반응 속도 개선
캐릭터가 점프할 때 느려지거나 반응이 즉각적이지 않은 문제를 해결하기 위해, 점프 시 즉각적으로 힘을 적용하는 방법을 최적화했습니다. 이를 통해 점프 타이밍이 더 정확해졌습니다.

```swift
// 즉시 적용되는 점프 힘
let impulseY: CGFloat = 60.0
character.physicsBody?.applyImpulse(CGVectorMake(0.0, impulseY))
```

3. 게임 오버 처리 및 사용자 피드백
캐릭터가 일정 범위를 벗어나면 게임 오버가 되도록 했으며, Game Over 메시지와 함께 사용자가 게임이 끝났음을 직관적으로 알 수 있게 구현했습니다.

```swift
func endGame() {
    guard !gameEnded else { return }
    setupGameOverLabel()  // 게임 오버 메시지 설정
    self.removeAllActions()  // 모든 액션 제거
    print("게임 종료")  // 디버그 메시지
    gameEnded = true
}
```
