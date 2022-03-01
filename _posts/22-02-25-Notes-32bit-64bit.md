---
title: 32비트 vs 64비트
category: [Notes, Youtube]
---

> 참고 유튜브

<iframe width="560" height="315" src="https://www.youtube.com/embed/SO2Kbif4Oro" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

> 32비트, 64비트라고 할 때의 비트란?

32비트와 64비트 시스템에서 말하는 비트는 CPU 레지스터의 크기를 말한다.

레지스터의 크기가 클수록 한번에 더 커다란 데이터를 처리할 수 있다.

<br>

> 레지스터란?

CPU의 구조는 세 부분으로 나뉜다.

1. 제어장치(Control Unit)
2. 레지스터(Registers)
3. 산술/논리연산장치(Arithmetic and Logic Unit = ALU)

CPU안에서 데이터를 연산하기 위해

CPU 내부에 데이터를 저장해 둘 공간이 필요하다 → 이 공간이 레지스터다!

즉, 이 레지스터의 크기가 32비트냐 64비트냐의 차이다.

32비트 → 2의 32승 = 4G (램 용량을 4G 이상 사용할 수 없음)

64비트 → 2의 64승 

<br>

> x86, x64 아키텍처란?

32비트시스템을 x86 아키텍처,

64비트 시스템을 x64 아키텍처라고 부른다.