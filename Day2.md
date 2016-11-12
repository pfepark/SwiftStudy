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
