TensorFlow는 데이터 플로우 그래프(Data flow graph)를 사용하여 수치 연산을 하는 오픈소스 소프트웨어 라이브러리입니다. 
그래프의 노드(Node)는 수치 연산을 나타내고 엣지(edge)는 노드 사이를 이동하는 다차원 데이터 배열(텐서,tensor)을 나타냅니다. 
유연한 아키텍처로 구성되어 있어 코드 수정 없이 데스크탑, 서버 혹은 모바일 디바이스에서 CPU나 GPU를 사용하여 연산을 구동시킬 수 있습니다. 

TensorFlow는 원래 머신러닝과 딥뉴럴 네트워크 연구를 목적으로 구글의 인공지능 연구 조직인 구글 브레인 팀의 연구자와 엔지니어들에 의해 개발되었습니다.
하지만 이 시스템은 여러 다른 분야에도 충분히 적용될 수 있습니다. 다음 문서에서 어떻게 TensorFlow를 설치하고 사용하는지에 대해 설명하겠습니다.

TensorFlow는 안정적인 Python 및 C API를 제공하며, C++, Go, Java, JavaScript, 그리고 Swift에 사용 가능한 하위 API를 제공합니다.
announce@tensorflow.org에 가입하여 출시 공지 및 보안 업데이트를 최신으로 유지하십시오.

설치
- CPU-only 릴리즈 설치 : 

pip install tensorflow

- CUDA를 지원하는 GPU를 위한 패키지 설치 : 

pip install tensorflow-gpu

자세한 지침 및 소스에서 빌드하는 방법은 Tensor Flow 설치를 참조하십시오.
당신이 도전적인 사람이라면, nightly binaries를 사용해보세요:

Nightly pip packages*
TensorFlow 가 PyPi의 tf-nightly-gpu 프로젝트를 통해 nightly pip 패키지를 제공할 수 있어서 기쁩니다. 
TensorFlow nightly 버전을 설치하기 위해서, pip install tf-nightly 을 실행하거나, pip install tf-nightly-gpu 를 실행하세요. 
Linux, Mac, Windows를 지원하는 CPU, GPU 패키지를 제공합니다.

첫 번째 TensorFlow 프로그램을 사용해보십시오.

$ python
>>> import tensorflow as tf
>>> tf.enable_eager_execution()
>>> tf.add(1, 2).numpy()
3
>>> hello = tf.constant('Hello, TensorFlow!')
>>> hello.numpy()
'Hello, TensorFlow!'


tensorflow.org의 튜토리얼 페이지에서 텐서플로우의 다양한 예제를 살펴보십시오.

기여 가이드라인
TensorFlow에 기여하고 싶다면, 기여 가이드라인을 반드시 확인하십시오. 이 프로젝트는 텐서플로우의 가이드라인을 준수합니다. 참여한다면, 
이 가이드라인을 준수해야 합니다.
요청 및 버그 제보에는 Git Hub의 issues 게시판을 이용합니다. 일반적인 질문이 있다면 
먼저 TensorFlow Discuss에서 자주 묻는 질문과 답변을 확인하고, 구체적인 질문을 
Stack Overflow에 올려주세요.
TensorFlow 프로젝트는 오픈소스 소프트웨어 개발의 모범이 되기 위해 노력합니다.

연속적인 빌드 상태

공식 빌드

Build Type	                   Status	                                 Artifacts
Linux CPU	                     ubuntu CC passing	                     pypi
Linux GPU                      ubuntu GPU PY3 passing	                 pypi
Linux XLA	                     ubuntu XLA falling	                     TBA
MacOS	                         MacOS PY2 CC passing                    pypi
Windows CPU	                   Windows CPU passing                     pypi
Windows GPU	                   Windows GPU falling	                   pypi
Android	                       Android passing	                       Download 1.13.1
Raspberry Pi 0 and 1	         Rpi01 py2 passing Rpi01 py3 passing	   Py2 Py3
Raspberry Pi 2 and 3	         rpi23 py2 passing Rpi23 py3 passing	   Py2 Py3

커뮤니티 지원 빌드

          Build Type	                         Status	                     Artifacts
          
IBM s390x	                                 Build running                   TBA
Linux ppc64le CPU Nightly	                 Build running	                 Nightly
Linux ppc64le CPU Stable Release	         Build passing	                 Release
Linux ppc64le GPU Nightly	                 Build passing	                 Nightly
Linux ppc64le GPU Stable Release	         Build passing                   Release
Linux CPU with Intel® MKL-DNN Nightly	     Build running	                 Nightly
Linux CPU with Intel® MKL-DNN 
Supports Python 2.7, 3.4, 3.5, and 3.6	   Build disabled	                 1.13.1 pypi
Red Hat® Enterprise Linux® 7.6 CPU & GPU 
Python 2.7, 3.6	                           Build passing	                 1.13.1 pypi

더 많은 정보에 대해서

ㆍTensorFlow Website
ㆍTensorFlow Tutorials
ㆍTensorFlow Model Zoo
ㆍTensorFlow Twitter
ㆍTensorFlow Blog
ㆍTensorFlow Course at Stanford
ㆍTensorFlow Roadmap
ㆍTensorFlow White Papers
ㆍTensorFlow YouTube Channel
ㆍTensorFlow Visualization Toolkit

tensorflow.org 커뮤니티 페이지에서 TensorFlow 커뮤니티에 대한 자세한 내용을 알아보십시오.

라이선스

Apache License 2.0
