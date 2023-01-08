# 기본기

- https://dartpad.dev/
- https://www.inflearn.com/course/dart-%EC%96%B8%EC%96%B4-%EC%9E%85%EB%AC%B8/unit/107600

## 출력 - print()

```dart
void main() {
  print('hello code factory');
}
```

## 변수

### 변수 선언

```dart
void main() {
  // variable
  var name = '코드팩토리';

  print(name); // '코드 팩토리'
}
```

### 값 변경

```dart
void main() {
  var name = '코드팩토리';

  print(name); // '코드 팩토리'

  name = '플러터 프로그래밍';

  print(name); // '플러터 프로그래밍'
}
```

### 같은 변수 재정의

```dart
void main() {
  var name = '코드팩토리';
  // Error - 같은 스코프 내에서 같은 변수 선언 불가
  var name = '플러터 프로그래밍';
}
```

## 정수 - int

```dart
void main() {
  // 정수 타입 변수 선언
  var number = 10;

  print(number); // 10

  // 계산
  var number1 = 2;
  var number2 = 4;

  print(number1 + number2); // 6
  print(number1 - number2); // -2
  print(number1 / number2); // 0.5
  print(number1 * number2); // 8
}
```

## 실수 - double

```dart
void main() {
  // 실수 타입 변수 선언
  double number = 2.5;

  print(number); // 2.5

  // 계산
  var number1 = 2.5;
  var number2 = 0.5;

  print(number1 + number2); // 3
  print(number1 - number2); // 2
  print(number1 / number2); // 5
  print(number1 * number2); // 1.25
}
```

## 불리언 - bool

```dart
void main() {
  // 불리언 타입 변수 선언
  bool isTrue = true;
  bool isFalse = false;

  print(isTrue); // true
  print(isFalse); // false
}
```

## 문자열 - string

```dart
void main() {
  // 문자열 타입 변수 선언
  String name = '레드밸벳';
  String name2 = '코드팩토리';

  print(name);  // 레드밸벳
  print(name2); // 코드팩토리

  // 빈 공백 문자 추가
  print(name + ' ' + name2); // '레드밸벳 코드팩토리'

  // $ 활용 1
  print('${name} {name2}'); // '레드밸벳 코드팩토리'
  print('${name.runtimeType} {name2}'); // 'String 코드팩토리'

  // $ 활용 2 - 객체의 프로퍼티 접근을 사용하는 경우 ${}로 감싸주어야 코드로 인식됨
  print('$name $name2'); // '레드밸벳 코드팩토리'
  print('$name.runtimeType $name2'); // '레드밸벳.runtimeType 코드팩토리'
}
```

## 추론 - var

- var 타입은 존재하지 않는다.
- 실행 시점에 우변의 타입값으로 지정 된다.

```dart
void main() {
  var name = '코드팩토리';
  var number = 1;
  var number2 = 0.5;
  var boolean = true;

  // 실행 시점에 지정되는 타입 확인
  print(name.runtimeType); // String
  print(number.runtimeType); // int
  print(number2.runtimeType); // double
  print(boolean.runtimeType); // int
}
```

> - var 타입만 사용하는 경우?
>   - 어쩔수 없는경우
>   - 복잡한 타입을 매번 지정하는 경우(?)

## 동적 타입 - dynamic

- 어떤 타입이든 변수에 할당 가능
- var, dynamic 차이
  - dynamic
    - 재 할당 시 타입이 변경됨
  - var 타입
    - 초기화 시점에 타입이 지정됨

```dart
void main() {
  dynamic val = '코드팩토리';
  print(val.runtimeType); // String

  val = 1;
  print(val.runtimeType); // int

  val = 0.5;
  print(val.runtimeType); // double

  val = true;
  print(val.runtimeType); // bool
}
```

## nullable - ?

- 모든 타입은 2가지로 나뉜다.
  - non-nullable
    - 특정 타입만 허용
  - nullable
    - 특정 타입 or null 허용

```dart
void main() {
  String name = '코드팩토리';

  name = null; // Error: The value 'null' can't be assigned to a variable of type 'String' because 'String' is not nullable.

  String? name2 = '블랙핑크';
  name2 = null;
  print(name2); // null
}
```

## null 유형 변경 - !

- 어떤 함수 실행시 null 타입이 절대 아니라는 것을 알려 준다.

```dart
void main() {
  String? name2 = '블랙핑크';

  // null이 아님을 알려준다.
  print(name2!); // 블랙핑크
}
```

## 상수 선언 - final, const

