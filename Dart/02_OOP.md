# 객체 지향 프로그래밍

## 클래스

`객체(object)`는 저장 공간에 할당되어 값을 가지거나 식별자에 의해 참조되는 공간을 말한다. 변수, 자료 구조, 함수 또는 메소드 등이 객체가 될 수 있다. 
이러한 객체를 메모리에 작성하는 것을 '인스턴스(instance)화' 한다고 하며 메모리에 작성된 객체를 인스턴스라고 한다.  
인스턴스화하기 위해서는 설계도가 필요한데 설계도 역할을 하는 것이 클래스(class)이다. 클래스 안에는 속성을 표현할 수 있는데 이를 프로퍼티(property) 라고 한다.

- 클래스는 가장 최상위 부모인 Object class를 상속받고 있다. => 객체지향 프로그래밍

```dart
void main() {
 Idol blackPink = Idol('블랙핑크', ['지수', '제니', '리사', '로제']); // 다트에서는 new 키워드 생략 가능

print(blackPink.name);
print(blackPink.members);
blackPink.sayHello(); // 함수실행
blackPink.introduce();  
}

class Idol{
  String name;
  List<String> members;

  Idol(this.name, this.members);
  
  void sayHello(){
    print ('안녕하세요 ${this.name}입니다');
  }
  
  void introduce(){
    print('저희 멤버는 ${this.members}가 있습니다.');
  }
}
```

- immutable 프로그래밍을 위해 constructor 앞에 final, const 키워드를 붙이기도 함.
    - 서로 다른 변수에 클래스를 const로 선언하고, 같은 parameter를 전달한 경우, 해당 인스턴스들은 같다고 본다. 


### getter, setter
- getter : 데이터를 가져올 때
- setter : 데이터를 설정할 때

```dart
void main() {
 Idol blackPink = Idol('블랙핑크', ['지수', '제니', '리사', '로제']);
  
  blackPink.firstMember = '제니';
  print(blackPink.firstMember);
}

class Idol{
  String name;
  List<String> members;

  Idol(this.name, this.members);
  
  Idol.fromList(List values)
    : this.members = values[0],
      this.name = values[1];
  
  void sayHello(){
    print ('안녕하세요 ${this.name}입니다');
  }
  
  void introduce(){
    print('저희 멤버는 ${this.members}가 있습니다.');
  }
  
  // getter
  String get firstMember {
    return this.members[0];
  }
  
  // setter
  set firstMember (String name) {
    this.members[0] = name;
  }
}
```
- setter function에는 매개변수 하나만!
    - List 매개변수가 final로 선언되어도 리스트 내부는 변경 가능
- getter function -> 간단한 데이터 가공에서 사용


### private class
- 클래스 앞에 `_`를 붙여준다.
- 같은 파일 내에서만 쓸 수 있고, 다른 파일에서는 불러올 수 없다.

### inheritance
- 상속을 받으면 부모 클래스의 모든 속성을 자식 클래스가 부여받는다.
- 자식클래스의 속성들은 부모 클래스로 넘어가지 않는다.
- 같은 자식 클래스끼리도 속성들을 공유하지 않는다.
- 타입 비교를 했을 때 자식 클래스의 경우 부모 클래스와 자식 클래스의 타입 둘 다 가진다.

```dart
class Idol {
  String name;
  int membersCount;

  Idol({
    required this.name,
    required this.membersCount,
  });

  void sayName() {
    print('저는 ${this.name}입니다.');
  }

  void sayMembersCount() {
    print('${this.name}은 ${this.membersCount}명의 멤버가 있습니다.');
  }
}

class BoyGroup extends Idol {
  BoyGroup(String name, int membersCount)
      : super(name: name, membersCount: membersCount);
  
  void sayMale () {
    print('우리는 남자아이돌입니다.');
  }
}
```

### method overriding
- `@override` 키워드를 사용하여 부모 클래스의 속성 덮어쓸 수 있음

```dart
void main() {
  TimesTwo tt = TimesTwo(2);
  TimesFour tf = TimesFour(2);
  
  print(tt.calculate());
  print(tf.calculate());
}

class TimesTwo {
  final int number;

  TimesTwo(this.number);

  int calculate() {
    return number * 2;
  }
}

class TimesFour extends TimesTwo {
  TimesFour(int number) : super(number);

  @override
  int calculate() {
    return super.calculate() * 2;
  }
}
```

### static keyword
- static은 instance에 귀속되지 않고 class에 귀속된다.

```dart
void main() {
  Employee seulgi = Employee('슬기');
  Employee chorong = Employee('초롱');
  
  seulgi.name = '선주';
  seulgi.printNameAndBuilding();
  chorong.printNameAndBuilding();
  
  Employee.building = '타워';

  seulgi.printNameAndBuilding();
  chorong.printNameAndBuilding();
  
  Employee.printBuilding();
}


class Employee {
  static String? building;
  String name;
  
  Employee(
  this.name,
  );
  
  void printNameAndBuilding(){
    print('제 이름은 $name입니다. $building 건물에서 근무하고 있습니다.');
  }
  
  static void printBuilding(){
    print('저는 $building에서 근무 중입니다.');
  }
  
}
```

### interface
- class 클래스명 implements 인터페이스명 형식으로 사용
- 인터페이스는 클래스의 구조를 강제한다.
- 인터페이스를 인스턴스화하지 못하도록 class 키워드 앞에 abstract 키워드를 붙일 수 있다.
    - abstract 키워드를 사용할 경우 인터페이스 내 함수 body 작성하지 않아도 됨
```dart
void main() {
  BoyGroup bts = BoyGroup('BTS');
  
  bts.sayName();
  print(bts is IdolInterface); // true
  print(bts is BoyGroup); // true
}

abstract class IdolInterface {
  String name;

  IdolInterface(this.name);

  void sayName() {}
}

class BoyGroup implements IdolInterface {
  String name;
  BoyGroup(this.name);

  void sayName() {
    print('제 이름은 ${this.name}입니다.');
  }
}
```

### generic
- generic : 타입을 외부에서 받을 때 사용
- 제너릭은 여러 개 받을 수 있음

```dart
void main() {
  Lecture<String> lecture1 = Lecture('1', 'lecture1');
  
  lecture1.printIdType();
  
  Lecture<int> lecture2 = Lecture(2, 'lecture2');
  
  lecture2.printIdType();
}

class Lecture<T> {
  final T id;
  final String name;
  
  Lecture(this.id, this.name);
  
  void printIdType(){
    print(id.runtimeType);
  }
}
```