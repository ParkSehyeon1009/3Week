# 3Week
# 현재 코드 및 내용 정리중 (2023-07-27 10:47)
# 함수 포인터 인자 / 반환값 활용 예제
```cpp
int add(int a, int b){return a + b;}
int sub(int a, int b){return a - b;}
int mul(int a, int b){return a * b;}
int div(int a, int b){return a / b;}

int main()
int (*fp[4])(int, int); //함수 포인터 배열 선언
fp[0] = add; 
fp[1] = sub;
fp[2] = mul;
fp[3] = div;

for (int i = 0; i < 4; i++)
{
  cout << fp[i](20,10) << endl;
}

return 0;
```
결과값은 아래와 같다.
```
30
10
200
2
```
<br>

# 제네릭 프로그래밍 활용 예제
# 09장 메모리 모델과 이름 공간
<br>

**분할 컴파일**<br>

<br> **기억 존속 시간, 사용 범위, 링크**
<br>자동 기억 존속 시간 : 함수 매개변수를 포함하여 함수 정의 안에 선언된 변수가 가지는 존속 시간 <br> 프로그램 실행이 그들을 정의하고 있는 블록 안으로 들어갈때 생성 <br> 대입된 메모리는 프로그램 실행이 해당 함수나 블록을 떠날 때 해제
<br>정적 기억 존속 시간 : 프로그램이 실행되는 전체 시간 동안 존속되는 영역, 정의된 모든 함수는 기본적으로 정적 기억 존속 시간내에 포함(외부 링크를 가진다)
쓰레드 존속시간 : 해당 쓰레드가 존속되는 전체 실행시간동안 유지되는 영역(Storage-Class Specifier을 통해 구현가능)
동적 기억 존속 시간 : 자유공간 혹은 힙이 해당되는 영역, 사용자가 메모리 제어 권한을 가진다. 단 동적으로 할당받은 메모리를 해제하지 않을 경우 메모리누수 발생

-사용 범위와 링크
사용범위 : 어떤 이름이 하나의 파일 안에서 얼마나 널리 알려져 있는가를 나타냄
링크 : 서로 다른 번역 단위들이 이름을 공유

-정적변수
프로그램이 종료되기 전까지 메모리가 소멸되지 않는 변수

-정적 존속 시간, 외부링크
일반적으로 외부 변수라 부르는 변수가 이에 속함
어떤 블록에도 속하지 않는 바깥에 이름을 선언해 정의
프로그램을 구성하는 모든 파일에서 프로그램 종료시 까지 사용할수 있음
하나의 변수에 대하여 한번의 정의만을 허용
단 모든 각각의 파일에 선언되어야 하는데 이러한ㄴ 점이 ODR을 위배함으로 extern 키워드 제공

**정적 존속 시간, 내부링크**
서로 다른 파일에서 서로 다른 변수들에게 같은 이름을 사용하는 법
같은 이름으로 정의된 외부 변수를 하나의 파일에서 sttic 외부 변수로 선언한다면, static으로 선언된 변수는 파일에서만 사용되는 변수로 인식

-기억 공간 제한자
register
static
extern
thread_local
mutable

-cv 제한자
const
voladtile

-함수와 링크
모든 함수는 정적 기억 존속 시간을 가진다
함수는 외부 링크를 가진다
static 키워드를 사용하여 함수에 내부 링크 부여 가능
함수의 사용범위를 하나의 파일로 제한
```
static int private(double x);

혹은

static int private((double x)
{
 ...
}
```
-새로운 이름 공간 기능
중복되는 함수나 변수 이름을 모두 변경하지않고 충돌하지 않도록 하기위한 문법

-using 선언, using 지시자
using 지시자가 명시한 네임스페이스의 모든 이름을 사용할수 있게 했다면 using 선언은 단 하나의 이름만을 범이 지정 연산자를 사용하지 않고도 사용할 수 있게 해줌
