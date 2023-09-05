<div align="center">
  
  ![header](https://capsule-render.vercel.app/api?type=Waving&text=Hello&animation=fadeIn&fontAlignY=35&height=150&color=auto)

#  :wave: Welcome my github profile !

## 성일정보고 소프트개발과 손은규
  
 <br/>
 <br/>
  
##  :clipboard: Once I've Used 
  
<img src="https://img.shields.io/badge/JAVA-007396?style=for-the-badge&logo=Java&logoColor=white">
<img src="https://img.shields.io/badge/Oracle-F80000?style=for-the-badge&logo=Oracle&logoColor=white"> 
<img src="https://img.shields.io/badge/Eclipse-2C2255?style=for-the-badge&logo=Eclipse%20IDE&logoColor=white">
<img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
<img src="https://img.shields.io/badge/VSCode-007ACC?style=for-the-badge&logo=VisualStudioCode&logoColor=white">

## :pencil2: Study log

[![Solved.ac](http://mazassumnida.wtf/api/v2/generate_badge?boj=kkwabaegi)](https://solved.ac/kkwabaegi)

![kkwabaegi's GitHub stats](https://github-readme-stats.vercel.app/api?username=kkwabaegi&show_icons=true&theme=transparent)
  
[![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=kkwabaegi&layout=compact&show_icons=true&theme=transparent)](https://github.com/kkwabaegi)
  
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fkkwabaegi&count_bg=%2379C83D&title_bg=%23555555&icon=katana.svg&icon_color=%23FFFFFF&title=%EB%B0%A9%EB%AC%B8%EC%9E%90&edge_flat=false)](https://hits.seeyoufarm.com)
  
</div>
  Vs code 
C+S+P
user setting(json)

//트리모양 나오기
"dart.previewFlutterUiGuides": true,

//저장시 자동 수정(const 추가)
"editor.codeActionsOnSave": {
        "source.fixAll": true
    },

//자동 줄바꿈
"editor.formatOnSave": true,

C+S+P
reload 개발자: 창 다시 로드

HTML꾸미기 참고 사이트:부트스트랩

아이콘 찾는데 : 어섬폰트

이미지 사용 : flutter run -d chrome --web-renderer html

import 'package:flutter/material.dart';

class AddPage extends StatefulWidget {
  String filePath;
  AddPage({super.key, required this.filePath});

  @override
  State<AddPage> createState() => _AddPageState();
}

class _AddPageState extends State<AddPage> {
  String filepath = '';

  List<TextEditingController> controllers = [
    TextEditingController(),
    TextEditingController(),
  ];

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    filepath = widget.filePath;
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(filepath),
        centerTitle: true,
      ),
      body: Form(
          child: Padding(
        padding: const EdgeInsets.all(10.0),
        child: Column(
          children: [
            TextFormField(
              controller: controllers[0],
              decoration: const InputDecoration(
                border: OutlineInputBorder(),
                label: Text('title',
                    style: TextStyle(fontSize: 20, color: Colors.green)),
              ),
            ),
            const SizedBox(
              height: 20,
            ),
            Expanded(
              child: TextFormField(
                controller: controllers[1],
                maxLines: 11,
                maxLength: 100,
                decoration: const InputDecoration(
                  border: OutlineInputBorder(),
                  label: Text('contents',
                      style: TextStyle(
                        fontSize: 40,
                        color: Colors.green,
                      )),
                ),
              ),
            ),
            ElevatedButton(
              onPressed: () {
                var title = controllers[0].text;
                var content = controllers[1].text;
                //print(title);
                Navigator.pop(context, "$title $content");
              },
              child: const Text('저장'),
            )
          ],
        ),
      )),
    );
  }
}


-----


import 'package:flutter/material.dart';
import 'package:flutter_application_diary/add_page.dart';

class MainPage extends StatefulWidget {
  const MainPage({super.key});

  @override
  State<MainPage> createState() => _MainPageState();
}

class _MainPageState extends State<MainPage> {
  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Main(),
    );
  }
}

class Main extends StatefulWidget {
  const Main({
    super.key,
  });

  @override
  State<Main> createState() => _MainState();
}

class _MainState extends State<Main> {
  dynamic result = 'Hello';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Main Page'),
      ),
      body: SizedBox(
          width: double.infinity,
          height: double.infinity,
          child: Column(
            children: [
              Text(
                result.toString().split(' ')[0],
                style: const TextStyle(fontSize: 50),
              ),
              Text(
                result.toString().split(' ')[1],
                style: const TextStyle(fontSize: 20),
              ),
            ],
          )),
      floatingActionButton: FloatingActionButton(
          onPressed: () async {
            result = await Navigator.push(
              context,
              MaterialPageRoute(
                builder: (context) => AddPage(filePath: 'temp'),
              ),
            ); //context 화면 순서 관리,
            print(result);
            setState(() {});
          },
          child: const Icon(
            Icons.add_circle_outline,
            size: 40,
          )),
    );
  }
}
----

import 'package:flutter/material.dart';
import 'package:flutter_application_diary/main_page.dart';

void main() {
  runApp(const MainPage());
}
