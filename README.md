# **0. 플러터 동작 방식**
플러터는 비디오 게임처럼 운영체제와 대화하지 않고 엔진을 이용해서 렌더링한다.<br>
운영체제는 그 엔진을 동작시키기만 한다.
## **0-1. 플러터 vs 리액트 네이티브**
플러터는 운영체제와 대화하지 않고 자체 C/C++ 엔진을 사용하기에 운영체제마다 스타일이 달라지지 않는다.<br>
리액트 네이티브는 운영체제와 직접적으로 대화하기에 같은 코드라도 운영체제 스타일에 맞게 변한다.<br>
그렇기에 플러터는 리액트 네이티브와 다르게 커스터마이징 된 디자인을 가질 수 있다.

## **0-2. Widget**
플러터에 모든 것은 위젯으로 이루어져 있다. 이 위젯들을 합치는 방식으로 앱을 만든다.<br>
`flutter create (프로젝트명)` 명령어로 프로젝트를 만들면 lib 폴더에 main.dart 파일이 있고, runApp() 함수가 있다.
```dart
// lib/main.dart
import 'package:flutter/material.dart';

void main() {
  runApp(/*위젯*/);
}
```
runApp()에 인자에는 클래스 형태인 위젯이 들어가는데 위젯을 만들기 위해서는 flutter SDK에 3개의 코어 위젯 중 하나를 상속받아야 한다.
```dart
// lib/main.dart
import 'package:flutter/material.dart';

void main() {
  runApp(App());
}

class App extends StatelessWidget {

}
```
그리고 StatelessWidget을 상속받은 클래스는 build() 메소드를 구현해줘야 한다.
```dart
...
class App extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    
  }
}
```
이 App 위젯을 루트 위젯이라고 하고 이 위젯의 build() 메소드는 MaterialApp 위젯 또는 CupertinoApp 위젯, 이 두개 중 하나를 반환해야한다.

Material과 Cupertino는 각각 구글과 애플의 디자인 시스템이다. 각각 구글 또는 iOS 느낌을 내고 싶을 때 선택하면 된다.

근데 플러터는 구글에서 만든 제품이기에 MaterialApp을 많이 선택된다고 한다.
```dart
class App extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp();
  }
}
```
MaterialApp의 인자에 home 이라는게 이 인자의 인수로 또다른 위젯을 넣어주면 된다.

플러터에서 모든 화면은 Scaffold 위젯을 가져야 한다.<br> Scaffold 위젯은 화면의 구조를 제공해준다.

Scaffold는 body 인자에 위젯이 들어가는데 Text 위젯을 이용하여 글자를 입력할 수도 있다.
```dart
...
Widget build(BuildContext context) {
    return MaterialApp(
        home: Scaffold(
            body: Text('Hello, world');
        )
    );
}
```
![](./images/0-2.1.png)

왼쪽 상단에 글자가 잘 뜨는 것을 확인할 수  있다.

Scaffold에 appBar라는 인자에도 위젯을 넣을 수 있다.<br>
```dart
...
return MaterialApp(
    home: Scaffold(
        appBar: AppBar(
            title: Text('Hello, flutter!'),
        ),
        body: Text('Hello, world');
    )
);
```
appBar 인자에 AppBar 위젯을 인수로 주고,<br>
AppBar 위젯에 title 인자에는 Text 위젯을 주었다.

![](./images/0-2.2.png)

상단에 AppBar가 잘 뜨는 것을 확인할 수 있다.

아래 텍스트를 가운데에 두고싶다면 Center()라는 또다른 위젯을 사용하면 된다.
```dart
return MaterialApp(
    home: Scaffold(
        appBar: AppBar(
            title: Text('Hello, flutter!'),
        ),
        body: Center(
            child: Text('Hello, world'),
        ),
    )
);
```
![](./images/0-2.3.png)

그럼 글자가 가운데에 잘 나타난다.

CSS의 모든 속성을 다 기억하고 있지 않듯이 위젯을 다 기억할 필요는 없다.<br>
문서를 찾아봐도 되고, VSC에 Extension이 보여주는 힌트를 볼 수도 있다.