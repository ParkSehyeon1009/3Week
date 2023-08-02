# 3Week

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
```cpp
#include<iostream>
using namespace std;

class Circle {
	int radius;//private
public:
	Circle(int radius = 1) {
		this->radius = radius;
	}
	int getRadius() {
		return radius;
	}
};

template<class T>
void myswap(T& a, T& b) {
	T tmp;
	tmp = a;
	a = b;
	b = tmp;
}

void main() {
	int a = 4, b = 5;
	myswap(a, b);
	cout << "a=" << a << "," << "b=" << b << endl;

	double c = 4, d = 5;
	myswap(c, d);
	cout << "a=" << a << "," << "b=" << b << endl;
	
	Circle donut(5), pizza(20);
	myswap(donut, pizza);
	cout << "donut 반지름=" 
    << donut.getRadius() << endl;
	cout << "pizza반지름=" 
    << pizza.getRadius() << endl;
}
```
# 09장 메모리 모델과 이름 공간
<br>

**분할 컴파일**<br>

<br> **기억 존속 시간, 사용 범위, 링크**
<br>자동 기억 존속 시간 : 함수 매개변수를 포함하여 함수 정의 안에 선언된 변수가 가지는 존속 시간 <br> 프로그램 실행이 그들을 정의하고 있는 블록 안으로 들어갈때 생성 <br> 대입된 메모리는 프로그램 실행이 해당 함수나 블록을 떠날 때 해제
<br>정적 기억 존속 시간 : 프로그램이 실행되는 전체 시간 동안 존속되는 영역, 정의된 모든 함수는 기본적으로 정적 기억 존속 시간내에 포함(외부 링크를 가진다)
<br>쓰레드 존속시간 : 해당 쓰레드가 존속되는 전체 실행시간동안 유지되는 영역(Storage-Class Specifier을 통해 구현가능)
<br>동적 기억 존속 시간 : 자유공간 혹은 힙이 해당되는 영역, 사용자가 메모리 제어 권한을 가진다. 단 동적으로 할당받은 메모리를 해제하지 않을 경우 메모리누수 발생

<br>**사용 범위와 링크**<br>
<br>사용범위 : 어떤 이름이 하나의 파일 안에서 얼마나 널리 알려져 있는가를 나타냄
<br>링크 : 서로 다른 번역 단위들이 이름을 공유
<br>
<br>**정적변수**<br>
<br>프로그램이 종료되기 전까지 메모리가 소멸되지 않는 변수

<br>**정적 존속 시간, 외부링크**<br>
<br>일반적으로 외부 변수라 부르는 변수가 이에 속함<br>
<br>어떤 블록에도 속하지 않는 바깥에 이름을 선언해 정의<br>
<br>프로그램을 구성하는 모든 파일에서 프로그램 종료시 까지 사용할수 있음<br>
<br>하나의 변수에 대하여 한번의 정의만을 허용<br>
<br>단 모든 각각의 파일에 선언되어야 하는데 이러한 점이 ODR을 위배함으로 extern 키워드 제공<br>
<br>
<br>**정적 존속 시간, 내부링크**<br>
<br>서로 다른 파일에서 서로 다른 변수들에게 같은 이름을 사용하는 법
<br>같은 이름으로 정의된 외부 변수를 하나의 파일에서 sttic 외부 변수로 선언한다면, static으로 선언된 변수는 파일에서만 사용되는 변수로 인식
<br>
<br>**기억 공간 제한자**<br>
<br>register : 자료형이나 앞 또는 뒤에 붙는 키워드, cpu와 가까운 레지스터 공간을 사용하여 연산 속도를 높임
```cpp
register int a;
int register a;
```
<br>static : 생성된 스코프가 종료한 이후에도 해당 값을 유지하게 해주는 변수로 만들어줌
```cpp
static int value = 1;
```
<br>extern : 다른 파일에서 선언한 전역변수를 가볍게 호출만 하여 프로젝트에서 사용하고 싶을때 사용
```cpp
//a.cpp

int number = 100;
```
```cpp
b.cpp

extern int number;
```
<br>thread_local : TLS를 지원하기 위해 추가된 기능
<br>TLS : thread별로 고유한 저장공간을 가질수 있는 방법
```cpp
thread_local unsigned int i = 0;
```
위와 같이 선언하면 변수는 각각의 thread에서만 동작한다.
<br>
<br>mutable : const함수 내부에서 멤버 변수드르이 값을 바꿀때 사용
```cpp
mutable int data_;
void printData(int x) const {data_ = x; // 변경 가능}
```

<br>**cv 제한자**
<br>volatile : 변수가 스레드에 의해 비동기적으로 변경될 수 있음을 알리기 위해 사용되는 제한자<br>
이 제한자는 final 변수를 제외한 변수에 선언될 수 있다.

<br>**함수와 링크**<br>
<br>
<br>모든 함수는 정적 기억 존속 시간을 가진다
<br>함수는 외부 링크를 가진다
<br>static 키워드를 사용하여 함수에 내부 링크 부여 가능
<br>함수의 사용범위를 하나의 파일로 제한
```
static int private(double x);

혹은

static int private((double x)
{
 ...
}
```
<br> **새로운 이름 공간 기능** <br>
<br>중복되는 함수나 변수 이름을 모두 변경하지않고 충돌하지 않도록 하기위한 문법
<br>
<br> **using 선언, using 지시자** <br>
<br>using 지시자가 명시한 네임스페이스의 모든 이름을 사용할수 있게 했다면 using 선언은 단 하나의 이름만을 범이 지정 연산자를 사용하지 않고도 사용할 수 있게 해줌
