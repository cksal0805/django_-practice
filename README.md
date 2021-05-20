# Django Prectice

## 🐱 Django 기초 연습용 레파지토리 입니다

- 대부분의 내용은 [Django문서](https://docs.djangoproject.com/ko/3.2/intro/)와 [장고걸스튜토리얼](https://tutorial.djangogirls.org/ko/django_start_project/) 를 참고하여 작성합니다.

### 목적

서버쪽은 늘 Node를 써왔는데, Django를 잠깐 쓸일이 생겨 쓰는김에 정리해 둡니다.

### 기록

- [x] **[5/19일] Django 개념과 기본셋팅 및 서버실행**
- [x] **[5/20일] Django 모델링**

### Django란 무엇인가?

python으로 만들어진 무료 어플리케이션 프레임워크 입니다.
장점으로는 초보자 분들이 배우기 쉬운 python으로 되어있다는 점이고, 로그인, 회원가입, 인증,cors등의 반복적으로 구현해야 하는 부분은 이미 만들어졌다 라는 점에서 개발 시간을 단축 시킬 수 있을 것 같습니다.

### Django에서 가지고 가는 패턴

보통 MVC 패턴을 많이 사용합니다.(특히 대표적으로 spring)
하지만 Django는 MVT(mobile-view-templates) 기반 입니다.

## 가상환경 (Virtual environment)

장고는 가상환경에 설치해서 독립적 환경에서 개발합니다.
강제는 아닙니다. 하지만 가상환경에서 개발을 적극 권합니다.
왜? 가상환경에서 설치해야 하나? 전역적인 공간에 설치해 개발을 진행 할 경우
한 컴퓨터에서 하나의 장고 버전만을 사용할 수 있습니다. a버전에서 프로젝트를 진행하다가 다른 프로젝트에서 c버전을 사용하려고 한다면 한 컴퓨터에서 하나의 장고 버전만을 사용할 수 있기에 버전업을 시켜야 하는데 충돌이나거나 문제가 생길 수 있죠.

### Node.js 와 Django의 비교

CRUD에 집중되어있는 프로젝트라면 Django 를 사용할 것 같고,
커스터마이징이 많이 필요하다면, Node.js를 선택 할 것 같은데,
개인적으로는 js를 주 언어로 쓰는 입장에서 Node.js가 편할 것 같습니다.
속도면에서도 그렇고요.

## 가상환경 및 장고 설치 및 셋팅

mac os 기준 **prectice_venv** 이라는 이름의 가상환경 설치(이름은 마음대로)

```shell
python3 -m venv prectice_venv
```

장고 설치 (당연히 파이썬은 설치 되어있다는 가정하에)

1. 가상환경 활성화

```shell (prectice_venv는 여러분이 만든 가상환경 이름)
source prectice_venv/bin/activate
```

2. 장고 설치

```shell
pip install django~=2.0.0
```
---
🔥 **ModuleNotFoundError: No module named 'pip' 라고 떠요!!!** 🔥 

만약 ModuleNotFoundError: No module named 'pip' 라고 뜬다면,
아래와 같이 장고를 설치하는데 필요한 pip버전이 최신인지 확인하고 install을 진행

```shell
python3 -m pip install --upgrade pip
```

만약 기존에 설치했었는데 안된다면 업그레이드 하고 삭제 후 재설치 하는 과정에서 권한 문제로 pip가 삭제된 상태로 남아 이런 현상이 발생 할 수 있으므로 pypa를 통해 pip를 재설치 해줍니다.

```shell
//curl을 이용해 다운
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

//설치
python get-pip.py
```

성공적으로 됐다면?

```shell
pip3 -V // 버전 확인 버전이 잘뜨면 성공적으로 설치 된거임
```

---

## 간단한 프로젝트 만들어보기

**✍🏻 아래 모든 셋팅은 반드시 가상환경에서 진행해주세요!!!**

> 😺 **가상환경 활성화 방법**
(prectice_venv에는 여러분이 만든 가상환경 이름)
mac os (shell에서) - source prectice_venv/bin/activate
window (cmd에서) - prectice_venv\Scripts\activat

#### 1. 장고프로젝트 시작하기(골격을 만들어주는 스크립트 실행)

- mysite 는 그냥 이름임 여러분 마음대로 하면 됨
- .은 현재 디렉토리에 불러오겠다는 소리

```shell
django-admin startproject mysite .
```

성공적으로 만들어 졌다면 아래와 같은 파이썬 파일이 생길 겁니다.
저는 back폴더 안에서 위의 설치들을 모두 진행했습니다.

```bash
.
├── 📂 back
├── 📄 manage.py            # Django 프로젝트와 다양한 방법으로 상호작용 하는 커맨드라인의 유틸리티
│   ├── 📄 __ init __.py
│   ├── 📄 settings.py      # 웹사이트 설정이 있는 파일
│   ├── 📄 asgi.py
│   ├── 📄 wsgi.py
│   └── 📄 urls.py           # urlresolver가 사용하는 파일
└── ...
```

**👀 asgi, wsgi 은 뭘까?**

Django 웹 어플리케이션 서버 아키텍쳐에서는 Django 프레임워크 내부의 url과 web server가 통신합니다.

여기서 web server로 많이 사용되는 Apach HTTP Server와 Tomcat은 JAVA기반이므로 파이썬 코드를 읽을 수 없다. 그렇기 떄문에 사용할 수 있는 웹서버는 매우 한정적입니다.

성능면에서 검증되어있는 apach쪽의 웹서버를 이용하면 좋은데,

이때 최적의 솔루션이 Apach 재단의 웹 서버 뿐만 아니라 모든 웹 서버와 Python 계열의 프레임 워크가 통신할 수 있게 해주는 미들 웨어를 사용하는 것입니다. 이게 바로 asgi,wsgi 입니다.

- asgi는 web server와 프레임워크(django) 애플리케이션을 연결해 주는 python의 표준 api, wsgi와의 상위호환

- wsgi는 ASGI이전의 Python의 표준 비동기 방식 기능에 구현에 있어서 문제가 많았던 wsgi라 asgi가 나왔다.

**자세한 사항은 아래 링크 참조**
https://nitro04.blogspot.com/2020/01/django-python-asgi-wsgi-analysis-of.html

#### 2. 설정변경

- mysite/settings.py을 조금 고쳐 볼게요. 설치한 코드 에디터를 열어 파일을 열어주세요

**시간 바꾸기**

> TIME_ZONE = 'UTC' -> TIME_ZONE = 'Asia/Seoul'

**정적파일 경로 추가하기**

> STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR, 'static'

**호스트설정**

디버깅 모드에서 ALLOWED_HOSTS 변수가 빈 리스트일 경우 ['localhost', '127.0.0.1', '[::1]'] 의미가 됩니다. 즉, **로컬 호스트에서만 접속**이 가능합니다.
애플리케이션을 배포할 때 PythonAnywhere의 호스트 이름과 일치하지 않으므로 다음 설정을 아래와 같이 변경해줘야 합니다.
> ALLOWED_HOSTS = ['127.0.0.1', '.pythonanywhere.com']

**DB설정**

데이터 베이스를 생성하기 위해 아래와 같은 명령어를 입력합니다.
python부터 입력하시면 됩니다. (아래 명령어를 실행하기 위해 manage.py이 필요)

```shell
 (prectice_venv) back$ python manage.py migratepython manage.py migrate
```

#### 3. 웹서버 시작하기

python부터 입력하시면 됩니다. (아래 명령어를 실행하기 위해 manage.py이 필요)

```shell
 (prectice_venv) back$ python manage.py runserver
```

브라우저에서
http://127.0.0.1:8000/ 를 입력해 열어보세요!

```shell
Django version 3.2.3, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
[19/May/2021 23:00:19] "GET / HTTP/1.1" 200 10697
[19/May/2021 23:00:19] "GET /static/admin/css/fonts.css HTTP/1.1" 200 423
[19/May/2021 23:00:19] "GET /static/admin/fonts/Roboto-Bold-webfont.woff HTTP/1.1" 200 86184
[19/May/2021 23:00:19] "GET /static/admin/fonts/Roboto-Regular-webfont.woff HTTP/1.1" 200 85876
[19/May/2021 23:00:19] "GET /static/admin/fonts/Roboto-Light-webfont.woff HTTP/1.1" 200 85692
Not Found: /favicon.ico
```

🤩 성공!

#### 이런경우는 어떻게하죠?

**🔥 Error: That port is already in use.**
이럴 경우 port 8000과 관련된 모든 프로세스를 죽이고 다시 실행시키면 된다.

```shell
sudo lsof -t -i tcp:8000 | xargs kill -9
```

**🔥 File "manage.py", line 17 from exc SyntaxError: invalid syntax**
python manage.py runserver시에 위와 같은 문제가 생긴다면,

1.현재 가상환경내부에서 진행하고 있는지 체크한다.
> 😺 **가상환경 활성화 방법**
(prectice_venv에는 여러분이 만든 가상환경 이름)
mac os (shell에서) - source prectice_venv/bin/activate
window (cmd에서) - prectice_venv\Scripts\activat

2. 현재 사용하는 파이썬의 버전을 지정해서 실행한다.

```shell
python3 manage.py runserver
```

---------------------

### 장고모델

특징: 객체지향적 설계, 장고안에 있는 모델은 객체의 특별한 종류, 이 모델을 저장하면 그 내용이 데이터베이스에 저장됩니다.

데이터베이스는 원하는 걸로 사용하면 됩니다. 하지만 이번 레포에서는 연습용이므로 SQLite(기본 장고 데이터베이스 어댑터)를 사용하도록 하겠습니다.

#### 어플리케이션 만들기

아래와 같이 입력해주면 자동으로 파이썬 패키지가 구성됩니다.
앱의 기본 디렉터리 구조를 자동으로 생성할 수 있는 도구를 제공하기 때문에, 코드에만 더욱 집중할 수 있습니다.

```bash
  python3 manage.py startapp blog
```

그러면 아래와 같은 폴더 구조를 보실 수 있을 겁니다.

```bash
.
├── 📂 blog
│   └── 📂 migrations 
│     └──  📄 __ init __.py
│   ├── 📄 __init__.py
│   ├── 📄 admin.py
│   ├── 📄 models.py
│   ├── 📄 tests.py
│   └── 📄 views.py
└── 
```

애플리케이션을 생성 후 장고에게 사용한다고 알려주겠습니다.
**mysite/settings.py** 에서 수정해주도록 하겠습니다.
INSTALLED_APPS에 우리가 만든 앱의 폴더네임을 추가해주시면 됩니다.

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog', // 여기 추가
]
```

#### 모델

model.py파일에 모델을 정의해보도록 하겠습니다.

코드는 👉🏻 [코드로바로가기(클릭)](https://github.com/cksal0805/django_practice/blob/main/back/blog/models.py) 또는 제 레파지토리 back/blog/model.py에서 확인하시면 됩니다.

- Class로 객체정의를 해줄 수 있다.
- Class 모델이름 ->  와 같은 형식으로 모델이름을 정의 할 수 있는데, 항상 첫 글자는 대문자 여야합니다.
- models는 장고모델임을 알려줌 -> 해당 모델이 DB에 저장되어야 함을 알려줍니다.
- 속성을 정의하고 데이터 타입을 알려주어야 합니다.

```python
title = models.CharField(max_length=200)
```

- def로 메서드를 정의할 수 있습니다.

#### 테이블

장고모델에 우리가 방금 모델 만들었고, 수정했다고 알려준다.

```bash
python3 manage.py makemigrations blog
```

실제 데이터베이스에 추가한다.

```bash
python3 manage.py migrate blog

// 하면 아래와 같이 뜬다.
Operations to perform:
  Apply all migrations: blog
Running migrations:
  Applying blog.0001_initial... OK
```
