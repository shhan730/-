---
layout: post
title: "Swift ValueType vs ReferenceType"
date: 2019-08-06
tag: [swift]
author: Han-SeungHun
---

# Swift로 알아보는 Value Type(값 타입) 과 Reference Type(참조 타입)의 차이점



Swift를 학습하다 보면 Value Type과 Reference Type 이라는 단어를 자주 볼 수 있습니다.

Swift상에서 Value Type과 Reference Type의 예시에 대해 알아보고

두개의 타입의 차이점을 실제 코드의 관점과 메모리의 관점에서 비교해 보고자 합니다.



## Swift에서 Value Type과 Reference Type의 종류



Swift에서 값 타입과 참조타입을 나누자면 다음과 같습니다.

|                     Value Type (값 타입)                     |    Reference Type (참조타입)    |
| :----------------------------------------------------------: | :-----------------------------: |
| 구조체(Structure)<br />열거타입(Enumerated type)<br />튜플(Tuple) | 클래스 인스턴스(Class Instance) |





이제 이 두가지 타입의 차이점에 대해 코드 관점으로 비교하여 봅시다.



## 실제 코드 관점에서의 차이점



###Value Type(값 타입)



값타입에는 대표적으로 구조체(Structure)가 있습니다.

이러한 값타입들의 특징은 **개별 인스턴스들이 각각의 독립된 사본으로 존재한다는 것 입니다.**

코드로 자세히 설명해 보도록 하겠습니다.



* Code

~~~swift
struct S {
  var data: Int = -1 
}
var a = S()
var b = a
a.data = 42
println("\(a.data), \(b.data)")
~~~



* Result

~~~bash
42 1
~~~



대표적인 값타입인 구조체를 생성한 후 내부에 프로퍼티(멤버변수)를 생성하였습니다.

이후 구조체의 인스턴스를 생성해 변수 a에 저장한 후, 변수 b에 변수 a에 있는 인스턴스를 대입하였습니다.

이후, a에 저장되어있는 인스턴스의 프로퍼티에 42를 저장하였습니다.

이때 a와 b의 프로퍼티를 모두 출력해 보면 **a와 b의 프로퍼티 값이 다른 것을 확인할 수 있습니다.**



이유는 간단합니다.

위에서 설명했듯이 값 타입들은 **개별 인스턴스들이 각각의 독립된 사본으로 존재하기 때문입니다.**

따라서 a의 저장된 인스턴스를 b에 대입하였을때 **실제 b에는 인스턴스의 사본이 저장된 것 입니다.**



``a.data = 42`` 는 a 내부 프로퍼티에만 저장이 된것이고 b의 프로퍼티는 -1이 그대로 남아있기 때문에

출력 값이 다음과 같이 나타난 것입니다.



###Reference Type(참조타입)



참조타입에는 대표적으로 클래스의 인스턴스가 있습니다.

이러한 참조타입들의 특징은 **암시적으로 공유된 인스턴스를 가진다는 것 입니다.**

코드로 자세히 설명해 보도록 하겠습니다.



* Code

~~~swift
class C {
  var data: Int = -1
}
var x = C()
var y = x
x.data = 42
println("\(x.data), \(y.data)") // "42, 42"
~~~



* Result

~~~bash
42 42
~~~



클래스를 생성한 후 내부에 프로퍼티(멤버변수)를 생성하였습니다.

이후 클래스의 인스턴스를 생성해 변수 x에 저장한 후, 변수 y에 변수 x에 있는 인스턴스를 대입하였습니다.

이후, x에 저장되어있는 인스턴스의 프로퍼티에 42를 저장하였습니다.

이때 x와 y의 프로퍼티를 모두 출력해 보면 **x와 y의 프로퍼티 값이 같은 것을 확인할 수 있습니다.**



이유는 간단합니다.

위에서 설명했듯이 참조 타입들은 **암시적으로 공유된 인스턴스를 가지기 때문입니다.**

따라서 x의 저장된 인스턴스를 y에 대입하였을때 **x와 y는 공유된 인스턴스를 가지는 것 입니다.**



## 메모리 관점에서의 차이점



### 메모리(Memory)의 구조



| 영역  |        역할        |
| :---: | :----------------: |
| Stack | 지역변수, 매개변수 |
| Heap  |      동적할당      |
| Data  | 전역변수, 정적변수 |
| Code  |   프로그램 Code    |



메모리는 그냥 사용하면 매우 비효율적 입니다.

따라서 우리는 메모리구조를 4개의 논리영역으로 나누어 사용합니다.

(Stack, Heap, Data, Code)



### Struct Instance 와 Class Instance 의 메모리 사용 차이점



* Struct Instance

~~~swift
struct Example{
	var num1:Int = 4
  var num2:Int = 5
}
~~~

이러한 구조체의 인스턴스가 메모리에 어떤식으로 저장되는지 알아봅시다.





| 영역  |                        저장된 Data                         |
| :---: | :--------------------------------------------------------: |
| Stack |                     num1 = 4, num2 = 5                     |
| Heap  |                                                            |
| Data  |                                                            |
| Code  | 프로그램 Code<br />var num1:Int = 4<br/>  var num2:Int = 5 |

값타입인 Struct는 다음과 같이 내부 프로퍼티가 Stack에 저장되었습니다.

**만약 Example의 인스턴스를 생성한다면 새로운 인스턴스의 프로퍼티는 Stack에 추가되어 새로 저장됩니다.**





* Class Instance



대표적인 Swift의 클래스인 UIView를 활용하겠습니다.

~~~Swift
var ci:UIView = UIView()
~~~

이러한 클래스의 인스턴스가 메모리에 어떤식으로 저장되는지 알아봅시다.





| 영역  |                 저장된 Data                 |
| :---: | :-----------------------------------------: |
| Stack |        ci 인스턴스 주소 (ci:UIView)         |
| Heap  |         UIView 인스턴스 (UIView())          |
| Data  |                                             |
| Code  | 프로그램 Code<br />var ci:UIView = UIView() |

레퍼런스 타입인 클래스의 인스턴스의 예시입니다.

일단 클래스의 인스턴스 자체는 Heap영역에 저장이 되었습니다.

하지만 인스턴스를 가르키는 ci는 Stack 영역에 저장되었습니다.



## 수고하셨습니다.

Swift언어에서의 값타입과 참조타입에 대하여 알아보았습니다.

더 자세한 내용을 공부하고자 할 경우 [여기](https://developer.apple.com/swift/blog/?id=10)를 참고하십시오.