- 변수 선언시 코드 맨 앞에 사용
- 변수의 값을 선언 후 다른 값으로 변경 불가
- final, const 사용시 타입 선언을 생략 할 수 있다.
  - var의 기능 제공
- final vs const
  - const
    - 빌드 타임에 값을 알고 있어야 한다.
    - 예) const DateTime now = DateTime.now(); // 사용 불가
  - final
    - 빌드 타임에 값을 몰라도 된다.
- 빌드 타임
  - 작성된 코드 결과물은 바이트 코드로 변환된다.
  - 사람이 이해할 수 있는 코드 작성후 코드 실행시 빌드 과정이 일어나게된다.
  - 빌드 과정에서 컴퓨터가 이해할 수 있는 바이트 코드로 변환된다.
  - 이 빌드가 실행되는 시점을 빌드 타임이라 한다.
- 작성 하는 순간 코드의 값을 알고 있어야 한다.
  - DateTime.now() 는 코드가 실행되는 시점의 시간을 반환한다.
  - const는 빌드 타입에 이미 값을알고 있어야 하므로 DateTime.now()의 값을 const에 담을 수 없다.

```dart
void main() {
  final String name = '코드팩토리';

  print(name);; // '코드팩토리'

  name = '블랙핑크'; // Error: Can't assign to the final variable 'name'.

  const String name2 = '블랙핑크';
  print(name2); // '블랙핑크'

  // final, const 사용시 타입 선언을 생략 할 수 있다.
  final name3 = '코드팩토리';
  const name4 = '블랙핑크';

  print(name3); // '코드팩토리'
  print(name4); // '블랙핑크'
}
```

## operator

- 변수 선언시 코드 맨 앞에 사용
- 변수의 값을 선언 후 다른 값으로 변경 불가

### %, ++, --, +=, -=, \*=, -= operator

```dart
void main() {
  int number = 2;

  print(number % 2); // 0
  print(number % 3); // 2

  print('--------'); // '--------'

  number++;
  print(number); // 3

  number--;
  print(number); // 2

  print('--------'); // '--------'

  double number2 = 4.0;
  print(number2); // 4

  number2 += 1;
  print(number2); // 5

  number2 -= 1;
  print(number2); // 4

  number2 *= 2;
  print(number2); // 8

  number2 /= 2;
  print(number2); // 4
}
```

### nullable operator

```dart
void main() {
  double? number = 4.0;
  print(number); // 4

  number = 2.0;
  print(number); // 2

  number = null;
  print(number); // null

  // number가 null인 경우 오른쪽 값으로 할당
  number ??= 3.0;

  print(number); // 3

  number ??= 5.0;

  print(number); // 3
}
```

### 비교 operator

```dart
void main() {
  int number1 = 1;
  int number2 = 2;

  print(number1 > number2); // false
  print(number1 < number2); // true
  print(number1 >= number2); // false
  print(number1 <= number2); // true
  print(number1 == number2); // false
  print(number1 != number2); // true
}
```

### 타입 비교 operator

```dart
void main() {
  int number1 = 1;

  print(number1 is int); // true
  print(number1 is String); // false

  print(number1 is! int); // false
  print(number1 is! String); // true
}
```

### and(&&), or(||) operator

```dart
void main() {
  // and
  bool result = 12 > 10 && 1 > 0;
  print(result); // true

  bool result2 = 12 > 10 && 1 < 0;
  print(result2); // false

  // or
  bool result3 = 12 > 10 || 1 > 0;
  print(result3); // true

  bool result4 = 12 > 10 || 1 < 0;
  print(result4); // true

  bool result4 = 12 < 10 || 1 < 0;
  print(result4); // false

  bool result5 = 12 < 10 || 1 > 0;
  print(result5); // true
}
```

## list

```dart
void main() {
  List<String> blackPink = ['제니', '지수', '로제', '리사'];
  List<number> numbers = [1, 2, 3, 4];
  List<number> numbers = [1, 2, 3, 4, 'test']; // Error: A value of type 'String' can't be assigned to a variable of type 'int'.

  // n번째 값 가져오기

  print(blackPink[0])
}
```

### n번째 값 가져오기

```dart
void main() {
  List<String> blackPink = ['제니', '지수', '로제', '리사'];
  print(blackPink[0]); // 제니

  // 범위를 초과하는 값 참조
  print(blackPink[4]); // Uncaught Error: RangeError (index): Index out of range: index should be less than 4: 4
}
```

### 길이 가져오기 .length

