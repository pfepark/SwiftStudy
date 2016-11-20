## Day2
#### function
````swift
// arg1, arg2는 호출할 때 사용하는 이름
// a, b는 함수내부에서 사용하는 이름
// postfix return syntax : C++등 다른 언어도 새롭게 도입되는 문법
func Add1( arg1 a : Int, arg2 b : Int ) -> Int
{
	print("Add1")
	return a+b
}

// 호출할 때나 함수안에서 같은 이름 a,b를 사용
func Add2( a : Int, b : Int ) -> Int
{
	return a+b
}

// 호출할 때 _는 이름 생략
func Add3( _ a : Int, _ b : Int) -> Int
{
	return a+b
}

func Add4( _ a : Int, b : Int) -> Int
{
	return a+b
}

// 함수 호출 방법 예제
var ret1 = Add1( arg1 : 2, arg2 : 3 )
var ret2 = Add2( a : 2, b : 3 )
var ret3 = Add3( 2, 3 )
var ret4 = Add4( 2, b : 3 )

func foo() -> Void	// Void 생략 가능
{
}

// 여러개 리턴하고 싶을 때
func goo() -> ( code:Int, msg:String )
{
	return (480, "Rx")
}

var ret5 = goo()
print(ret5.code, ret5.msg)

// call by reference
func hoo( num : inout Int)
{
	num = 20
}

var age = 34
hoo(num : &age)		// call by reference, inout argument
print(age)

// default parameter
function foo( msg : String = "Hello" )
{
	print( msg )
}

foo(msg : "asap")
foo()

// functions with variable arguments
func average(num : Double...) -> Double
{
	showType(num)
	
	var total = 0.0
	for n in num
	{
		total = total + n
	}
	var ave = total / Double(num.count)
	return ave
}

var ret = average(num : 1.1, 2.3, 3.12, 5.7)

// function overloading
func foo( a : Int )
{
	print("1")
}

func foo( b : Int )
{
	print("2")
}

func foo( _ b : Int )
{
	print("3")
}

func foo( a : Int, b : Int )
{
	print("4")
}

foo(a:0)
foo(b:0)
foo(1)
foo(a:1, b:2)

// function type
func goo( a : Int, b : Int ) -> Int
{
	return a + b
}
showType(goo)	// (Int, Int) -> Int

var fp : (Int, Int) -> Int		// function Type
fp = goo

var result = fp(12, 14)		//  주의 : 함수 타입 변수로 함수 호출시 인자 이름을 표시하지 않음

// typealais
typealias FP = (Int, Int) -> Int
var f : FP
````

#### closure
````swift
func Sort( _ar : inout Array<Int>, compare : (Int, Int) -> Bool )	// _ ar : [Int]
{
	for i in 0...ar.count - 2
	{
		for j in j + 1...ar.count - 1
		{
			if compare( ar[i], ar[j] )	// 인자로 전달된 비교 정책 함수를 다시 호출
			{
				let temp = ar[i]
				ar[i] = ar[j]
				ar[j] = temp
			}
		}
	}
}

var x = [1, 2, 4, 15, 10, 9, 6, 7, 20]

// compare function
func cmp1( _ a : Int, _ b : Int ) -> Bool
{
	return a < b
}

func cmp2( _ a : Int, _ b : Int ) -> Bool
{
	return a > b
}

print(x)
Sort( &x, compare:cmp1 )
print(x)

