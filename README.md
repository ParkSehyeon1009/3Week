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
# 09장 메모리 모델과 이름 공간
<br>

**분할 컴파일**<br>

<br> **기억 존속 시간, 사용 범위, 링크**
<br>자동 기억 존속 시간 : 함수 매개변수를 포함하여 함수 정의 안에 선언된 변수가 가지는 존속 시간 <br> 프로그램 실행이 그들을 정의하고 있는 블록 안으로 들어갈때 생성 <br> 대입된 메모리는 프로그램 실행이 해당 함수나 블록을 떠날 때 해제
<br>정적 기억 존속 시간ㅍㅍ