```dart
void main() {
  List<String> blackPink = ['제니', '지수', '로제', '리사'];
  print(blackPink.length); // 4;
}
```

### 값 추가 .add()

```dart
void main() {
  List<String> blackPink = ['제니', '지수', '로제', '리사'];
  // 값 추가
  blackPink.add('555');

  print(blackPink); // ['제니', '지수', '로제', '리사', '555'];
}
```

### 값 제거 .remove()

```dart
void main() {
  List<String> blackPink = ['제니', '지수', '로제', '리사'];
  // 값 제거
  blackPink.remove('리사');

  print(blackPink); // ['제니', '지수', '로제'];
}
```

### index 가져오기 .indexOf()

```dart
void main() {
  List<String> blackPink = ['제니', '지수', '로제', '리사'];
  // 인덱스 알아오기
  print(blackPink.indexOf('리사')); // 3
}
```

## map

- 키/벨류로 이루어짐

```dart
void main() {
  Map<String, String> dictionary = {
    'Harry Potter': '해리포터',
    'Ron Weasley': '론 위즐리',
    'Hermione Granger': '헤르미온 그레이저'
  };

  print(dictionary); // {Harry Potter: 해리포터, Ron Weasley: 론 위즐리, Hermione Granger: 헤르미온 그레이저}

}
```

### 값 단일 추가

```dart
void main() {
  Map<String, String> dictionary = {
    'Harry Potter': '해리포터',
    'Ron Weasley': '론 위즐리',
    'Hermione Granger': '헤르미온 그레이저'
  };

  dictionary['Spiderman'] = 'james';
  print(dictionary); // {Harry Potter: 해리포터, Ron Weasley: 론 위즐리, Hermione Granger: 헤르미온 그레이저, Spiderman: james}
}
```

### 값 여러값 추가 .addAll()

```dart
void main() {
  Map<String, String> dictionary = {
    'Harry Potter': '해리포터',
    'Ron Weasley': '론 위즐리',
    'Hermione Granger': '헤르미온 그레이저'
  };

  dictionary.addAll({
    'Spiderman': 'james',
    'iron': 'tommy'
  });
  print(dictionary); // {Harry Potter: 해리포터, Ron Weasley: 론 위즐리, Hermione Granger: 헤르미온 그레이저, Spiderman: james, iron: tommy}

}
```

### 값 가져오기

```dart
void main() {
  Map<String, String> dictionary = {
    'Harry Potter': '해리포터',
    'Ron Weasley': '론 위즐리',
    'Hermione Granger': '헤르미온 그레이저'
  };

  print(dictionary['Hermione Granger']); // '헤르미온 그레이저'

  // 없는 키로 가져오기
  print(dictionary['Hermione Granger22']); // null
}
```

### 값 제거 - remove();

```dart
void main() {
  Map<String, String> dictionary = {
    'Harry Potter': '해리포터',
    'Ron Weasley': '론 위즐리',
    'Hermione Granger': '헤르미온 그레이저'
  };

  dictionary.remove('Harry Potter');
}
```

### 키/값 가져오기 - keys, values

```dart
void main() {
  Map<String, String> dictionary = {
    'Harry Potter': '해리포터',
    'Ron Weasley': '론 위즐리',
    'Hermione Granger': '헤르미온 그레이저'
  };

  print(dictionary.key); // (Harry Potter, Ron Weasley, Hermione Granger)
  print(dictionary.values); // (해리포터, 론 위즐리, 헤르미온 그레이저)
}
```

## set

- 중복값 없이 리스트로 저장

```dart
void main() {
  Set<String> names = {
    'flutter',
    'black pink',
    'flutter',
  };

  print(names); // {flutter, black pink}

}
```

### 값 추가 - add();

```dart
void main() {
  Set<String> names = {
    'flutter',
    'black pink'
  };

  names.add('other');
  print(names); // {flutter, black pink, other}

}
```

### 값 삭제 - remove();

```dart
void main() {
  Set<String> names = {
    'flutter',
    'black pink',
    'other'
  };

  names.remove('other');
}
```

### 값 존재 확인 - contains();

```dart
void main() {
  Set<String> names = {
    'flutter',
    'black pink',
    'other'
  };

  names.contains('other'); // true
}
```

## if/else 문

```dart
void main() {
  int number = 2;
  if(number % 2 == 0) {
    print('짝수');
  } else {
    print('홀수');
  }

  number = 3;
  if(number % 3 == 0) {
    print('나머지 0');
  } else if(number % 3 == 1) {
    print('나머지 1');
  } else {
    print('나머지 2');
  }
}
```

