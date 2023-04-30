# 숫자 야구(Number-Baseball)

<br/>

> 숫자 야구는 숫자를 사용하는 게임이며 두 명의 상대가 플레이하는 게임입니다. 저희는 콘솔 창에서 동작하는 숫자 야구 게임을 구현해봤습니다.
>
> 진행 기간: 2023.04.24 ~ 2023.04.28

<br/>

## 목차

1. [팀원](#팀원)
2. [타임 라인](#타임라인)
3. [Flow Chart](#Flow-Chart)
4. [실행 화면](#실행-화면)
5. [트러블 슈팅](#트러블-슈팅)
6. [참고 링크](#참고-링크)
7. [팀 회고](#팀-회고)

<br/>

## 팀원

| myungsun                                                     | yyss99(와이)                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src="https://avatars.githubusercontent.com/u/74762699?s=400&u=44a002eb9bfd2be6f192a6f994f9552d081060b8&v=4" width="250" height="250" style="border-radius: 50%;"/> | <img src="https://cdn.discordapp.com/attachments/1099908467956908102/1102102859002163311/Screenshot_20230430-1421342.png" width="250" height="250" style="border-radius: 50%;"/> |
| [Github Profile](https://github.com/myungsun7782)            | [Github Profile](https://github.com/yy-ss99)                 |

<br/>

## 타임라인

핵심 Commit 위주로 작성했습니다.

- refactor: checkNumbers 함수에서 기능 분리
- refactor: showMenu 함수 내에서 if-else if 구문을 switch 문으로 변경
- feat: 스트라이크 개수에 따른 게임 결과를 반환하는 함수 구현 
- feat: checkNumbers 함수에서 0과 중복되는 값 제거하는 로직 추가
- feat: 사용자가 입력한 임의의 수를 검증하는 함수 구현

<br/>

## Flow Chart

**[STEP 1. 순서도(Flow-Chart)]**

<img src="https://user-images.githubusercontent.com/74762699/235338235-2605f62a-4902-491a-bb1d-709806f5961e.png" style="zoom: 50%;" />

**[STEP 2. 순서도(Flow-Chart)]**

<img src="https://user-images.githubusercontent.com/74762699/235338255-35cc321f-b57c-4653-b0e1-315e825d7408.png" style="zoom:50%;" />

<br/>

## 실행 화면

1. 사용자가 게임 메뉴 옵션을 입력하는 실행 화면
   - 사용자는 1 또는 2를 선택할 수 있고, 1과 2가 아닌 다른 숫자를 입력하거나 문자를 입력할 경우 "입력이 잘못되었습니다."라는 문장을 출력합니다.

<img src="https://user-images.githubusercontent.com/74762699/235338397-a16497f6-4a53-4d26-a976-e3dd0a0372a1.gif" width="400" height="400" />

2. 사용자가 세 개의 숫자를 입력하는 실행 화면
   - 0을 제외한 한 자리 숫자 3개를 띄어쓰기로 구분하여 입력했는 지 확인한 뒤, 올바르게 입력했다면 '스트라이크와 볼 개수'를 출력해서 보여주고, 올바르지 않게 입력했다면 '입력이 잘못되었습니다.'를 출력합니다.
     - 스트라이크 기준: 사용자가 입력한 숫자와 컴퓨터의 숫자를 비교했을 때 숫자와 자리 위치가 모두 맞는 경우 
     - 볼 기준: 사용자가 입력한 숫자와 컴퓨터의 숫자를 비교했을 때 숫자만 맞는 경우

<img src="https://user-images.githubusercontent.com/74762699/235338489-1da82164-c467-4fe9-bb29-ad10190254dd.gif" width="400" height="400" />

3. 숫자 야구 게임에서 컴퓨터가 승리하는 경우 실행 화면
   - 사용자가 남은 기회 안에 스트라이크 개수를 모두 맞추지 못하면 '컴퓨터 승리...!' 를 출력하고 게임을 종료합니다.

<img src="https://user-images.githubusercontent.com/74762699/235338660-09a887e1-69c3-4ce5-9b4f-a3a455a1b09b.gif" width="400" height="400" />

4. 숫자 야구 게임에서 사용자가 승리하는 경우 실행 화면
   - 사용자가 남은 기회 안에 스트라이크 개수를 모두 맞추면 '사용자 승리!' 를 출력하고 게임을 종료합니다.

<img src="https://user-images.githubusercontent.com/74762699/235338714-840fdb5d-d3b2-4512-b055-13e4da93d4c1.gif" width="400" height="400"/>

<br/>

## 트러블 슈팅

겪었던 문제점과 고민했던 부분을 중심으로 작성했습니다.

### 함수 분리 

1. `사용자의 입력한 유효한 숫자 값을 받은 뒤 게임 결과를 알려주는 함수`를 구현할 때 `볼과 스트라이크 결과를 출력해주는 기능`과 `누가 이겼는 지에 대한 결과를 출력해주는 기능`을 묶어서 생각했습니다. 하지만, 이렇게 하면 하나의 함수에서 너무 많은 기능을 수행하게 됐습니다. 그래서 저희는 `볼과 스트라이크 결과를 출력해주는 기능`과 `누가 이겼는 지에 대한 결과를 출력해주는 기능`을 분리한 뒤, 해당 함수에서 호출하는 형태로 코드를 수정했습니다.

##### 함수 분리 전 코드 

```swift
func getGameResult(with validNumber: [Int]) -> (Bool, String?) {
    let (ballCount, strikeCount) = getBallAndStrikeResult(of: validNumber)
    let isGameOver = isGameFinished(strikeCount: strikeCount)
    
    if count >= 0 {
        print("\(strikeCount) 스트라이크, \(ballCount) 볼")
    }
    
    if strikeCount != 3 {
        print("남은 기회 : \(count)\n")
    }
    
    if strikeCount == 3 {
        return (isGameOver, "사용자 승리!")
    } else if count > 0 {
        return (isGameOver, nil)
    } else {
        return (isGameOver, "컴퓨터 승리...!")
    }
}
```

##### 함수 분리 후 코드

```swift
func getGameResult(with strikeCount: Int) -> Bool {
    if strikeCount == 3 {
        print("사용자 승리!\n")
        return false
    } else {
        print("남은 기회 : \(count)\n")
    }
    
    if count == 0 {
        print("컴퓨터 승리...!\n")
        return false
    }
    
    return true
}

func showBallAndStrikeResultWith(_ ballCount: Int, _ strikeCount: Int) {
    print("\(strikeCount) 스트라이크, \(ballCount) 볼")
}
```

2. `사용자의 숫자 입력 값에 대한 유효성 검사를 하는 함수`에 `유효하지 않은 값이 들어 있는 지를 확인하는 역할`, `한 자리 수로 구성된 숫자 배열을 반환해주는 역할` 그리고 `한 자리 수로 구성된 숫자 배열에서 중복 결과를 반환해주는 역할`이 존재했습니다. 이렇게 하다보니 하나의 함수가 너무 많은 로직과 역할을 가지게 돼서 각 역할을 함수로 나눈 뒤에 `사용자의 숫자 입력 값에 대한 유효성 검사를 하는 함수`에서 호출하도록 했습니다.

##### 함수 분리 전 코드 

```swift
func checkNumbers(for userInput: String) -> [Int]? {
    let invaildInput = -1
    let vaildNumberLength = 1
    let vaildNumberCount = 3
    let separatedInput = userInput.split(separator: " ")
                                  .map { Int($0) ?? invaildInput }
                                  .filter { $0 != 0 }
    
    if separatedInput.contains(invaildInput) ||
        Set(separatedInput.filter({ String($0).count == vaildNumberLength })).count != vaildNumberCount {
        return nil
    }
    return separatedInput
}
```

##### 함수 분리 후 코드 

```swift
func checkNumbers(for userInput: String) -> [Int]? {
    let invaildInput = -1
    let validNumberLength = 1
    let validNumberCount = 3
    let separatedInput = userInput.split(separator: " ")
                                  .map { Int($0) ?? invaildInput }
                                  .filter { $0 != 0 }
    
    if hasInvalidInput(in: separatedInput, invaildInput) ||
        hasInvalidNumberCount(in: separatedInput, validNumberCount, validNumberLength) {
        return nil
    }
    return separatedInput
}

func hasInvalidInput(in separatedInput: [Int], _ invalidInput: Int) -> Bool {
    return separatedInput.contains(invalidInput) ? true : false
}

func getValidLengthNumbers(in separatedInput: [Int], _ validNumberLength: Int) -> [Int] {
    return separatedInput.filter { String($0).count == validNumberLength }
}

func hasInvalidNumberCount(in separatedInput: [Int], _ validNumberCount: Int, _ validNumberLength: Int) -> Bool {
    let validLengthNumbers = getValidLengthNumbers(in: separatedInput, validNumberLength)
    return Set(validLengthNumbers).count != validNumberCount ? true : false
}
```

<br/>

### if-else 구문을 Switch 구문으로 변경

처음에는 `사용자에게 메뉴를 보여주는 함수`에서 사용자에게 입력받은 메뉴 숫자 번호를 입력 받은 뒤 if-else if-else 구문으로 분기 처리를 하였습니다. 하지만, 사용자가 선택할 수 있는 메뉴 번호는 1 또는 2 라는 한정된 범위였기에 switch 구문에서 각 case를 사용하여 분기를 처리하였습니다. 이렇게 코드를 수정하니 if-else문보다 코드가 더 직관적이고 가독성을 높아졌습니다. Switch문이 이런 장점 외에도 값의 범위, 튜플, 열거형 등 다양한 패턴을 사용할 수 있고, case 내에서 일치하는 값에 대한 변수 또는 상수를 선언할 수 있는 장점이 있습니다.

##### if-else if-else문을 사용한 코드

```swift
func showMenu() {
    let startOption = "1"
    let endOption = "2"
    var isMenuChoiceOn = true
    
    while isMenuChoiceOn {
        print("1. 게임시작 \n2. 게임종료 \n원하는 기능을 선택해주세요 : ", terminator: "")
        guard let menuChoice = readLine() else { continue }
        
        if menuChoice == startOption {
            startGame()
        } else if menuChoice == endOption {
            break
        } else {
            print("입력이 잘못되었습니다.")
        }
    }
}
```

##### Switch문을 사용한 코드

```swift
func showMenu() {
    let startOption = "1"
    let endOption = "2"
    var isMenuChoiceOn = true
    
    while isMenuChoiceOn {
        print("1. 게임시작 \n2. 게임종료 \n원하는 기능을 선택해주세요 : ", terminator: "")
        guard let menuChoice = readLine() else { continue }
        
        switch menuChoice {
        case startOption:
            startGame()
        case endOption:
            isMenuChoiceOn = false
        default:
            print("입력이 잘못되었습니다.")
            continue
        }
    }
}
```

<br/>

### guard문의 early-exit

`startGame` 함수에서 사용자의 게임 숫자를 옵셔널 바인딩을 통해 입력받아야 했습니다. 옵셔널 바인딩 방법에는 if let 바인딩, guard let 바인딩이 있습니다. 처음에는 if let 바인딩을 통해 입력받아서 코드를 작성했었는데, 이렇게 작성하다 보니 if let 구문 안에서 또 조건문을 처리해야 할 상황이 있었는데, 조건문을 넣게 되면 코드 들여쓰기가 2번이 초과가 됐습니다. 그래서 guard let 바인딩을 통해 guard문 아래에 조건문을 추가하여 원하는 로직을 구현할 수 있었습니다. 이 상황에서 guard문의 early exit라는 장점을 몸소 체감할 수 있었습니다.

##### guard문을 사용한 코드

```swift
func startGame() {
    var isGameOn = true
    while isGameOn {
        print("\n숫자 3개를 띄어쓰기로 구분하여 입력해주세요.\n중복 숫자는 허용하지 않습니다.\n입력 : ", terminator: "")
        
        guard let userInput = readLine(),
              let validNumber = checkNumbers(for: userInput) else {
            print("입력이 잘못되었습니다. \n")
            continue
        }
        let (ballCount, strikeCount) = getBallAndStrikeResult(of: validNumber)
        
        decreaseCount()
        showBallAndStrikeResultWith(ballCount, strikeCount)
        isGameOn = getGameResult(with: strikeCount)
    }
    resetGame()
}
```

<br/>

## 참고 링크

[Swift API Design Guidelines](https://www.swift.org/documentation/api-design-guidelines/)

[Swift API Design Guidelines(한국어 번역)](https://minsone.github.io/swift-internals/api-design-guidelines/)

[Optional Documentation](https://developer.apple.com/documentation/swift/optional)

[Swift Standard Library](https://developer.apple.com/documentation/swift/swift-standard-library)

[Github의 README 파일에 이미지/동영상 올리는 방법](https://ndb796.tistory.com/557)

<br/>

## 팀 회고

### 우리 팀이 잘한 점

- 서로 책임감이 넘치게 프로젝트를 수행 함
- 시간 약속을 아주 잘 지킴
- 서로의 피드백이 빨라서 좋았음
- 모르는 건 모른다고 질문을 하면 서로에게 최선을 다해 답변 함
- 밀도 높은 집중력
- 명확한 하루 목표를 가지고 개발을 시작함
- 의견 조율이 잘 됐음

### 우리 팀이 개선할 점 

- 초반에 convention에 맞지 않은 commit 메시지를 작성해서 push를 날린 것
- 고차 함수 컨벤션을 지키지 못하고 개발한 점
- 조금 더 명확한 이유를 가지고 근거를 제시하지 못한 점
- 페어 프로그래밍 규칙을 잘 이해하지 못 하고 진행한 점
- 서로에 대해서 알아가는 시간이 부족했던 점

### 서로에게 좋았던 점 피드백 

**[yyss99(와이)]**

- 사소한 오타나 컨벤션 오류가 많았는데 바로 수정할 수 있게 말해줘서 좋았음 
- 의견 수용을 잘 해줘서 좋았음

**[myungsun]**

- 열심히 하려고 하는 모습이 좋았음
- 쉬는 시간 없이 밀도 있게 개발하려고 하는 모습이 좋았음
- 연락이 잘 돼서 좋았음

### 서로에게 아쉬웠던 점 피드백 

**[yyss(와이)]**

- 의견을 말할 때, 근거를 더 명확하게 해서 상대방에게 설득을 하면 더 성장할 거 같다.

**[myungsun]**

- 의견을 말할 때, 근거를 더 명확하게 해서 상대방에게 설득을 하면 더 성장할 거 같다.
