# oop

- https://dartpad.dev/
- https://www.inflearn.com/course/dart-%EC%96%B8%EC%96%B4-%EC%9E%85%EB%AC%B8/unit/107631

## class

### constructor

```dart
void main() {
  Idol blackPink = new Idol('블랙핑크', ['지수', '제니', '리사', '로제']);
  Idol bts = new Idol('BTS', ['RM', '진', '슈가', '제이홉', '지민', '뷔', '정국']);
}

class Idol {
  String name;
  List<String> members;

  // 생성자
  Idol(String name, List<String> members)
    : this.name = name,
      this.members = members;


  void sayHello() {
    print(this.name);
  }

  void introduce() {
    print(this.members);
  }
}
```

### constructor - short cut

```dart
void main() {
  Idol blackPink = new Idol('블랙핑크', ['지수', '제니', '리사', '로제']);
  Idol bts = new Idol('BTS', ['RM', '진', '슈가', '제이홉', '지민', '뷔', '정국']);
}

class Idol {
  String name;
  List<String> members;

  // 생성자 - short cut
  Idol(this.name, this.members);

  void sayHello() {
    print(this.name);
  }

  void introduce() {
    print(this.members);
  }
}
```

### constructor - named constructor

```dart
void main() {
  Idol blackPink = new Idol('블랙핑크', ['지수', '제니', '리사', '로제']);
  Idol bts = new Idol.fromList([
    ['RM', '진', '슈가', '제이홉', '지민', '뷔', '정국'],
    'BTS',
  ]);
}

class Idol {
  String name;
  List<String> members;

  // 생성자 - named constructor
  Idol(this.name, this.members);

  // 스태틱 메서드
  Idol.fromList(List values)
    : this.members = values[0],
      this.name= values[1];
}
```

### constructor - other

```dart
void main() {
  Idol blackPink = new Idol('블랙핑크', ['지수', '제니', '리사', '로제']);
}

class Idol {
  String name = '';
  List<String> members = [];

  // 생성자
  Idol(String name, List<String> members) {
    this.name = name;
    this.members = members;
  }
}
```

## immutable programming

### final class member

- 대부분의 클래스 변수를 final로 선언하는 습관 필요

```dart
void main() {
  Idol blackPink = new Idol('블랙핑크', ['지수', '제니', '리사', '로제']);
  Idol bts = new Idol('BTS', ['RM', '진', '슈가', '제이홉', '지민', '뷔', '정국']);

  blackPink.name = 'a';
}

class Idol {
  // 상수 설정
  final String name = '';
  final List<String> members = [];

  // 생성자
  Idol(String name, List<String> members) {
    this.name = name;
    this.members = members;
  }


  void sayHello() {
    print(this.name);
  }

  void introduce() {
    print(this.members);
  }
}
```

### const instance

- const instance를 만드는 경우 맴버가 동일한 경우 인스턴스 비교시 동일한것으로 판단 됨

```dart
void main() {
  Idol blackPink = const Idol('블랙핑크', ['지수', '제니', '리사', '로제']);
  Idol blackPink2 = const Idol('블랙핑크', ['지수', '제니', '리사', '로제']);

  print(blackPink == blackPink2); // true

}

class Idol {
  final String name;
  final List<String> members;

  const Idol(this.name, this.members);
}
```

### getter/setter

- 메서드가 아닌 getter 를 사용하는 이유
  - getter : 데이터를 간단하게 가공하는 경우 사용
  - 메서드 : 로직이 많이 추가되는 경우 사용

```dart
void main() {
  Idol blackPink = Idol('블랙핑크', ['지수', '제니', '리사', '로제']);

  // getter
  print(blackPink.firstMember); // '지수'

  // setter
  blackPink.firstMember = '에이미';
  print(blackPink.firstMember); // '에이미'

}

class Idol {
  String name;
  List<String> members;

  Idol(this.name, this.members);

  // getter
  String get firstMember {
    return this.members[0];
  }

  // setter - 하나의 값만 인자로 전달 가능
  set firstMember(String name) {
    this.members[0] = name;
  }
}
```

### private member

- 파일 외부에서 사용할 수 없음
- 이름 앞에 `_` 를 붙인다.
  - class, member, method 모두 가능

```dart
void main() {
  _Idol blackPink = _Idol('블랙핑크', ['지수', '제니', '리사', '로제']);

  // getter
  print(blackPink._firstMember); // '지수'

  // setter
  blackPink._firstMember = '에이미';
  print(blackPink._firstMember); // '에이미'

}

// private 맴버
class _Idol {
  // private member
  String _name;
  // private member
  List<String> _members;

  _Idol(this._name, this._members);

  // private method
  List<String> _getMembers() {
    return this._members;
  }

  // private getter
  String get _firstMember {
    return this._members[0];
  }

  // private setter
  set _firstMember(String name) {
    this._members[0] = name;
  }
}
```

## 상속

