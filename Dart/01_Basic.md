# 다트 기본기

## 변수
1. 변수는 `var`로 선언
2. 같은 스코프 내 변수 재선언 불가
3. 변수 타입 : String(문자), int(정수), double(실수), bool, var(할당된 값으로 타입 유추), dynamic(어떤 타입이던지 가능)
    - 변수 타입 체크 : `변수.runtimeType`
    - string은 `+`로 문자열 연결 가능
    - ''안에 `${변수명}` 형식으로 사용 가능
    - var는 한번 선언할 때 해당 타입으로 고정, dynamic은 선언 후 다른 타입 할당 가능
4. nullable, non-nullable, null
    - 변수 타입 뒤에 `?` 넣으면 nullable
    - 변수 타입 뒤에 `!` 넣으면 non-nullable
5. final, const로 선언할 시 재할당 불가능
    - final : 선언, 할당 따로 가능
    - const : 선언과 동시에 초기화 진행 (할당)
    - final, const 사용 시 var 키워드 생략 가능
6. DateTime
    - DateTime 값은 now 함수 또는 utc, parse 함수 사용
    - DateTime.now() 실행 시 코드가 실행되는 시점을 기록
    - const 키워드는 빌드 타임에 값을 알고 있어야 하기 때문에 DateTime과 함께 사용 불가 (final은 사용 가능)


## Operator
- null operator (`변수 ??= 값`) : 해당 변수가 null 값일 때 우항의 값 할당 
- type check operator (`변수 is 타입`) : bool 값 반환
- 해당 타입이 아닌지를 체크하려면 `is!` 사용
- logical operator : and (`&&`), or (`||`)


## 객체
- List : `List<type>` 형태로 사용 -> `List<int> num = [1, 2];`
- Map :`Map<key, value>` 형태로 사용 -> `Map<String, int> = {'age':20}`
- Set : `Set<type>` 형태로 사용 -> `Set<String> name = {"seon", "zoo"}`
    - List는 중복을 허용하는 반면, Set은 중복값을 처리한다.

## enum
- 특정 값만 존재한다는 것을 명시하기 위해 사용


## 함수
- positional parameter : 순서가 중요
    - optional한 매개변수는 대괄호로 묶어줌
- named parameter: 순서가 바뀌어도 상관없음
    - 필수값은 required 키워드 붙여서 사용
    - optional한 값은 기본값 붙여서 사용
    - 함수 호출 시 => `addNumbers(x:1, y:2)` 형태로 사용
- void : return하는 값이 없는 함수
- positional parameter와 named parameter 혼용 가능
- arrow function : inline function일 경우 return 키워드 생략 가능
- typedef : 함수 타입 정의하는데 사용 => `typedef 유형 이름 = 함수 타입`
```dart
typedef Operation = int Function(int x, int y, int z);

int add(int x, int y, int z) => x + y + z;
int subtract(int x, int y, int z) => x - y - z;

int calculate(int x, int y, int z, Operation operation){
    return operation(x, y, z)
}

void main () {
    Operation operation = add;

    int result = operation(10, 20, 30);

    print(result); // 60

    operation = subtract;

    int result2 = operation(10, 20, 30);

    print(result2); // -40

    int result3 = calculate(30, 40, 50, add);

    print(result3); // 60;

    int result4 = calculate(30, 40, 50, subtract);

    print(result4); // -40
}
```