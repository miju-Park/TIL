# Chrome DevTools 사용팁
| 참고 사이트 : https://medium.com/javascript-in-plain-english/use-chrome-devtools-like-a-senior-frontend-developer-99a4740674

## 커맨드 
* 윈도우 : Ctrl + Shift + P
* Mac : Cmd + Shift + P

위 단축키로 입력하거나 아래 화면과 같이 메뉴로 진입하면 커맨드 메뉴를 사용할 수 있다.

![](https://miro.medium.com/max/875/1*yLkbB362F69UWTK-Pku3_g.png)

커맨드 패널에는 다양한 종류의 기능들이 제공된다.

![](https://miro.medium.com/max/875/1*hk4R78EHvQqu2HmpUSLKyQ.gif)

## 스크린샷

전체 화면은 캡쳐하거나 특정 DOM을 캡쳐하고 싶을 때, 위 커맨트 패널에서 가능하다.

* Screenshot Capture full size screenshot
 : 현재 페이지 전부를 캡쳐할 수 있다.
* Capture node screenshot
 : Elements를 선택하고 난 후 위 커맨드를 실행하면 특정 DOM을 정확하게 캡쳐할 수 있다.

 ## 콘솔의 마지막 실행 결과 참조값

 콘솔에서 디버깅 하는 경우, 이전 실행 결과값을 저장하는 내부 변수 **$_** 를 사용할 수 있다.

 ## XHR 재요청

 페이지 내에서 호출되었던 리퀘스트를 다시 요청하고자 할 때, 페이지 새로고침 대신 **Replay XHR**을 사용해보자.

 * 네트워크 탭 > XHR 선택 > Replay XHR 실행

 ![](https://miro.medium.com/max/875/1*230w0KnTpsa7c62SdvpTLA.png)

## 객체 배열을 테이블로 보기

```javascript
let users = [{name: 'Jon', age: 22},
  {name: 'bitfish', age: 30},
  {name: 'Alice', age: 33}]
```
위와 같은 형태의 객체 배열이 있다고 가정해봤을 때, 콘솔에서 객체 내용을 한눈에 확인하기는 쉽지 않다.
![](https://miro.medium.com/max/875/1*eQXZ734rw66Tbvmo_-9gMQ.png)

이 때, 크롬에서 객체 배열을 테이블 형태로 보여주는 기능을 제공한다.

* 콘솔 > table(배열변수명)

아래와 같이 배열 값을 출력해준다.

![](https://miro.medium.com/max/875/1*irMyKccSEIIW8Ex4CAO-0A.png)

## $0 (선택된 Element를 콘솔에서)

**$0** 역시 내부 변수로 현재 선택된 element를 참조하는 값이다.

* Element > 특정 element 선택 > Console > $0 입력시, 해당 element 출력

## H (Element 바로 숨기기)

Element를 바로 숨길 수 있는 단축키가 **H** 이다.

Element 선택한 후, H 입력 시 바로 visibility:hidden 스타일을 적용시켜준다. 