```dart
void main() {
  print('----------- Idol ------------');
  Idol apink = Idol(name: '에이핑크', membersCount: 5);

  apink.sayName();
  apink.sayMembersCount();

  print('----------- Boy Group ------------');
  BoyGroup bts = BoyGroup('BTS', 7);
  bts.sayName();
  bts.sayMembersCount();
  bts.sayMale();

  print('----------- Girl Group ------------');
  BoyGroup redVelvet = GirlGroup('레드벨벳', 7);
  redVelvet.sayName();
  redVelvet.sayMembersCount();
  redVelvet.sayFemale();

  print('----------- Type Comparison ------------');
  print(apink is Idol); // true
  print(bts is BoyGroup); // true
  print(redVelvet is GirlGroup); // true
  print(bts is Idol); // true
}

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
  BoyGroup(
    String name,
    int membersCount,
  ) : super(
    name: name,
    membersCount: membersCount,
  );

  void sayMale() {
    print('저는 남자 아이돌 입니다.');
  }
}

class GirlGroup extends Idol {
  GirlGroup(
    String name,
    int membersCount,
  ) : super(
    name: name,
    membersCount: membersCount,
  );

  void sayFemale() {
    print('저는 여자 아이돌 입니다.');
  }
}
```

## Method Override

- 부모 클래스의 메서드와 동일한 signature로 선언한경우 부모 클래스의 메서드를 덮어 씌울 수 있다.
- @override 어노테이션을 사용하지 않아도 동일함(사용 하는것을 추천)

```dart
void main() {
  TimesTwo tt = TimesTwo(2);

  print(tt.calculate()); // 4

  TimesFour tf = TimesFour(2);

  print(tf.calculate()); // 8
}

class TimesTwo {
  final int number;

  TimesTwo(this.number);

  int calculate() {
    return this.number * 2;
  }
}

class TimesFour extends TimesTwo {
  TimesFour(
    int number,
  ): super(number);


  @override
  int calculate() {
    // 아래 모두 허용
    // return super.number * 4;
    // return this.number * 4;
    // return number * 4;

    return super.calculate() * 2;
  }
}
```

## Static Keyword

- static은 인스턴스에 귀속되지 않고 클래스에 귀속된다.

```dart
void main() {
  Employee seulgi = new Employee('슬기');
  Employee chorong = new Employee('초롱');

  seulgi.printNameAndBuilding();  // 제 이름은 슬기입니다. null 건물에서 근무하고 있습니다.
  chorong.printNameAndBuilding(); // 제 이름은 초롱입니다. null 건물에서 근무하고 있습니다.

  Employee.building = '오투';

  seulgi.printNameAndBuilding();  // 제 이름은 슬기입니다. 오투 건물에서 근무하고 있습니다.
  chorong.printNameAndBuilding(); // 제 이름은 초롱입니다. 오투 건물에서 근무하고 있습니다.

  Employee.printBuilding(); // 저는 오투 건물에서 근무합니다.
}

class Employee {
  static String? building;
  final String name;

  Employee(
    this.name,
  );

  void printNameAndBuilding() {
    print('제 이름은 ${name}입니다. ${building} 건물에서 근무하고 있습니다.');

  }

  static void printBuilding() {
    print('저는 ${building} 건물에서 근무합니다.');
  }
}
```

## Interface

- 특수한 구조를 강제

```dart
void main() {
  BoyGroup bts = new BoyGroup('BTS');
  GirlGroup redVelvet = new GirlGroup('레드벨벳');

  bts.sayName();  // 제 이름은 BTS입니다
  redVelvet.sayName();  // 제 이름은 레드벨벳입니다
}

class IdolInterface {
  String name;

  IdolInterface(this.name);

  void sayName() {}
}

class BoyGroup implements IdolInterface {
  String name;

  BoyGroup(this.name);

  void sayName(){
    print('제 이름은 ${name}입니다');
  }
}

class GirlGroup implements IdolInterface {
  String name;

  GirlGroup(this.name);

  void sayName(){
    print('제 이름은 ${name}입니다');
  }
}
```

```dart
void main() {
  BoyGroup bts = new BoyGroup('BTS');
  GirlGroup redVelvet = new GirlGroup('레드벨벳');

  bts.sayName();  // 제 이름은 BTS입니다
  redVelvet.sayName();  // 제 이름은 레드벨벳입니다
}

// 추상 클래스, 함수 몸체 불필요
abstract class IdolInterface {
  String name;

  void sayName() {}
}

class BoyGroup implements IdolInterface {
  String name;

  BoyGroup(this.name);

  void sayName(){
    print('제 이름은 ${name}입니다');
  }
}

class GirlGroup implements IdolInterface {
  String name;

  GirlGroup(this.name);

  void sayName(){
    print('제 이름은 ${name}입니다');
  }
}
```

## Generic

- 타입을 외부에서 받을 때 사용

```dart
void main() {
  Lecture<String> lecture1 = Lecture('123', 'lecture1');
  lecture1.printIdType(); // String

  Lecture<int> lecture2 = Lecture(123, 'lecture1');
  lecture2.printIdType(); // int
}

class Lecture<T> {
  final T id;
  final String name;

  Lecture(this.id, this.name);

  void printIdType() {
    print(id.runtimeType);
  }
}
```
