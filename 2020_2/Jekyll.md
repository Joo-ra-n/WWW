# Jekyll로 나도 블로그 좀 만들어보자

요즘 구글링을 좀 하다보면 드는 생각인데, github pages를 이용한 블로그들이 좀 눈에 띄는 것 같다.  본인은 어떤 키워드에 대해 구글링을 했을 때, 다음 블로그가 나오면 무조건 거르고, 네이버 블로그가 나오면 일단 들어가서 스크롤을 쭉 내려본다. 그리고 우리가 높은 확률로 마주하는 것은...

![naverblog](Jekyll.assets/naverblog.jpg)

~~신뢰의 이모티콘~~이 친구다.. 물론 이는 대체로 가십거리일 때의 이야기이지만, 무슨 라플라스 변환 표 구하는 것도 아니고 어떠한.. 전문 지식(최소 학부 수준)을 네이버 블로그에서 얻는다면 그것도 좀 문제가 있어 보인다.~~아니라고?~~ 해서 티스토리..가 좀 더 전문적으로 보일 확률이 있는데, 진짜! 개발자라면! Jekyll을 이용해서 블로깅을 할 수 있다. 이제 내가 당신에게 그것을 어떻게 설명해 주도록 하겠다. 잘 따라오도록 하여라.

## Jekyll이 뭔데?

