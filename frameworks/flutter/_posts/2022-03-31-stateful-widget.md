---
title: "플러터 : Stateful 위젯"
excerpt: Stateful 위젯이 무엇인지 알아본다.
header:
  actions:
    - label: 플러터 더 알아보기
      url: https://jinhyun.blog/frameworks/flutter/
---

`Stateless` 위젯은 변경할 수 없습니다. 즉, 속성을 변경할 수 없으며 모든 값이 최종적입니다.

`Stateful` 위젯은 위젯의 수명기간 동안 변경될 수 있는 상태를 유지합니다. 상태 저장 위젯을 구현하려면 최소한 두 개의 클래스가 필요합니다.

1. 인스턴스를 생성하는 `StatefulWidget` 클래스
2. `State` 클래스

`StatefulWidget` 클래스는 그 자체로 변경할 수 없으며 버리고 다시 생성할 수 있지만 `State` 클래스는 위젯의 수명기간 동안 지속됩니다.

실제로 어떻게 적용되는지 확인해보도록 하겠습니다.

처음 프로젝트를 생성하면 `main.dart` 파일의 소스 코드는 다음과 같습니다.

{% highlight dart linenos %}

import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({Key? key, required this.title}) : super(key: key);

  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: const Icon(Icons.add),
      ),
    );
  }
}

{% endhighlight %}

위 앱은 플로팅 버튼을 클릭하면 _counter 변수가 증가되고 출력됩니다.

이제 구조적으로 어떻게 작동하는지 설명하겠습니다.

MyHomePage 클래스는 StatefulWidget을 상속받았습니다. StatefulWidget은 인스턴스를 만드는 클래스라고 앞서 설명했습니다. State를 만드는 createState() 메서드를 통해 _MyHomePageState 클래스를 생성합니다.

_MyHomePageState 클래스는 State를 상속받았습니다. 제네릭은 MyHomePage로 타입이 지정되었습니다. State 클래스는 수명기간동안 변경할 수 있는 상태를 유지한다고 앞서 설명했습니다. 이를 좀 더 풀어 말하면 State를 상속받은 인스턴스의 메모리가 반환되기 전까지 텍스트나 이미지, 목록 등이 실시간이나 원할 때 변경될 수 있다는 의미입니다.
