---
layout: post
title: "APT: 3. Code Style"
permalink: /apt/code-style
---

이번 자료에서는 코드의 가독성을 높이는 방법에 대해서 알아보도록 하겠습니다. 대부분의 프로젝트가 파이썬을 이용할 것이기 때문에 Python 위주로 글을 작성하였습니다.

## 코드 스타일이란?

코드 스타일 (Code Style) 은 개발을 위해 코드를 작성할 때 따르는 룰이나 가이드라인입니다. 특정 코드 스타일을 따른다면, 다른 개발자의 이해를 도울 뿐만 아니라, 후에 자신이 작성한 코드를 재방문할 때 덜 헷갈리고, 또 버그가 생겨서 디버깅을 해야 할 때도 문제점을 더 빨리 찾을 수 있습니다. 특히 구글같이 많은 개발자들이 일하는 회사의 경우 혼란을 방지하기 위해 모든 개발자가 같은 체계적인 방식으로 코드를 작성하는 것이 필수적입니다. 

이러한 장점들 때문에 널리 쓰이는 모든 컴퓨터 언어는 코드 스타일들이 있습니다. 하지만, 언어에 따라 대중적으로 쓰이는 코드 스타일이 여러 개인 경우도 있습니다. 예를 들어 자바스크립트의 경우, Standard, Airbnb, Google 등의 코드 스타일이 존재합니다.

다행히, 우리가 사용할 파이썬은 대중적인 코드 스타일이 하나밖에 없습니다.

## PEP

PEP은 Python Enhancement Proposal의 준말로,  파이썬을 사용하는 개발자들에게 유용한 정보나 새로운 기능에 대해 알려주는 문서들입니다.

