hashcode()와 equals() 차이
===

hashcode에 대한 이해
---

hashcode() : 객체의 해시코드 값을 반환. 

HashMap, HashTable : key - value 쌍으로 객체를 보관하는 도구
=> HashMap, HashTable은 hashcode를 이용함으로써, 객체를 저장하는 다른 도구들(ex.ArrayList)에 비해 장점을 가짐

장점?
Key의 hashcode를 통해 value 값을 더 쉽게 찾아낼 수 있음.(key값에는 어떤 객체든 올 수 있음 -> 객체보다 int값(hashcode)를 찾는 것이 편리


![hashcode 예시1 - member클래스](https://mblogthumb-phinf.pstatic.net/MjAxNzAyMDhfOCAg/MDAxNDg2NTI0MDI0Nzg2.IcNAK9PbIw5_uRfo-IBOUqNQMvHNNeSMhM7IPyV6elsg.0YMyQLWAdDIDkluOw7Viu51JQvi4PBiGWS_9lFFgea4g.PNG.travelmaps/Member.PNG?type=w800)
-> member 클래스 (이름과 나이를 저장하는 회원 형태의 클래스)

![hasecode 예시2 - main](https://mblogthumb-phinf.pstatic.net/MjAxNzAyMDhfMjk5/MDAxNDg2NTI0MDgzMDM5.dpcY_2VPRYVmZ629dsVnLd96_fw3P-s_4yfbUgGO7Jkg.YDJrHZMkJITuvinX1FkdWt0KOOy5e48cOT7cBh-jnqcg.PNG.travelmaps/result.PNG?type=w800)

![위의 코드 결과](https://mblogthumb-phinf.pstatic.net/MjAxNzAyMDhfMjE0/MDAxNDg2NTI0MTE3OTMx._IkJgXq0WvdEvRy7-dUbs2L0OR4JY49IqgRNVCDjNDUg.lvzdOa_landfdLUYJIJWGhSPL-tf5z8dfrA7GUTi8UYg.PNG.travelmaps/result1.PNG?type=w800)

첫 줄 15db9742는 16진수/ 이를 10진수로 변환시킨 366712642가 object 객체의 hashcode 리턴값.
서로 다른 객체는 서로 다른 주소값을 갖기 때문에 다른 hashcode 값을 가짐.

__hashcode() 메소드는 각 객체에 대응되는 고유한 정수값을 리턴__

--> 현재 hashcode메소드는 Object클래스에서 정의된 그대로의 메소드 (주소값과 연관이 있음)
--> _Member클래스를 정의할 때 hashcode메소드를 오버라이드하여 변경하지 않았기 때문에 Object클래스에서 정의된 그대로의 메소드임_

___하지만! String의 경우는 hashcode가 주소값과 관련 없음___
String클래스는 hashcode 오버라이드 과정을 통해 새롭게 정의

String클래스에서 hashcode
---

String클래스에서는 hashcode메소드를 재정의함.
__같은 문자열은 같은 hashcode값을 가짐!!__

if, String클래스에서 hashcode를 재정의하지 않으면, 
String a = "자바"
String b = new String("자바")
a와 b의 hashcode는 서로 다른 값이어야 함

but,
String 클래스 입장에서 a와 b는 같은 객체 (같은 문자열이기 때문)
같은 문자열을 갖는 두 객체의 __hashcode가 다르면 hashcode의 의미가 없어짐/ hashcode를 활용해서 Map이나 Set에 저장된 Key값을 찾아야 하는데,
같은 객체인데도 불구하고 hashcode값이 다르면, 제대로 찾을 수 없음__

따라서 인위적으로 String클래스 안에서의 hashcode메소드를 재정의하여 같은 String객체에 대해(equals 리턴값이 true) hashcode가 같아지도록 함.

hashcode와 equals의 차이
---

![새롭게 정의된 클래스]



