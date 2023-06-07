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
import 'package:flutter_image_slideshow/flutter_image_slideshow.dart';
import 'package:readmore/readmore.dart';

class MovieDetail extends StatelessWidget {
  Map<String, dynamic> movie;

  MovieDetail({super.key, required this.movie});

  @override
  Widget build(BuildContext context) {
    var movieTitle = movie['title']
        .toString()
        .replaceAll(' !HS ', '')
        .replaceAll(' !HE ', '');
    dynamic titleImage = movie['posters'].toString().isEmpty
        ? Image.asset('assets/images/no_image.png')
        : Image.network(movie['posters'].toString().split('|')[0]);
    //var stills = movie['stlls'].toString().split('|');
    List<Widget> stills = [];
    if (movie['stlls'].toString().isEmpty) {
      stills.add(Image.asset(
        'assets/images/no_image.png',
        fit: BoxFit.fitHeight,
      ));
    } else {
      for (var k in movie['stlls'].toString().split('|')) {
        stills.add(Image.network(
          k,
          fit: BoxFit.fitHeight,
        ));
      }
    }

    //만약 없으면 로컬 이미지
    //있으면 네트워크 이미지
    return Scaffold(
      appBar: AppBar(title: Text('영화 상세 정보($movieTitle)')),
      body: Padding(
        padding: const EdgeInsets.all(10),
        child: SingleChildScrollView(
          child: Column(
            children: [
              SizedBox(
                height: 100,
                child: Center(
                  child: Text(movieTitle,
                      style: const TextStyle(
                          fontSize: 50, fontWeight: FontWeight.bold)),
                ),
              ),
              Row(
                children: [
                  Expanded(
                      child: Text(
                    '키워드 : ${movie['keywords']}',
                    style: const TextStyle(
                      fontSize: 20,
                    ),
                  )),
                  Container(
                      width: 300,
                      alignment: Alignment.centerRight,
                      child: Hero(tag: movie['movieSeq'], child: titleImage))
                ],
              ),
              const SizedBox(
                height: 20,
              ),
              ReadMoreText(
                movie['plots']['plot'][0]['plotText'],
                textAlign: TextAlign.left,
                trimLines: 2,
                trimMode: TrimMode.Line,
                trimCollapsedText: 'Show more',
                trimExpandedText: 'Show less',
                style: const TextStyle(fontSize: 15),
                moreStyle: const TextStyle(
                    fontSize: 14,
                    fontWeight: FontWeight.bold,
                    color: Colors.red),
                lessStyle: const TextStyle(
                    fontSize: 14,
                    fontWeight: FontWeight.bold,
                    color: Colors.blue),
              ),
              ImageSlideshow(
                  autoPlayInterval: 3000,
                  isLoop: true,
                  width: double.infinity,
                  height: 200,
                  children: stills)
            ],
          ),
        ),
      ),
    );
  }
}
