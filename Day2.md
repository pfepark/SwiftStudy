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
````
