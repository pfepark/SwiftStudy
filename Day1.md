##Day1
### 변수와 상수
````swift
var n1 : Int = 10
var n2 = 10				// 우변 초기값으로 타입 결정
//var n3				// 초기값 필요

var n5 : Int = 10		// 변수
let c1 : Int = 10		// 상수

var s1 : String = "hello"  // 문자열
var ch1 : Character = "A"  // 문자.. 주의 'A' 가 아님
//var ch2 : Character = "AB"  // error. "AB"는 String!!

var n6 : Int32 = 10
//var n7 : Int64 = n6 // error
var n7 : Int64 = Int64(n6) // ok.. 명시적 변환

var max = Int.max
var min = Int.min

var n1 = 10
var n2 = 0x10   // 16진수
var n3 = 0o10   // 8진수
var n4 = 0b10   // 2진수
var n5 = 1_000_000        // typedef

typealias int = Int32
````

### 연산자
````swift
if (a=b)  //C에서는 버그.. swift는 =가 void를 리턴하므로 컴파일 에러

// overflow : &+, &- &%
var n1 : Int = Int.max + 1  // error
var n1 : Int = Int.max &+ 1 // ok

// range operator
for num in (0...5)
{
  print(num)
}
0
1
2
3
4
5

var r = 0....5
var r2 : CountableClosedRange<Int> = CountableClosedRange<Int>( uncheckedBounds:(lower:0 upper:5) )
for num in r2
{
  print(num)
}
  
````