> **Jekyll** is a simple, blog-aware, static site generator for personal, project, or organization sites. Written in Ruby by Tom Preston-Werner, [GitHub's](https://en.wikipedia.org/wiki/GitHub) co-founder, it is distributed under the open source MIT license.
>
> (영문 위키피디아 발췌)

진짜.. 본인도 영어 3등급을 받은 영포자라고 할 수 있다. 하지만 본인이 재수하던 시절, 강순동(영어 선생님임) 선생님은 이렇게 말씀하셨다.

> that 부터 버려삐라!

물론 저 글에는 `that`이 없다. 아마 중요한 부분만 해석하라는 뜻으로 말씀하셨던 것 같은데, 차근차근 중요한 단어를 짚어보자.

##### simple, blog-aware, static site generator

간단하고, 블로그에 관심 많고, 정적인 사이트 생성기라고 한다. 앞의 두 개는 쉽게 이해가 가는 데, 정적인 사이트가 대관절 무엇일까? 물론 앞에서 잘 설명해 주었을 수도 있지만, 원래 탑솔러는 남을 잘 믿지 않는다. 해서 내가 다시 설명해 주도록 하겠다.

### 정적 웹 페이지?

![static_webpage](https://github.com/Joo-ra-n/WWW/raw/master/SoftwareHighSchool/statics/classdata/jekyll/staticwebsite.PNG)

위 사진은 `정적 웹 페이지`의 구동 방식을 나타낸 것인데, 왼쪽에 보이는 PC가 사용자고, 오른쪽에 저 첩첩첩 쌓여있는것이 웹 서버다. 사용자는 WWW를 통해 웹 페이지에 무엇가를 요청(Request)하게 된다. 이 때 웹 서버는 따로 어떤 작업을 하지 않고 그대로 HTML 문서를 출력해주게 된다. 대표적으로 메모장을 켜서 `뭐시기.html` 파일을 만들어서 기본적인 HTML 문서를 만들면? 그게 바로 정적 웹 페이지가 된다. 그렇다면 동적 웹 페이지도 있을까?

![dynamic_webpage](https://github.com/Joo-ra-n/WWW/raw/master/SoftwareHighSchool/statics/classdata/jekyll/dynamicwebsite.PNG)

물론 있다. 마찬가지로 위 사진은 `동적 웹 페이지`의 구동 방식을 나타낸 것이고, 똑같이 왼쪽의 PC가 사용자고, 오른쪽의 첩첩첩이 웹 서버다. 여기서 다른 것은, 웹 서버는 따로 데이터베이스 서버를 두어서, 사용자가 어떤 페이지를 요청했을 때 내부 프로세싱을 거쳐 HTML 문서를 작성한 후에 그 문서를 출력해주게 된다.(django를 활용해 만들었던 페이지들이 그 예다.)

이러한 구조적 차이로 인해 `정적 웹 페이지`와 `동적 웹 페이지`의 장단점이 발생하는데,

**정적 웹 페이지**

+ 장점
  + 로딩 속도가 빠르다(따로 뭔가 처리할 필요 없이 요청한 페이지를 바로 출력하면 됨).
  + 유지비가 적게 든다(데이터베이스 서버 필요 없음).
+ 단점
  + 비전문가가 사용하기에 쉽지 않다.
  + 서비스가 한정적이다(이미 저장된 정보만 보여줄 수 있음).

**동적 웹 페이지**

+ 장점
  + 서버 안에 저장된 데이터들을 통해 여러 서비스를 할 수 있다.
  + 비전문가가 사용하기에 편리하다(네이버, 다음 블로그 등).
  + 유지보수에 용이하다.
+ 단점
  + 느리다(사용자가 요청하면 데이터베이스 서버에서 데이터를 가공해야 함).
  + 비싸다(추가적으로 앱 서버를 두어야 함).

다시 Jekyll 이야기로 돌아가서, 왜 정적 웹 페이지 이야기가 나왔느냐 하면, Github Pages는 정적 웹 페이지만 호스팅 할 수 있는데, 이는 `정적 웹 페이지 생성기`인 Jekyll과 아주 잘 어울린다! ~~사실 뭐가 먼전지는 잘 모르겠다~~ ~~닭vs달걀~~ 그리고 다음 키워드는 바로.. `Ruby`다.

#### Ruby?

이름부터 예쁜 이 언어는.. 일본인이 만들었다! ~~이제 이시국 끝나서 써도됨~~  
아무튼 파이썬에서 우리가
```
pip install
```
을 사용하는 것처럼, 루비에서도 비슷한 명령어가 있는데,
```
gem install
```
이다! 일단 루비부터 설치하고 차근차근 따라해보자. 윈도우를 기준으로 설명하도록 할 텐데, 맥은.. ~~지영이가?~~ 

#### Ruby 설치하기
[Ruby Installer 공식 페이지](https://rubyinstaller.org/)  
일단 위의 페이지로 들어가서 빨갛고 커다란 Download를 누르면 다음과 같은 창이 뜰 것이다.  
![RubyInstaller](../softwarehighschool/statics/classdata/jekyll/rubyinstaller.PNG)  
우리가 사용할 버전은 2.6.6-1이고, 대단히 친절하게도 두꺼운 글씨로 되어 있다.
혹여 그럴 사람은 없겠지만 32비트 윈도우를 사용 중이라면 바로 아래에 있는 x86을 받아서 설치하면 된다. 설치파일을 다운로드 받은 후 실행시켜 보자.

![rubyinstall1](../softwarehighschool/statics/classdata/jekyll/rubyinstall1.png)  
![rubyinstall2](../softwarehighschool/statics/classdata/jekyll/rubyinstall2.png)  
설치 중 위의 사진처럼 체크해주고 설치를 진행하면 된다. 두 번째 사진의 경우 딱히 쓸 일은 없지만, 혹시를 위해 설치해둔다고 생각하면 편하다. 설치에 시간이 좀 소요되는데, 물이라도 한 잔 마시면서 기다리도록 하자.

모두 설치가 되었다면, 다음과 같은 창이 뜰 것이다.  
![rubyinstall3](../softwarehighschool/statics/classdata/jekyll/rubyinstall3.png)  
여기서 Finish를 눌러주면

![rubyinstall4](../softwarehighschool/statics/classdata/jekyll/rubyinstall4.png)  
위와 같은 창이 뜨는데, unsure하기 때문에 1,3 을 치고 Enter를 눌러주면 파일이 설치가 되고,
다 됐을 때 엔터를 한 번 더 누르면 터미널 창이 꺼지게 된다. 그리고 파이참을 재시작 후, 터미널 창에서
```
ruby -v
```
를 치면 현재 설치된 `ruby`의 버전이 나오게 된다. 현재 설치된 버전을 확인해보면
```
ruby -v
ruby 2.6.6p146 (2020-03-31 revision 67876) [x64-mingw32]
```
라고 나올 것이다. 위처럼 나오지 않았다면 뭔가 잘못 설치했을 확률이 높기 때문에 다시 찬찬히 확인해 보도록 하자.

일단 `jekyll` 및 기타 라이브러리들을 사용하기 위해 몇 가지를 Terminal 창에서 install 해주자.
```
gem install jekyll
gem install jekyll-feed
gem install bundle
gem install github-pages
gem install tzinfo-data
``` 
처음부터 블로그를 만들기는 대단히 어려운 작업이기 때문에, 다음 사이트들을 참고하여 마음에 드는 테마를 구하자.
하지만 이 문서에서는 편의를 위해 완성되어 있는 블로그를 사용할 것이다.

[https://github.com/topics/jekyll-theme](https://github.com/topics/jekyll-theme)  
[http://jekyllthemes.org/](http://jekyllthemes.org/)  
[https://jekyllthemes.io/free](https://jekyllthemes.io/free)  
[http://themes.jekyllrc.org/](http://themes.jekyllrc.org/)  
Minima, Clean Blog 등 유명한 테마들이 포함되어 있다. Jekyll은 구글에 자료가 많은 편이므로, 구글링을 통해 각 테마를 사용하는 법을 익히도록 하자.

#### 완성된 블로그 베끼기(!)
우리가 참고할 [블로그 주소](https://theorydb.github.io/)이고,  
[블로그 깃헙 주소](https://github.com/theorydb/theorydb.github.io)를 눌러보자.

![githubfork](../softwarehighschool/statics/classdata/jekyll/githubfork.png)  
fork를 누르고, 나의 repository를 선택해주면 나의 repository에 fork된다. 그 후, fork한 나의 repository에 들어가서 톱니바퀴 모양을 눌러 설정 창으로 들어가자. 다음과 같은 창이 나올 것이다.  
![forksetting](../softwarehighschool/statics/classdata/jekyll/forksetting.PNG)  
빨간색 네모 친 부분(repository name)을 `username.github.io`로 바꿔주자. 본인의 username은 Joo-ra-n 이기 때문에
```
Joo-ran.github.io
```
로 설정해주었다. 그 후 오른쪽의 `Rename` 버튼을 클릭해주면 repository name이 성공적으로 변경할 수 있다. 아래쪽의 Issue 부분에만 체크해 주고, 주소창에
```
https://username.github.io
```
를 입력하면...  
![githubpages404error](../softwarehighschool/statics/classdata/jekyll/githubfork.png)  
404 에러가 뜬다! Github Pages에 리얼타임으로는 반영이 되지 않으므로 잠시 기다려 주도록 하자. 잠시 기다린 후 다시 주소를 쳐보면..

![githubpageswelldone](../softwarehighschool/statics/classdata/jekyll/githubpageswelldone.png)  
원래의 블로그를 잘 베껴온 모습이다. 이로써 내용물은 남의 것이지만, 어쨌든 내 username으로 된 블로그가 하나 생겼다. 이제 이 블로그를 내 입맛에 맞게 조금씩 바꾸어나가는 작업을 하게 될 것이다.. 

이제 이 베껴온 블로그를 로컬에서 편집하기 위해 Pycharm을 켜고, terminal에 다음과 같이 입력해주자.
```
git clone https://github.com/"username".github.io // 본인 repository를 로컬로 clone
...
cd "username".github.io                           // "username".github.io로 경로 변경
bundle install                                    // ???
bundle exec jekyll serve                          // jekyll 블로그 로컬서버 오픈
```
이렇게 하면 localhost 주소인 `127.0.0.1:4000`으로 아까 github pages에서 보았던 것과 같은 페이지가 열리게 된다.
앞으로 우리는 pycharm에서 파일들을 수정한 뒤, 로컬 서버에서 확인해 보고 문제가 없으면 github에 push하는 식으로 블로깅을 진행할 것이다.

ctrl+c를 눌러 일단 서버를 닫고, 무엇을 수정해야 하는 지 알아보자.

##### 1. 변경해야 하는 것
+ _featured_tags/ : 블로그 포스팅 게시판 대분류
+ _featured_categories/ : 블로그 포스팅 게시판 소분류
+ _data/ : 개발자 및 기타 정보 폴더(author.yml 파일 또한 수정 필요)
+ _config.yml : 블로그의 환경변수를 설정하는 파일. 기본적인 블로그 세팅 담당
+ README.md : github 소스 페이지에 뜨는 문서이자, About 메뉴 클릭 시 나타나는 블로그 소개글

##### 2. 변경하면 좋은 것
+ assets/ : 이미지, CSS 등을 저장한 폴더(여기에서 검색 이미지도 바꿀 수 있음)
+ _layouts/ : 포스트 외부의 틀을 정하는 폴더(페이지, 구성요소 등 UXUI 변경 시 수정 필요)
+ _includes/ : 기본 페이지 폴더(여기에선 footer를 바꿀 수 있다)
+ Gemfile.lock : Gemfile에 기록한 라이브러리를 설치 후 기록하는 파일(중복 설치 방지)
+ .gitignore : github에 올리고 싶지 않은 파일들을 적어 놓은 리스트
+ sitemap.xml : 테마의 사이트맵
+ robots.xml : 검색엔진 수집 등에 대한 정책을 명시하는 설정 파일
+ posts.md : 포스트 작성 관련 설정 파일

##### 3. 뭐가 있는지 확인만 하자
+ _posts. : 실제 글을 쓰는 폴더
+ index.html : 블로그의 메인 페이지(최초 접속 시 뜨는 페이지)
+ 404.md : 404 Not Found Error가 떴을 때 페이지

[지킬 한글화 공식 페이지](http://jekyllrb-ko.github.io/docs/structure/)를 참고해서 뭐가 있는지 보면 된다.

일단 `_featured_categories/`, `_featured_tags` 파일들을 수정해서 전체적인 블로그의 틀을 잡는 것이 좋다.
내가 블로그를 어떤 식으로 운영할 지 생각해 보고 기존의 게시판들을 갈아엎은 후에 나의 입맛에 맞게 게시판 구조를 바꾸자.
그 후 `_posts` 폴더의 포스트들을 한 개(참고용)을 제외하고 전부 삭제한 후, 일단 나만의 게시물을 하나 쓰면 된다.
다음은 본인이 시험삼아 한 번 작성해 본 것이다. 원래 있던 글 제목 양식에 맞추어 마크다운 문서 제목을 정해주면 된다.
```
2020-07-20-etcetera-myfirstpost.markdown

---  
layout: post  
title: "[기타] 나의 첫 번째 포스팅"  
subtitle: "내 블로그에 첫 번째 글을 써보자"  
categories: etcetera  
tags: 블로깅 마크다운 지킬
comments: true  
---  
  
> 원래의 블로그 글을 참고하여 나의 첫 번째 포스팅을 해보자.  

---
나의 첫 번째 블로그 글

TEST 중

```
그러면 기존의 글(남의 것)이 다 사라지고, 일단 내가 방금 쓴 글만 블로그에 있게 된다.
이제 뭔가 나만의 블로그같은 느낌이 들지 않는가? ~~아님 말고...~~

또 `_data/authors.yml` 파일을 확인해보면 내부에 social 탭이 있는데, 여기를 참조해주면 좌측 목차가 있는 곳 하단에 내 SNS를 삽입할 수도 있다.
그리고 이제 좌측 목차의 배경, 전체 배경, favicon, logo, footer 정도를 바꿔주면 꽤 그럴듯해 보이게 되는데, 이것들은 `_config.yml` 파일과, `assets` 폴더에서 관리할 수 있다.
`_config.yml` 파일을 열어보면 뭔가 주루루루루룩 나오는데 여기에 있는 영어로 된 설명을 잘 읽어보고 하나하나 바꿔보면 된다.
세세하게 설명을 해 주고 싶지만.. 개인마다 원하는 바가 조금씩 다르기 때문에 실제로 보이는 부분와 그 부분에 대응하는 코드 부분을 비교해 가면서 바꿔 보는 게 가장 좋다고 생각하는 바이다.  
![jekyllblogdone](../softwarehighschool/statics/classdata/jekyll/jekyllblogdone.png)  
(내가 만든 블로그 예시)
![opengraph](../softwarehighschool/statics/opengraph.png)  
(내가 만든 블로그 오픈그래프)

마지막으로.. DISQUS라는 API를 이용하여 포스트의 댓글 기능을 구현할 텐데, ~~고맙게도~~ 블로그 원래 주인 분께서 잘 짜 놓으셔서 처음에는 DISQUS API가 포스팅 하단에 잘 붙어 있을 것이다.
하지만 `_config.yml` 파일의 `shortname` 부분을 수정해야 진정 내 블로그에 내 DISQUS가 붙게 되는데, 이를 위해서는 DISQUS 가입과 신뢰할 수 있는 사이트 추가만 해주면 된다.
[여기](https://disqus.com/admin/settings/advanced/)를 누르고, 아래쪽 I wanna... 뭐시기를 누르면 초기 페이지 설정이 뜨는데, 거기에 trusted domain에 `"username".github.io`를 추가해 주면 DISQUS가 포스팅 하단에 잘 붙는 것을 확인할 수 있을 것이다.