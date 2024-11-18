---
title: Swift - 옵셔널 대해서 알아보자.
date: 2024-11-18 11:12:00 + 09:00
categories: [iOS, Swift]
tags: [swift, optional]
---

Swift에서 변수나 상수에 값이 할당되지 않았을 경우 어떤식으로 처리 할 수 있을까?
이러한 상황을 해결할 수 있는 방법 중 하나로 **옵셔널(Optional)** 사용이 있다.

옵셔널에 대해서 자세하게 알아보자.

## 옵셔널(Optional)이란?
옵셔널은 변수 또는 상수에 **값이 할당되지 않은 상황을 처리하기 위해 안전하고 일관된 접근 방식을 제공하는 타입**을 말한다.

이게 무슨 소리인지 옵셔널에 사용법과 같이 알아보겠다.

## 옵셔널(Optional) 사용법

옵셔널(Optional)은 아래와 같이 선언할 수 있다.
```swift
var optionalExample: Int?
```
위처럼 옵셔널(Optional)을 선언했을때 **아무 값도 넣지 않았을 경우 nil 이 할당**된다.
- nil: 옵셔널(Optional)에 값이 없음을 나타낸다.

>참고: 옵셔널(Optional)이 아닌 변수에는 nil이 할당될 수 없다.

옵셔널(Optional)을 선언하는 법을 알아봤으니 더 자세한 내용으로 들어가보자.

옵셔널(Optional)에 값을 할당할때는 어떤식으로 할당할까?
아주 간단하다.

```swift
var optionalExample: Int?
optionalExample = 10
```

위처럼 변수에 값을 할당하는 것과 똑같이 할당하면 된다. <br>
이처럼 옵셔널에 값이 할당되었을 경우 값이 옵셔널(Optional) 내에서 **래핑**되었다고 표현한다.

그럼 옵셔널(Optional)은 일반 변수와 무엇이 다를까?

옵셔널(Optional)이 일반 변수와 다른점은 **옵셔널 안의 값을 사용하기 위해서는 언래핑을 해줘야 한다는 점**이다.

언래핑이란 무엇인지 어떻게 사용하는지 알아보자.

## 옵셔널 언래핑
옵셔널 내에 값이 할당되었을 경우 할당된 값이 옵셔널 내에서 **래핑**되었다고 표현된다고 위에서 설명하였다.

이렇게 래핑된 옵셔널 안의 데이터를 바로 사용하면 어떤일이 일어나는지부터 확인해보자.
```swift
var example: Int? = 10
```
위 코드에서는 Int형 옵셔널(Optional) 변수에 10을 할당해주었다.
이것을 일반 변수처럼 사용하게 되면 어떤 일이 일어날까?
```swift
var example: Int? = 10
print(example) // Expression implicitly coerced from 'Int?' to 'Any'
```

실행 결과
```
Optional(10)
```

우리가 일반 변수를 사용했을때처럼 동작하지 않는다. 
왜 저런 경고문자가 뜨며 실행 결과는 왜 10이 아닌 Optional(10) 으로 뜨는 것일까?

천천히 알아보자.<br>

우선 Expression implicitly coerced from 'Int?' to 'Any' 이러한 경고 문자가 나타나는 이유를 알아보자.

옵셔널(Optional) 변수를 사용하기 위해서는 언래핑을 해줘야 한다고 위에서 설명을 하였다. 그 이유가 여기에서 나타나는 것이다.

옵셔널을 언래핑 해주지 않고 옵셔널 값을 사용할 경우 Swift 내부에서 자동 형 변환이 일어난다. 

```swift
var example: Int? = 10
print(example) // Expression implicitly coerced from 'Int?' to 'Any'
```

위 코드에서 경고 표시가 나타난 이유가 바로 이것 때문이다.


Swift 언어는 **옵셔널(Optional) 타입을 명시적으로 처리하도록 설계**되어 있기 때문에 이렇게 **자동 형 변환이 일어나는 상황에서 사용자에게 경고를 표시해주는 것**이다.

경고 메시지를 살펴보면 **Any 타입으로 자동 형 변환**된 것을 알 수 있다.

> **Any 타입이란?** 모든 타입을 저장할 수 있는 최상위 타입<br>
> Int, String, Double, Bool, Optional도 포함이 가능하다.

이렇게 옵셔널 언래핑을 하지 않았을 경우 생기는 문제점에 대해서 자세히 알아보았다. 이제 옵셔널 언래핑을 어떻게 처리하는지에 대해서 알아보자.

### 강제 언래핑
옵셔널이 nil이 아닌 값이 할당되있다는게 확실한 경우 강제 언래핑으로 옵셔널을 언래핑 할 수 있다.

강제 언래핑은 느낌표(!)를 옵셔널 변수 끝에 붙혀서 사용한다.

아래 코드를 같이 봐보자.
```swift
var example: Int?
example = 10

if example != nil{
    print(example!)
}else{
    print("값이 없음.")
}
```
위 코드처럼 옵셔널(Optional) 변수에 할당된 값이 nil이 아닐 경우에 강제 언래핑을 사용할 수 있다.

그럼 옵셔널(Optional) 변수에 값이 nil 일 경우에 강제 언래핑을 사용하면 어떻게 될까?

아래 코드에서 확인해보자.

```swift
var exmaple: Int?
print(example!)
```

실행 결과
```
error: Unexpectedly found nil while unwrapping an Optional value
```
바로 런타임 오류가 발생한다.

