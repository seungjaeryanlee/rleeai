---
layout: post
title: 주피터 노트북 확장 프로그램 사용하기
---

**jupyter_contrib_nbextensions**는 몇십 가지의 확장 프로그램을 모아둔 패키지입니다. 그 중에서 특히 많이 찾으실 만한 확장 프로그램들은 다음과 같습니다.



## 지원하는 확장 프로그램들

### Variable Inspector (변수 탐색기)

MATLAB을 사용하신 분들이라면 굉장히 친숙한 변수 탐색기입니다. 

![변수 탐색기 데모]({{ "/assets/20180415/variable_explorer.gif" | absolute_url }})



### Codefolding (코드 접기)

코드가 길어지면 항상 필요한 코드 접기 기능입니다.

![코드 접기 데모]({{ "/assets/20180415/codefolding_1.png" | absolute_url }})

![]({{ "/assets/20180415/codefolding_2.png" | absolute_url }})

![]({{ "/assets/20180415/codefolding_3.png" | absolute_url }})



### Collapsible Headings (섹션 접기)

주피터 노트북이 길어지다 보면 유용한 섹션 접기 기능입니다.

![섹션 접기 데모]({{ "/assets/20180415/collapsible_headings.png" | absolute_url }})



### Table of Contents (목차)

주피터 노트북이 길어졌을 때 깔끔하게 보기 좋게 만드는 목차 기능입니다.

![목차 데모]({{ "/assets/20180415/toc_demo1.gif" | absolute_url }})



## 확장 프로그램 설치하기

### 1. pip

`pip` 으로 설치를 하실 경우에는 PyPi에서 jupyter_contrib_nbextensions를 설치하면 됩니다!

```bash
pip install jupyter_contrib_nbextensions
```

그 이후에 자바스크립트와 CSS 파일들을 설치합니다.

```bash
jupyter contrib nbextension install --user
```

### 2. conda

`conda`로 설치를 하는 경우에는 `conda-forge`가 제공하는 `jupyter_contrib_nbextensions`를 설치하면 됩니다.

```bash
conda install -c conda-forge jupyter_contrib_nbextensions
```



## 확장 프로그램 사용하기

우선 주피터 노트북을 실행시킵니다. 

```bash
jupyter notebook
```

그 이후, 다음의 링크로 들어갑니다.

```
http://localhost:8888/nbextensions
```

모두 정상적으로 설치되었으면, 다음과 같은 웹페이지가 보일 겁니다.

![설정 페이지]({{ "/assets/20180415/nbextensions.png" | absolute_url }})

원하시는 확장 프로그램을 고르고 Enable을 누르면 적용이 됩니다!
