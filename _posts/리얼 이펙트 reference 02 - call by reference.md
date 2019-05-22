리얼 이펙트 reference 02 - call by reference

call by value 

가장 일반적인 함수 호출의 형태로 호출방식은 값의 복사로 이루어진다. 값을 인자로 전달하는 함수의 호출 방식

Call by reference

함수 호출 시 변수의 주소를 전달해 인자로 전달된 주소가 가리키는 변수의 조작을 함수 내에서 가능하게 하는 것. 주소 값을 인자로 전달하는 함수의 호출방식

예시) Swap 함수를 사용하여 Call by value 와 Call by reference

![image](https://user-images.githubusercontent.com/49223403/58148204-c300e600-7c98-11e9-85fb-80bc65ed9384.png)

main 안에 swap 함수를 만들어 구현하게 되는 경우 정상적으로 swap 된다.

![image](https://user-images.githubusercontent.com/49223403/58148219-dad86a00-7c98-11e9-98a8-68158f5926a9.png)

swap을 main 밖에 만들어 코드를 실행하면 swap 되지않고 main의 i, j값이 출력된다.

![image](https://user-images.githubusercontent.com/49223403/58148298-21c65f80-7c99-11e9-87c9-1d70a7e358d7.png)

![image](https://user-images.githubusercontent.com/49223403/58148323-44f10f00-7c99-11e9-9fcb-f3ba5f864f98.png)

swap의 i의 값이 메인의 i값과 상관없는 곳에 호출 되기 때문이다.

![image](https://user-images.githubusercontent.com/49223403/58148536-348d6400-7c9a-11e9-87bf-df2da6fbf3b4.png)

메인과 swap 함수의 스택 메모리

![image](https://user-images.githubusercontent.com/49223403/58148668-9bab1880-7c9a-11e9-8974-e68ec17abf47.png)

swap함수에서는 i와 j의 값이 서로 바뀌지만 main에서 swap을 호출했을 때의 i와j 값으로 초기화 된다. 

swap 함수에서 빠져나와 main에서 출력될 때는 swap 함수 호출하기 전의 메모리상태가 복구가 되어 2,3이 출력이 된다. 이것을 메인으로 retrun from swap()이라고 한다.

Swap 함수가 값을 복사해서 가져가도 main에서 값이 변하지 않는 문제점을 지니게 된다. i와 j를 전달 할 때 i,j를 전달하는게 아닌 주소 값을 전달하여 저장하는 방식을 이용하면 문제점이 해결 된다.

![image](https://user-images.githubusercontent.com/49223403/58148845-47546880-7c9b-11e9-8721-d45eb10fea7e.png)

주소값을 전달하기 위해 바뀐 코드. i와 j의 주소값을 전달 받는다.

![image](https://user-images.githubusercontent.com/49223403/58149001-01e46b00-7c9c-11e9-8539-930bc78f5a43.png)

주소값을 전달 받은 Swap 함수

Swap의 i의 값은 무슨 값으로 초기화 되는가? -> Swap을 호출 했을 때의 i값의 주소값을 호출하게 된다.

포인터를 사용하여 main의 i와 j의 값을 변경한 것이다. 

Swap 함수를 빠져나오면서 return form Swap()이 되면서 Swap 함수의 메모리가 Pop 된다.

코드를 실행하면 정상적으로 Swap 되어 출력된다.

![image](https://user-images.githubusercontent.com/49223403/58149187-cbf3b680-7c9c-11e9-8c7a-1b8becac2801.png)