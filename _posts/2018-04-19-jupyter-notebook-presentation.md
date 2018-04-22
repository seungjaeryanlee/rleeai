---
layout: post
title: 주피터 노트북으로 발표하기 (nbconvert, RISE)
category: jupyter
---

## 주피터 nbconvert

주피터 노트북은 코드를 짜는데 최적화되어 있는 참 고마운 앱입니다. 그런데 작성한 코드로 발표할 때는 글씨가 너무 작고 필요없는 내용이 많아 스크롤을 계속 해야 돼서 상당히 불편합니다. 그래서 주피터가 만든 것이 **nbconvert** 로, 주피터 ipynb 노트북을 그대로 슬라이드 형태로 바꿔주는 프로그램입니다. 



## nbconvert 사용하기

### 1. 슬라이드쇼 구성하기

![슬라이드쇼 툴바]({{ "assets/20180419/slideshow_toolbar.png" | absolute_url }})

우선 메뉴에서 View > Cell Toolbar > Slideshow 를 찾아서 클릭합니다.

![]({{ "assets/20180419/slide_type.png" | absolute_url }})

그러면 각각의 셀마다 **Slide Type**을 설정할 수 있습니다. 총 다섯 가지가 있는데, 각각은 다음을 의미합니다.

* Slide, Sub-Slide, Fragment
  * 내용이 어떻게 슬라이드에 보여지는지 좌우합니다.
* Skip
  * 슬라이드에 보이지 않습니다.
* Notes
  * 발표자를 위한 노트로, 슬라이드에 보이지 않습니다.

예를 들어, 아래와 같이 슬라이드를 구성하면:

![슬라이드 구성 예제]({{ "assets/20180419/slide_type_ex.png" | absolute_url }})

다음과 같이 슬라이드쇼가 만들어집니다.

![슬라이드쇼 예제]({{ "assets/20180419/slideshow_use.gif" | absolute_url }})



### 2. 슬라이드쇼 보기

이제 아래 코드를 통해 슬라이드쇼를 볼 수 있습니다.

**주의**: CDN을 쓰기 때문에 인터넷에 연결되어 있어야 합니다.

```bash
jupyter nbconvert Hello,_Colaboratory.ipynb --to slides --post serve
```



## RISE

RISE는 Reveal.js IPython Slideshow Extension의 준말로, nbconvert를 더 편하게 쓸 수 있게 만들어주는 확장 프로그램입니다.

RISE의 장점은 두 가지입니다.

* 주피터 노트북 안에서 슬라이드 쇼 모드로 바로 변경 가능
* 슬라이드 쇼 내에서 코드 실행 가능

![RISE 데모]({{ "assets/20180419/rise.gif" | absolute_url }})



## RISE 설치하기

**주의**: RISE는 기본적으로 확장 프로그램이라서 확장 프로그램 툴을 설치해야 합니다. 확장 프로그램 설치법은 [이 포스트](http://www.rlee.ai/2018/04/15/jupyter-notebook-exntesions/)를 참고하시기 바랍니다.

### 1. pip

우선 `pip`으로 PyPI 에서 RISE를 설치합니다.

```bash
pip install RISE
```

그 다음에 자바스크립트와 CSS 파일을 설치합니다.

```bash
jupyter-nbextension install rise --py --sys-prefix
```

마지막으로 설치를 마친 RISE를 enable합니다.

```
jupyter-nbextension enable rise --py --sys-prefix
```

### 2. conda (추천)

RISE의 제작자가 추천하는 설치방식입니다.  아래처럼 `damianavila82` 채널에서 rise를 설치합니다.

```bash
conda install -c damianavila82 rise
```



## RISE 사용하기

주피터 노트북 안에서 **Alt +R** 단축키로 슬라이드 쇼 모드로 바꿀 수 있습니다.



## 추가 리소스

[nbconvert 영어 가이드](https://nbconvert.readthedocs.io)

[nbconvert 깃헙](https://github.com/jupyter/nbconvert)

[RISE 영어 가이드](https://damianavila.github.io/RISE/)

[RISE 깃헙](https://github.com/damianavila/RISE)