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