## switch 문

```dart
void main() {
  int number = 3;

  switch(number % 3) {
    case 0:
      print('나머지 0');
      break;
    case 1:
      print('나머지 1');
      break;
    default:
      print('나머지 2');
      break;
  }
}
```

## loop

### for loop

```dart
void main() {
  // for loop
  for(int i = 0; i < 10; i++) {
    print(i);
  }

  List<int> numbers = [1,2,3,4,5,6];

  // for
  int total = 0;
  for(int i = 0; i < numbers.length; i++) {
    total += numbers[i];
  }

  print(total); // 21

  // for .. in
  int total2 = 0;
  for(int number in numbers) {
    total2 += number;
  }

  print(total2); // 21


  // continue
  int total2 = 0;
  for(int number in numbers) {
    if(number == 5) {
      continue;
    }
    total2 += number;
  }

  print(total2); // 16

}
```

### while loop

```dart
void main() {
  int total = 0;

  while(total < 10) {
    total += 1;
  }

  print(total); // 10;

  // break;
  total = 0;

  while(total < 10) {
    total += 1;
    if(total == 5) {
      break;
    }
  }

  print(total); // 5;
}
```

### do while loop

```dart
void main() {
  int total = 0;

  do {
    total += 1;
  }
  while(total < 10);

  print(total); // 10;
}
```

## enum

```dart
enum Status {
  approved, // 승인
  pending, // 대기
  rejected, // 거절
}

void main() {
  Status status = Status.pending;

  if(status == Status.approved) {
    print('승인');
  } else if(status == Status.pending) {
    print('대기');
  } else {
    print('거절');
  }
}
```

## 함수 선언

```dart
void main() {
  String result = addNumbers(1, 2, 3);
  print(result); // '짝수'
}

// 3 개의 숫자(x, y, z)를 더하고 짝수 홀수인지 반환
String addNumbers(int x, int y, int z) {
  int sum = x + y + z;

  return sum % 2 == 0 ? '짝수' : '홀수';
}
```

### optional 파라미터

```dart
void main() {
  String result = addNumbers(1);
  print(result);
}

String addNumbers(int x, [int y  = 20, int z = 30]) {
  int sum = x + y + z;

  return sum % 2 == 0 ? '짝수' : '홀수';
}
```

### named 파라미터

```dart
void main() {
  // 명시적으로 인자를 전달 해야 함.
  String result = addNumbers(x: 10, y: 20, z: 30);
  print(result);
}

// 인자 받는 형식이 다름
String addNumbers({
  required int x,
  required int y,
  required int z
}) {
  int sum = x + y + z;

  print('x : ${x}');
  print('y : ${y}');
  print('z : ${z}');

  return sum % 2 == 0 ? '짝수' : '홀수';
}
```

### named 파라미터 + optional

```dart
void main() {
  // 명시적으로 인자를 전달 해야 함.
  String result = addNumbers(x: 10, y: 20);
  print(result);
}

// 인자 받는 형식이 다름
String addNumbers({
  required int x,
  required int y,
  // optional
  int z = 40
}) {
  int sum = x + y + z;

  print('x : ${x}');
  print('y : ${y}');
  print('z : ${z}');

  return sum % 2 == 0 ? '짝수' : '홀수';
}
```

## void

- 아무것도 없음을 나타냄

## arrow function

```dart
void main() {
  int result = addNumbers(x: 10, y: 20);
  print(result); // 70
}

int addNumbers({
  required int x,
  required int y,
  // optional
  int z = 40
}) => x + y+ z;
```

## typedef

- 함수를 변수에 담기 위한 목적

```dart
void main() {
  Operation operation = add;
  Operation operation2 = subtract;

  int result = operation(10, 20, 30);

  print(result); // 60
  print(result2); // -40
}

// signature
typedef Operation = int Function(int x, int y, int z);

// 더하기
int add(int x, int y, int z) => x + y + z;
// 빼기
int subtract(int x, int y, int z) => x - y - z;
```

```dart
// 응용
void main() {

  int result = calculate(10, 20, 30, add);
  int result2 = calculate(10, 20, 30, subtract);

  print(result); // 60
  print(result2); // -40
}

// signature
typedef Operation = int Function(int x, int y, int z);

// 더하기
int add(int x, int y, int z) => x + y + z;
// 빼기
int subtract(int x, int y, int z) => x - y - z;
// 계산기
int calculate(int x, int y, int z, Operation operation) {
  return operation(x, y, z);
}
```