강제 언래핑은 옵셔널(Optional) 변수의 값이 nil 일 경우 사용하면 런타임 에러를 발생시키기 때문에 추천하는 방법은 아니다.

그렇다면 안전하게 처리하는 방법으로는 어떤 것이 있을까?
그 방법으로는 **옵셔널 바인딩**이 있다.

### 옵셔널 바인딩
옵셔널 바인딩은 옵셔널(Optional) 변수의 값이 nil 이 아닐 경우 임시 변수나 상수에 값을 할당하여 사용하는 방법이다.

아래 코드에서 확인해보자.
```swift
var example: Int? = 10

if let optionalExample = example{
    print(optionalExample)
}else{
    print("값이 없음.")
}
```

실행 결과
```
10
```

이처럼 값이 nil이 아닌 경우에 임시 변수나 상수에 할당하여 사용할 수 있다.<br>
>단 옵셔널 바인딩에 사용된 임시 변수나 상수는 if 문 안에서만 사용할 수 있다.

이러한 이유 덕분에 옵셔널(Optional) 변수의 이름과 똑같이 사용할 수도 있다.

```swift
var exmaple: Int? = 10

if let exmaple = exmaple{
    print(exmaple)
}else{
    print("값이 없음.")
}
```

실행 결과
```
10
```

이렇게 옵셔널(Optional) 변수명과 똑같이 짓어 사용할 수 있는데 좀 더 편리하게 사용하는 방법도 존재한다.

```swift
var example: Int? = 20

if let example{
    print(example)
}else{
    print("값이 없음.")
}
```

실행 결과
```
20
```

이런식으로 변수 이름을 같게 하면 할당하는 부분을 안쓰고도 옵셔널 바인딩을 할 수 있다.

또한 옵셔널(Optional) 변수의 값이 nil일 경우엔 기본값을 제공하게 할 수도 있다.

### 기본값 제공
옵셔널(Optional) 변수의 값이 nil일 경우 기본값을 사용하게 한다.
코드로 확인하겠다.

```swift
var example: Int?
print(example ?? 20)
```

실행 결과
```
20
```
이처럼 옵셔널(Optional) 변수의 값이 nil일 경우 기본값을 사용하게 만들 수도 있다.

기본값을 설정할때 옵셔널(Optional)에 사용된 데이터 타입에 꼭 맞출 필요는 없다.

```swift
var example: Int?
print(example ?? "No Data")
```
실행 결과
```
No Data
```

이런식으로 Int? 로 옵셔널(Optional) 타입을 지정하더라도 기본값으로는 다른 데이터 타입을 사용할 수 있다.

이 밖에도 암묵적 언래핑 방식이 있는데 아래에서 자세하게 설명하겠다.

## 암묵적 언래핑
암묵적 언래핑이란 **옵셔널 변수의 값이 반드시 있을 것이라고 가정하고 선언하는 방식**이다.

암묵적 언래핑을 사용하면 **옵셔널 바인딩, 강제 언래핑을 사용하지 않고도 옵셔널 변수의 값에 바로 접근**할 수 있다.

어떤식으로 사용하는지 알아보자.

### 암묵적 언래핑 사용법
옵셔널 변수를 선언할때 데이터 타입 뒤에 물음표(?)를 붙혔지만 암묵적 언래핑은 느낌표(!)를 붙혀서 사용한다.

아래에 코드를 확인해보자.
```swift
var example: Int!
```
위 코드처럼 데이터 타입 뒤에 느낌표(!)를 붙혀서 암묵적 언래핑으로 사용할 수 있다.

사용 예시를 확인해보자.

```swift
var example: Int!
example = 2

var array = ["Hello", "World", "My", "Name"]

if example != nil{
    print(array[example])
}else{
    print("값이 없음.")
}
```

실행 결과
```
My
```
이런식으로 강제 언래핑을 사용하지 않더라도 옵셔널 값에 접근할 수 있다.


이처럼 암묵적 언래핑을 사용하면 옵셔널 바인딩, 강제 언래핑을 사용하지 않고도 편리하게 옵셔널 값에 접근할 수 있는데 왜 자주 사용되지 않는 것 일까?

그 이유는 다음과 같다.

**예상치 못한 런타임 에러 발생**
- 암묵적 언래핑은 옵셔널 값이 반드시 존재하는 상황에서만 사용해야한다. 만약 옵셔널 값이 nil 이라면 런타임 에러가 발생한다.
  
**옵셔널의 목적이 사라진다**
- 옵셔널을 사용하는 이유는 변수의 값이 할당되지 않았을 경우를 처리하는데 암묵적 언래핑을 사용할 경우 값이 무조건 있어야하기 때문에 옵셔널을 사용하는데 의미가 없어진다.
  
**안전성 부족**
- 옵셔널의 값이 nil일 경우 런타임 에러가 발생하기 때문에 옵셔널 바인딩으로 안전하게 처리하는 것보다 안전성 부분에서 효율이 떨어진다.

이와 같은 이유로 옵셔널의 값으로 nil이 할당될 가능성이 조금이라도 있을 경우엔 암묵적 언래핑 사용을 피해야한다.

## 정리
옵셔널이란 변수 또는 상수의 값이 없거나 있을 수 있는 상태를 처리하는 타입으로 옵셔널에 값이 할당되면 그 값은 옵셔널 타입에 래핑된 상태로 저장된다.

옵셔널의 값에 접근하기 위해서는 언래핑을 해줘야한다.