##Day3

#### casting
```` swift
class Animal {}
class Dog : Animal {}
class Cat : Animal
{
	func Cry() { print "Cat cry") }
}

// 1. 부모 참조에 자식을 담을 수 있다.
var p1 : Cat = Cat()
var p2 : Animal = Cat()

// 2. 부모 참조가 누구를 가리키는지 조사하기
print( p2 is Cat )
print( p2 is Dog }
print( p2 is Animal }

// 3. 실제 객체 타입으로 캐스팅하기
//p2.Cry()	// error. p2가 Cat을 가르키지만 타입은 Animal
var p3 = p2 as! Cat
//var p3 = p2 as! Dog	// 잘못된 캐스팅 발생시 예외 전달
var p3 = p2 as? Dog		// Optional 타입 리턴.. 실패시 nil
showType(p3)
if p3 == nil
{
	print ("p3 is not Dog")
}
//p3.Cry()
````
