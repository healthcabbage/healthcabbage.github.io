reference[참조자]

```
const
call by reference
return reference
reference member -> 클래스가 참조자를 멤버로 가질 경우 주의해야 될점들
const TYPE& 
```

const (상수)

읽기 전용으로 객체가 변하는 것을 막게 해준다.

예시)

![image](https://user-images.githubusercontent.com/49223403/57350820-86ae8f80-719a-11e9-82b7-c2985b0c9eb4.png)

![image](https://user-images.githubusercontent.com/49223403/57350862-a80f7b80-719a-11e9-9545-db83456c1a73.png)

KTest t를 출력할 경우

Age = 49; 가 출력이 되었으나, const를 사용해 객체의 변경을 막으니 IncAge(), Print()가 함수 내부에서 값을 변경하는지 안하는지 아는 방법이 없다. 

여기서 IncAge는 값을 변경하므로 호출 되지 않아야 되고, Print()는 값을 변경시키지 않음으로 호출되어야 된다.

빌드를 해보면 에러메세지가 나오며, IncAge(), Print() 모두 에러가 발생한다. 

에러 메세지의 내용을 보면 this 포인터를 const Ktest에서 Ktest &로 변환할 수 없다고 뜬다.

![image](https://user-images.githubusercontent.com/49223403/57351004-3dab0b00-719b-11e9-8483-cb44701dc987.png)

컴파일러가 IncAge가 값을 변경하는지 않하는지 모르기 때문에 에러가 발생한 것이다.

값을 변경하는지 안하는지에 대한 것을 어떻게 알까?

-> 모든 멤버 함수 내부에는 객체 자신을 가리키는 this 포인트가 유지된다. 

실제로 값을 접근할 때, age는 this->age로 this에 age를 접근하는 코드가 된다. 

![image](https://user-images.githubusercontent.com/49223403/57351222-05f09300-719c-11e9-83fb-4bea673e2751.png)

this 포인터가 값을 변경시키지 않는다면, 멤버 함수 전체가 값을 변경하지 않는 것이다. this 함수를 const로 선언하면 되지만 this는 이미 존재하는 함수로 const 선언이 가능하지 않다. (변수가 아니기 때문이다.)

그래서 멤버함수를 정의할 때는 this는 멤버함수 내부의 상수다라고 선언이 가능하다.

![image](https://user-images.githubusercontent.com/49223403/57351356-9038f700-719c-11e9-9925-5146e6bf1553.png)

함수 이름 다음에 붙여 주면 this를 const로 선언하는 방법이다. 

컴파일러는 멤버변수 접근 혹은 멤버 함수 접근에서 값을 변경시키는 지 this가 상수로 처리되는지 확인이 가능하다.

![image](https://user-images.githubusercontent.com/49223403/57351446-e443db80-719c-11e9-9975-ee5b11fe1092.png)

IncAge()를 똑같이 상수 선언을 하지만 함수 내부에서 this로 접근하는 등호의 멤버가 왼쪽으로 사용되어 값이 변경된다는 의미로 에러가 난다.

![image](https://user-images.githubusercontent.com/49223403/57351558-4f8dad80-719d-11e9-9051-4a4991a10a9d.png)

const KTest t는 상수로 선언했을때 값이 변경되지 않는걸 보장하기 위해 멤버함수 호출은 상수 함수만 호출이 된다.

Print()는 상수함수 IncAge()논상수함수이기에 Print()만 호출이 가능하다. 