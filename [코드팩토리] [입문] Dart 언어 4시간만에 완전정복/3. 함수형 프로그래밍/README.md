# 함수형 프로그래밍

- https://dartpad.dev/
- https://www.inflearn.com/course/dart-%EC%96%B8%EC%96%B4-%EC%9E%85%EB%AC%B8/unit/107631

## list -> map/set 변환

```dart
void main() {
  List<String> blackPink = ['로제', '지수', '리사', '제니', '제니'];

  print(blackPink); // [로제, 지수, 리사, 제니, 제니]
  print(blackPink.asMap()); // {0: 로제, 1: 지수, 2: 리사, 3: 제니, 4: 제니}
  print(blackPink.toSet()); // {로제, 지수, 리사, 제니}
}
```

## map iterable

```dart
void main() {
  List<String> blackPink = ['로제', '지수', '리사', '제니', '제니'];

  print(blackPink);                       // [로제, 지수, 리사, 제니, 제니]
  print(blackPink.asMap());               // {0: 로제, 1: 지수, 2: 리사, 3: 제니, 4: 제니}
  print(blackPink.toList());              // [로제, 지수, 리사, 제니, 제니]


  Map blackPinkMap = blackPink.asMap();

  print(blackPinkMap.keys);               // (0, 1, 2, 3, 4)
  print(blackPinkMap.keys.toList());      // [0, 1, 2, 3, 4]

  print(blackPinkMap.values);             // (로제, 지수, 리사, 제니, 제니)
  print(blackPinkMap.values.toList());    // [로제, 지수, 리사, 제니, 제니]

  Set blackPinkSet = Set.from(blackPink); // [로제, 지수, 리사, 제니]

  print(backPinkSet.toList());
}
```

## List.map()

```dart
void main() {
  List<String> blackPink = ['로제', '지수', '리사', '제니', '제니'];

  Iterable<String> newBlackPink = blackPink.map((x){
    return '블랙핑크 ${x}';
  });

  print(blackPink);              // [로제, 지수, 리사, 제니, 제니]
  print(newBlackPink);           // (블랙핑크 로제, 블랙핑크 지수, 블랙핑크 리사, 블랙핑크 제니, 블랙핑크 제니)
  print(newBlackPink.toList());  // [블랙핑크 로제, 블랙핑크 지수, 블랙핑크 리사, 블랙핑크 제니, 블랙핑크 제니]

  Iterable<String> newBlackPink2 = blackPink.map((x) => '블랙핑크 ${x}');

  print(newBlackPink);           // (블랙핑크 로제, 블랙핑크 지수, 블랙핑크 리사, 블랙핑크 제니, 블랙핑크 제니)
  print(newBlackPink.toList());  // [블랙핑크 로제, 블랙핑크 지수, 블랙핑크 리사, 블랙핑크 제니, 블랙핑크 제니]


  String number = '13579';

  final parsed = number.split('').map((x) => '${x}.jpg').toList();
  print(parsed); // [1.jpg, 3.jpg, 5.jpg, 7.jpg, 9.jpg]
}
```

## Map.map();

```dart
void main() {
  Map<String, String> harryPotter = {
    'Harry Potter': '해리포터',
    'Ron Weasley': '론 위즐리',
    'Hermion Granger': '헤르미온 그레이저',
  };

  // key, value 변경
  Map<String, String> result = harryPotter.map((key, value) => MapEntry(
      'Harry Potter Character - ${key}',
      '해리포터 캐릭터 - $value'
  ));

  print(result);  // {Harry Potter Character - Harry Potter: 해리포터 캐릭터 - 해리포터, Harry Potter Character - Ron Weasley: 해리포터 캐릭터 - 론 위즐리, Harry Potter Character - Hermion Granger: 해리포터 캐릭터 - 헤르미온 그레이저}

  // map --> 리스트로 변경
  final keys = harryPotter.keys.map((x) => 'HPC ${x}').toList();
  final values = harryPotter.values.map((x) => '해리포터 ${x}').toList();

  print(keys);  // [HPC Harry Potter, HPC Ron Weasley, HPC Hermion Granger]
  print(values); // [해리포터 해리포터, 해리포터 론 위즐리, 해리포터 헤르미온 그레이저]

  // set --> set 변환
  Set blackPinkSet = {
    '로제',
    '지수',
    '제니',
    '리사',
  };

  final newSet = blackPinkSet.map((x) => '블랙핑크 ${x}').toSet();

  print(newSet);  // {블랙핑크 로제, 블랙핑크 지수, 블랙핑크 제니, 블랙핑크 리사}
}
```

## where

