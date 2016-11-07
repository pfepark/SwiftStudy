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

### Optional
````swift
var n1 : Int = nil  // error
var n2 : Optional<Int> = nil
n2 = 10
print(n2)   // Optional(10)
print(n2!)  // 10

var s1 = "10"       // "10sdf"이면 캐스팅 실패
var n3 = Int(s1)    // 실패 가능성이 있는 모든 함수, 캐스팅 등은 리턴값이 Optional

if (n3 == nil)
{
    // failure
}
else
{
    print("\(n3!)")
}

var n4 : Optional<Int> = nil
var n5 : Int? = nil		// 축약 표기
````

### Tuple
````swift
var t1 : (Int, Double) = (1, 3.14)
var t2 = (1, 3.14)		// 초기화시 (  ) 나오면 Tuple

var n1 = t1.0		// tuple의 0번째 요소 접근
var (n3, d1) = t1
var (_, d2) = t1	// _ 첫번째 요소는 생략

var pt = (x:1, y:2)
var x = pt.0
var y = pt.y
````

### Array
````swift
var arr1 : Array<Int> = [1,2,3]
var arr2 : [Int] = [1,2,3]
var arr3 = [1,2,3]

// array object
print( arr1.isEmpty )
print( arr1.count )

arr1.append(7)

print( arr1 )

// [ ] operator
var ar1 = [1,2,3]
var ar2 = [1,2,3]

var ar3 = ar1 + ar2
ar3[0] = 10

ar3[0...2] = [7,8,9]
ar3[3...5] = ar1[0...2]

print(ar3)

// 순회
for num in ar3
{
    print(num)
}

for (idx, num) in ar3.enumerated()  // (index, value)
{
    print(idx, num)
}

// 배열은 객체이므로 맴버함수가 있다
ar3.removeAll()
````