PEP 에는 많은 양의 문서가 있는데, 그 중에 코드 스타일에 관한 글을 **PEP8** 과 **PEP257** 입니다. PEP 8은 전반적인 코드 스타일에 관한 것이며, PEP257은 docstring이라는 파이썬 특유의 주석에 대한 스타일을 다룹니다. 두 문서 모두 파이썬의 창시자인 Guido van Rossum이 직접 쓴 글로, [대부분의 파이썬 개발자들은 PEP8을 충실하게 따릅니다.](http://sideeffect.kr/popularconvention#python)

이 문서들은 어떻게 들여쓰기를 할 지, whitespace를 어떻게 사용할 지, 어떻게 주석을 달지, 여러 줄에 코드를 어떻게 나눠쓸지 등 많은 상황에서 대한 규칙을 정해놓습니다. 그러므로, 이 두 문서는 파이썬으로 프로젝트를 시작하기 전에 적어도 한 번은 읽어보는 것을 매우 추천합니다. (추가 자료 참고)

### PEP20: The Zen of Python

사람들이 파이썬을 좋아하는 이유들 중 하는 뛰어난 가독성입니다. 정형화된 PEP8과 PEP257을 따를 시 코드가 읽기 편하기 때문입니다. 하지만 모든 코딩 스타일이 그렇듯이, 두 문서가 아무리 길어도 모든 상황에 대해서 정답을 줄 수는 없습니다. 그렇기 때문에 PEP20은 마치 십계명처럼 어떤 것이 파이썬스러운 (pythonic) 것인지 설명을 합니다.

```
아름다움이 추함보다 좋다.
명시가 암시보다 좋다.
단순함이 복잡함보다 좋다.
복잡함이 꼬인 것보다 좋다.
수평이 계층보다 좋다.
여유로운 것이 밀집한 것보다 좋다.
가독성은 중요하다.
특별한 경우라는 것은 규칙을 어겨야 할 정도로 특별한 것이 아니다.
허나 실용성은 순수성에 우선한다.
오류 앞에서 절대 침묵하지 말지어다.
명시적으로 오류를 감추려는 의도가 아니라면.
모호함을 앞에 두고, 이를 유추하겠다는 유혹을 버려라.
어떤 일에든 명확한 - 바람직하며 유일한 - 방법이 존재한다.
비록 그대가 우둔하여 그 방법이 처음에는 명확해 보이지 않을지라도.
지금 하는게 아예 안하는 것보다 낫다.
아예 안하는 것이 지금 당장보다 나을 때도 있지만.
구현 결과를 설명하기 어렵다면, 그 아이디어는 나쁘다.
구현 결과를 설명하기 쉽다면, 그 아이디어는 좋은 아이디어일 수 있다.
네임스페이스는 좋은 아이디어다 -- 마구 남용해라!
```



## Pylint

당연하게도, PEP에 명시된 모든 규칙을 기억하는 것은 어려운 일입니다. 규칙의 수도 꽤 되고, 개발을 하게 되면 코드의 가독성보다는 코드가 작동하는지 관심이 먼저 가기 마련입니다. 그렇기 때문에, 쓰여진 코드가 PEP8 을 따르는 코드인지 확인해주는 Pylint 라는 프로그램이 존재합니다. (Pylint 에서의 lint는 코드를 analyze해서 potential error를 찾는 프로그램을 총칭합니다. Pylint 역시 PEP8 외의 다른 기능도 많습니다)

### 설치

Pylint는 pip을 이용해서 간단하게 설치할 수 있습니다.

```
pip install pylint
```

### 사용하기

만약 `ASDF.py` 라는 파일이 PEP 8을 따르는지 확인하고 싶다면, 터미널에서 다음 명령어를 사용합니다.

```
pylint ASDF.py
```

실행 시 많은 양의 글이 출력될 것입니다. 파일이 PEP8을 따르지 못할 경우, 출력 초반에 다음과 비슷한 목록이 있을 것입니다.

```
C:  1, 0: Missing module docstring (missing-docstring)
W:  3, 0: Uses of a deprecated module 'string' (deprecated-module)
C:  5, 0: Invalid constant name "shift" (invalid-name)
C:  6, 0: Invalid constant name "choice" (invalid-name)
C:  7, 0: Invalid constant name "word" (invalid-name)
C:  8, 0: Invalid constant name "letters" (invalid-name)
C:  9, 0: Invalid constant name "encoded" (invalid-name)
```

이 목록은 파일 안에 코드 중 정확히 어느 부분이 잘못되었는지 알려줍니다.

첫 글자는 어떤 식의 문제인지 알려줍니다.

* **C**: Convention (관례)
* **R**: Refactor (리팩토링)
* **W**: Warning (경고)
* **E**: Error (에러)

다음 두 숫자는 문제된 코드의 장소를 알려줍니다. 예를 들어 `1, 0` 의 경우 파일의 첫 줄에서 문제가 생겼다는 것을 뜻하고, `2, 5` 의 경우 두번째 줄의 5번째 글자에서 문제가 생겼음을 뜻합니다.

그 이후의 글은 그 문제가 무엇인지 설명합니다. 짧은 글만으로 무엇이 틀렸는지 이해가 안 갈 경우, 괄호 안의 symbol을 통해 더 자세히 알아 볼 수 있습니다. 예를 들어, 첫 줄에 어떤 문제가 있는지 모르겠다면 다음 명령어를 사용합니다.

```
pylint --help-msg=missing-docstring
```

그렇다면 다음 출력이 생성됩니다.

```
:missing-docstring (C0111): *Missing docstring*
  Used when a module, function, class or method has no docstring. Some special
  methods like __init__ doesn't necessarily require a docstring. This message
  belongs to the basic checker.
```



## 결론

이번 자료에서는 파이썬의 코딩 스타일에 대해서 알아보았고, 코딩 스타일을 시행할 때 유용한 Pylint 에 대해서도 배웠습니다. 기존에 파이썬 개발을 하면서 코딩 스타일을 따르지 않은 경우, Pylint 의 에러 메시지가 과도하게 복잡해 보일 수도 있습니다. 하지만 PEP8을 따르는 것은 초반의 불편함을 감수할 만큼이 가치가 있으며, 사용하다 보면 어느새 익숙해져 있는 자신을 발견하실 수 있으실 것입니다. ^^



## 추가 자료

* The Hitchhiker's Guide to Python: Code Style: 항상 참고할 만한 웹사이트 / 책입니다.
  * [영어](http://docs.python-guide.org/en/latest/writing/style/)
  * [한글](http://python-guide-kr.readthedocs.io/ko/latest/writing/style.html)
* PEP 원본
  * [PEP8](https://www.python.org/dev/peps/pep-0008/)
  * [PEP20: The Zen of Python](https://www.python.org/dev/peps/pep-0020/)
  * [PEP257: Docstring Conventions](https://www.python.org/dev/peps/pep-0257/)
* PEP 번역본
  * [PEP8](https://bitbucket.org/sk8erchoi/peps-korean/src/767c779c164856af198a9d08d906a55b24652728/pep-0008.txt)
  * [PEP20](https://bitbucket.org/sk8erchoi/peps-korean/src/767c779c164856af198a9d08d906a55b24652728/pep-0020.txt)
* [Pylint 정식 튜토리얼](https://docs.pylint.org/en/1.9/tutorial.html)