// 클로져 (익명의 함수) 사용하기, C++ 람다, Java : 클로져, Objective-C : 블럭
Sort( &x, compare : { (a : Int, b : Int) -> Bool in return a < b } )
Sort( &x, compare : { (a : Int, b : Int) in return a < b } )		// 리턴 타입을 유추가능하므로 클로져에서 리턴타입 생략 가능
Sort( &x, compare : { (a, b in return a < b } ) 					// 컴파일러가 데이터 타입 추론 가능하므로 생략 가능
Sort( &x, compare : { a, b in return a < b } )						// 인자 전달의 ( ) 생략 가능
Sort( &x, compare : { a, b in a < b } )
Sort( &x, compare : { $0 < $1 } )
Sort( &x, compare : < )

// trailing closure
/ 마지막 인자가 함수타입일때는 함수호출() 뒤에 클로져 표현 가능
Sort( &x ){ $0 < $1 }	// 마지막 인자일경우만 가능

// 클로져와 타입
var f = { ( a: Int, b : Int) -> Int in return a + b }
showType(f)		// ((Int, Int)) -> Int
````

#### class
````swift
struct SPoint
{
	var x : Int = 0
	var y : Int = 0
}

class CPoint
{
	var x : Int = 0
	var y : Int = 0
}

var n = 0
var ar = [1,2,3]

var sp1 = SPoint()		// 구조체는 값 스택에 할당.
var sp2 = sp1			// 값 타입의 복사
sp2.x = 10

print(sp2.x)	// 10
print(sp1.x)	// 0

var cp1 = CPoint()	// 클래스는 힙에 할당 : 상속 가능, 소멸자 가능, reflection 으로 동적 타입 검사 가능
var cp2 = cp1		// 참조 타입의 복사
cp2.x = 12

print(cp2.x)	// 12
print(cp1.x)	// 12
````

#### initializer
````swift
// 1. 모든 맴버 data는 반드시 어떤 방식으로든 초기화 되어야 한다. (단, Optional타입은 예외)
// 2. 생성자 이름은 init
// 3. 자신을 담은 포인터(참조) self
class Point
{
	var x : Int
	var y : Int
	
	// designated initializer 지정 초기화
	// 지정 초기화 메소드는 클래스의 원시 초기화 메소드이다. 
	// 이 초기화 과정에서는 해당 클래스의 모든 멤버를 초기화해야 한다. 
	// 따라서 현 클래스에서 새롭게 정의한 모든 멤버의 초기값을 세팅하고, 
	// 다시 부모의 초기화 메소드를 호출하여 상속 받은 모든 멤버들의 초기값을 세팅한다.
	init( x : Int, y : Int ) { self.x = x, self.y = y }
	
	// 생성자에서 다른 생성자 호출 하고 싶으면 편의(convenience)생성자로 만든다.
	convenience init() { self.init( x:0, y:0 ) }
	
	// 소멸자 : deinit.. ()를 표시하지 않는다.
	deinit { print("deinit") }
}

var p1 = Point( x:10, y:20 )
print(p1.x)

var p2 : Point? = Point()
p2 = nil		// p2 call deinit

// 상속과 생성자
class Rect : Point
{
	var width = 0
	var height = 0
	
	init()
	{
		//super.init() // 편의생성자는 호출안됨
		super.init(x:0, y:0)
	}
}

var v = Rect()
````

#### property
````swift
class Point
{
	var x : Int
	var y : Int
	
	init()
	{
		x = 0
		y = 0
		print("Point init")
	}
}

class Rect
{
	// stored property(저장 속성) : 메모리 할당됨.
	var pt1 = Point()
	lazy var pt2 = Point()		// 지연된 속성 lazy property
	
	// calculation property(계산 속성): 메모리 할당이 아닌 연산 수행
	// 사용자는 변수처럼 사용하지만.. 클래스 제작자는 함수 처럼 만드는 문법 - C#등과 유사
	var width : Int {
		get { return pt2.x - pt1.x }
		set { pt2.x = pt1.x + newValue }
	}
	
	// type property (형식 속성) : static맴버 data
	static var count : Int = 0
}

Rect.count = 10		// 형식 속성 사용. 클래스이름.속성

var r1 = Rect()
print("aa")

r1.pt2.x = 10	// 처음 사용.. 이 순간 pt2가 생성된다.

print(r1.width)
r1.width = 30
print(r1.width)
````

#### subscript
````swift
class Vector
{
	var buffer : Array<Int> = [1,2,3,4]		// empty 배열 초기화
	
	// subscript : 객체를 배열처럼 사용하게 하는 문법 [] 연산자 재정의 기술
	subscript(idx, Int) -> Int {
		get { return buffer[idx] }
		set { buffer[idx] = newValue }
	}
	
	subscript(idx : String) -> String {
		get { return "aa" }
	}
	
	subscript(idx1 : Int, idx2 : Int) -> (Int, Int) {
		get { return (buffer[idx1], buffer[idx2]) }
	}
}

var v = Vector()
v[0] = 100
print( v[0] )		// []연산자 재정의, C# : indexer

print( v["one"] )
print( v[1,2] )
````

#### method
````swift
class People
{
	var name = ""
	var age = 0
	
	func set( _ name : String, _ age : Int = 10)
	{
		self.name = name
		self.age = age
		
		print("People set")
	}
}

class Student : People
{
	// 부모함수를 재정의 할떄는 반드시 override 필요
	override func set( _ name : String, _ age : Int = 20 )
	{
		self.name = name
		self.age = age
		
		print("Student set")
	}
	
	static func foo() {}
}

var p : People = Student()
//p.set("aa", 20)	// 부모 타입의 참조로 함수 호출

p.set("AAA")	// p.set("AAA", 10) 10은 people 디폴트 인자
print(p.age)

// 디폴트 인자는 컴파일 시간에 채워 지지만 어느 함수를 호출 할지는 실행시간에 결정한다.
````

#### extension
````swift
class Car
{
	func go() { print("Car go") }
	init()		{ print("Car init") }
}

var c = Car()
c.go()

// 기존 클래스에 새로운 메소드 추가하기. objective-c 에서 category
extension Car
{
	func stop() { print("Car stop") }
	
	//var speed : Int		// error. stored property 추가 안됨
	var speed : Int { get { return 0 } }	// calculation property 가능
	
	subscript ( idx : Int ) -> Int { get { return 0 } }	// ok
	
	/ 편의 생성자 추가 가능. 일반 생성자 안됨
    // deinit 추가 안됨
}

c.stop()

// String extension.

var s = "ABCDEFG"

// string subscript 함수가 인자가 Int가 아니다
print(s[s.startIndex])
print(s[s.index(s.startIndex, offsetBy: 2)])

extension String
{
    subscript (idx : Int) -> Character {
        get {
            return self[ self.index(self.startIndex, offsetBy: idx) ]
        }
    }
}

print(s[1])
````