```dart
void main() {
  List<Map<String, String>> people = [
    {
      'name': '로제',
      'group' : '블랙핑크',
    },
    {
      'name': '지수',
      'group' : '블랙핑크',
    },
    {
      'name': 'RM',
      'group' : 'BTS',
    },
    {
      'name': '뷔',
      'group' : 'BTS',
    },
  ];

  print(people);  // [{name: 로제, group: 블랙핑크}, {name: 지수, group: 블랙핑크}, {name: RM, group: BTS}, {name: 뷔, group: BTS}]

  final newPeople = people.where((x) => x['group'] == '블랙핑크');

  print(newPeople);
}
```

## reduce

- reduce 함수를 호출하는 데이터 타입과 동일한 타입을 reduce 콜백 함수에서 리턴해야한다.

```dart
void main() {
  List<int> numbers = [
    1, 3, 5, 7, 9
  ];
  /**
  ------------
  prev : 1
  next : 3
  total : 4
  ------------
  prev : 4
  next : 5
  total : 9
  ------------
  prev : 9
  next : 7
  total : 16
  ------------
  prev : 16
  next : 9
  total : 25
  */

  int result = numbers.reduce((prev, next){
    print('------------');
    print('prev : ${prev}');
    print('next : ${next}');
    print('total : ${prev + next}');

    return prev + next;
  });

  print(result); // 25

  List<String> words = [
    '안녕하세요 ',
    '저는 ',
    '코드팩토리입니다.',
  ];

  final sentence = words.reduce((prev, next) => prev + next);
  print(sentence);  // 안녕하세요 저는 코드팩토리입니다.

}
```

## fold

- reduce와 다르게 아무 타입이든 반환할 수 있다.

```dart
void main() {
  List<int> numbers = [1, 3, 5, 7, 9];

  /**
  ------------
  prev : 0
  next : 1
  total : 1
  ------------
  prev : 1
  next : 3
  total : 4
  ------------
  prev : 4
  next : 5
  total : 9
  ------------
  prev : 9
  next : 7
  total : 16
  ------------
  prev : 16
  next : 9
  total : 25
  */
  final sum = numbers.fold<int>(0, (prev, next) {
    print('------------');
    print('prev : ${prev}');
    print('next : ${next}');
    print('total : ${prev + next}');

    return prev + next;
  });

  print(sum); // 25


  List<String> words = [
    '안녕하세요 ',
    '저는 ',
    '코드팩토리입니다.',
  ];

  final sentence = words.fold<int>(0, (prev, next) => prev + next.length);
  print(sentence);  // 18

}
```

## cascading operator - ...

```dart
void main() {
  List<int> even = [
    2, 4, 6, 8
  ];

  List<int> odd = [
    1, 3, 5, 7
  ];

  print([even, odd]);       // [[2, 4, 6, 8], [1, 3, 5, 7]]
  print([...even, ...odd]); // [2, 4, 6, 8, 1, 3, 5, 7]

  print(even == [...even]); // false
}
```

## example

```dart
void main() {
  List<Map<String, String>> people = [
    {
      'name': '로제',
      'group' : '블랙핑크',
    },
    {
      'name': '지수',
      'group' : '블랙핑크',
    },
    {
      'name': 'RM',
      'group' : 'BTS',
    },
    {
      'name': '뷔',
      'group' : 'BTS',
    },
  ];

  print(people);  // [{name: 로제, group: 블랙핑크}, {name: 지수, group: 블랙핑크}, {name: RM, group: BTS}, {name: 뷔, group: BTS}]

  final parsedPeople = people.map((x) => Person(
    name: x['name']!,
    group: x['group']!
  ));

  print(parsedPeople);  // (Person(name: 로제, group: 블랙핑크), Person(name: 지수, group: 블랙핑크), Person(name: RM, group: BTS), Person(name: 뷔, group: BTS))


  /**
  로제
  지수
  RM
  뷔
  */
  for(Person person in parsedPeople) {
    print(person.name); //
  }

  final bts = parsedPeople.where(
    (x) => x.group == 'BTS',
  );

  print(bts); // (Person(name: RM, group: BTS), Person(name: 뷔, group: BTS))

  final result = people.map(
    (x) => People(
      name: x['name']!,
      group: x['group']!,
    )
  ).where((x) => x.group == 'BTS');

  print(result);  //(Person(name: RM, group: BTS), Person(name: 뷔, group: BTS))
}

class Person {
  final String name;
  final String group;

  Person({
    required this.name,
    required this.group,
  });

  @override
  String toString() {
    return 'Person(name: ${this.name}, group: ${this.group})';
  }
}
```
