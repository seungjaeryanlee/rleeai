---
layout: post
title: 주피터 노트북 코드 프로파일링 1
---

## 코드 프로파일링이란?

코드를 짤 때 제품의 완성도도 중요하지만, 제품이 얼마나 시간과 메모리를 소모하는지도 중요할 때가 많습니다. 코드 프로파일링 (성능 분석)은 코드를 최적화하기 위해 함수 호출 주기와 빈도, 시간과 메모리 소요 등을 측정하는 것을 뜻합니다.

이러한 작업을 돕는 프로그램을 프로파일러 (profiler)라고 합니다. 이 포스트에서는 주피터 노트북에서 기본적으로 제공하는 `%time` , ` %timeit` , `%prun` 에 대해 알아보도록 하겠습니다.

## %time

`%time`은 한 줄의 코드의 실행시간을 측정할 때 쓸 수 있습니다. 단순히 측정할 줄 앞에 `%time`을 붙이면 됩니다. 

예를 들어, 아래의 셀을 실행하면,

```python
%time import tensorflow
```

다음과 같은 출력을 합니다.

```
CPU times: user 1.7 s, sys: 524 ms, total: 2.22 s
Wall time: 9.95 s
```

## %timeit

`%timeit`은 코드의 소요시간을 여러 번 측정해 좀 더 정확히 파악할 때 쓰입니다. `%time`과 똑같이, 측정하려는 줄 앞에 `%timeit` 을 덧붙이기만 하면 됩니다.

```python
%timeit None is None
```

이런 출력을 받습니다.

```
17.9 ns ± 0.27 ns per loop (mean ± std. dev. of 7 runs, 10000000 loops each)
```

즉, `None is None`의 실행 시간은 평균 17.9 ns 이며, 표준편차는 0.27 ns 입니다.

`%timeit`은 한 줄의 소요시간을 측정할 때, 그 줄을 $n$번 실행시켜서 $a$라는 평균을 얻습니다. 그 방식을 $r$ 번 반복해서, 평균값들 $\{a_1, a_2, \ldots a_r\}$을 측정하고, 이 평균값을 토대로 평균과 표준편차를 계산합니다.

`%timeit`은 그 줄의 소요시간에 따라 $n$과 $r$을 조정합니다. 예를 들어,

```python
%timeit 2**100000
```

을 실행할 경우,

```
291 µs ± 26.5 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
```

위와 같이 $r = 7, n = 1000$ 으로 설정합니다.

만약 좀 더 정확한 측정을 위해 $r$과 $n$의 값을 조정하고 싶다면, `-n`과 `-r` 플래그로 간단히 조정할 수 있습니다.

```
%timeit -r 1 -n 1 2**100000
```

마지막으로, 만약 한 줄이 아니라 셀 전체의 코드의 시간을 측정하고 싶으면, 셀의 첫 줄에 `%%timeit`을 추가하면 됩니다.

```
%%timeit
circular_ref = circular_ref[0] = [0]
assert circular_ref == circular_ref[0][0][0][0][0][0][0]
```

## %prun

`%prun`은 단순히 시간을 측정하는 `%time` , `%timeit` 과는 달리, 함수를 실행시킬 때 어느 부분에서 시간이 가장 많이 소요되었는지 출력하는 커맨드입니다. 예를 들어, 다음과 같은 함수에 `%prun`을 실행시키면

```
from time import sleep

def wait_one_second():
    sleep(1)
def wait_half_second():
    sleep(0.5)

def prun_example():
    wait_one_second()
    wait_one_second()
    wait_half_second()

%prun prun_example()
```
아래와 같은 표를 볼 수 있습니다.

```
         10 function calls in 2.503 seconds

   Ordered by: internal time

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        3    2.503    0.834    2.503    0.834 {built-in method time.sleep}
        1    0.000    0.000    2.503    2.503 {built-in method builtins.exec}
        1    0.000    0.000    2.503    2.503 <ipython-input-4-xx>:8(prun_example)
        2    0.000    0.000    2.002    1.001 <ipython-input-4-xx>:3(wait_one_second)
        1    0.000    0.000    0.501    0.501 <ipython-input-4-xx>:5(wait_half_second)
        1    0.000    0.000    2.503    2.503 <string>:1(<module>)
        1    0.000    0.000    0.000    0.000 {method 'disable' of '_lsprof.Profiler' objects}
```

여기서 각각의 열은 다음을 의미합니다.

* **ncalls** - 함수가 호출된 횟수.
* **tottime** - 이 함수 내에서 소요된 시간. 다른 함수를 호출하면 그 함수의 시간은 포함하지 않음. (초 단위)
* **percall** - tottime을 ncalls로 나눈 값.
* **cumtime** - 이 함수 내에서 소요된 시간. 다른 함수를 호출할 때 그 함수 내에서 소요된 시간을 포함함. (초 단위)
* **percall** - cumtime을 ncalls로 나눈 값.

## 추가

만약 `%time` , `%timeit` , `%prun`에 대해서 더 알고 싶다면, 주피터 노트북 내에서

```
%time?
%timeit?
%prun?
```

을 실행하면 각각의 커맨드에 대한 설명서가 나타납니다.
