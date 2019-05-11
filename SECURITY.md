TensorFlow를 안전하게 사용하기
이 문서는 신뢰할 수없는 프로그램 (모델 또는 모델 매개 변수)을 안전하게 처리하고 데이터를 입력하는 방법을 설명합니다. 
아래에서는 TensorFlow의 취약점을 보고하는 방법에 대한 지침도 제공합니다.


TensorFlow 모델은 프로그램
TensorFlow의 런 타임 시스템은 프로그램을 해석하고 실행합니다. 어떤 기계 학습 종사자 용어 모델은 TensorFlow가 실행하는 프로그램으로 표현됩니다. 
TensorFlow 프로그램은 계산 그래프로 인코딩됩니다. 모델의 매개 변수는 종종 체크 포인트에 별도로 저장됩니다.

런 타임에 TensorFlow는 제공된 매개 변수를 사용하여 계산 그래프를 실행합니다. 제공되는 매개 변수에 따라 계산 그래프의 동작이 달라질 수 있습니다. 
TensorFlow 자체는 샌드 박스가 아닙니다. 계산 그래프를 실행할 때 TensorFlow는 파일을 읽고 쓰고 네트워크를 통해 데이터를 주고받으며 추가 프로세스를 
생성 할 수 있습니다. 이러한 모든 작업은 TensorFlow 프로세스의 권한으로 수행됩니다. 이러한 유연성을 허용하면 강력한 기계 학습 플랫폼이 되지만 보안에
영향을 미칩니다.

계산 그래프는 또한 입력을 받아들일 수 있습니다. 이러한 입력은 TensorFlow에 제공하여 모델을 교육하는 데 사용하는 데이터이거나 모델을 사용하여 
데이터에 대한 추론을 실행하는 데 사용됩니다.

TensorFlow 모델은 프로그램이므로 보안 측면에서 다루어야합니다.


신뢰할 수없는 모델 실행
일반적으로 샌드 박스 (예 : nsjail)에서 항상 신뢰할 수없는 모델을 실행합니다.

모델이 신뢰할 수 없게 되는 여러 가지 방법이 있습니다. 확실하게, 신뢰할 수 없는 부분이 TensorFlow 커널을 제공하면 임의의 코드가 실행될 수 있습니다. 
신뢰할 수없는 사용자가 TensorFlow 그래프를 생성하는 Python 코드와 같이 Python 코드를 제공하는 경우에도 마찬가지입니다.

신뢰할 수없는 당사자만이 일련화된 계산그래프 (GraphDef, SavedModel 또는 이와 유사한 디스크 형식)를 제공하더라도 TensorFlow에서 사용할 수 있는 
계산 프리미티브 집합은 강력하기 때문에 TensorFlow 프로세스가 효율적으로 임의적으로 실행된다고 가정해야합니다 암호. 하나의 일반적인 해결책은 몇 가지
안전 작업만을 허용 목록으로 만드는 것입니다. 이것은 이론상 가능하지만 실행을 샌드 박싱하는 것이 좋습니다.

사용자가 검사 점을 제공했는지 여부는 계산 그래프에 따라 다릅니다. 악의적인 검사 점이 안전하지 않은 동작을 유발할 수 있는 계산 그래프를 쉽게 만들 수
있습니다. 예를 들어, tf.Variable의 값에 따라 tf.cond를 포함하는 그래프를 생각해보십시오. tf.cond의 한 지점은 무해하지만 다른 지점은 안전하지 
않습니다. tf.Variable이 검사 점에 저장되었으므로 검사 점을 제공하는 사람은 이제 그래프가 제어 할 수 없더라도 안전하지 않은 동작을 트리거 할 수 
있습니다. 즉, 그래프에는 자체의 취약점이 포함될 수 있습니다. 사용자가 자신을 대신하여 실행하는 모델에 체크 포인트를 제공 할 수 있게 하려면 
(예 : 고정 모델 아키텍처의 모델 품질을 비교하기 위해) 모델을 신중하게 감사해야하며 TensorFlow 프로세스를 샌드 박스에서 실행하는 것이 좋습니다.


신뢰할 수없는 입력 수락
버그가 없다고 가정 할 때 신뢰할 수없는 입력을 안전하게 처리 할 수 ​​있다는 의미에서 안전한 모델을 작성할 수 있습니다. 
이 문제에 의존하지 않는 두 가지 주된 이유가 있습니다. 첫째, 신뢰할 수없는 입력에 노출되어서는 안 되는 모델을 작성하기 쉽고 
둘째, 소프트웨어 시스템에 충분한 복잡성이 있는 버그가 있습니다. 사용자가 입력을 제어하게하면 TensorFlow 또는 종속 라이브러리에서 
버그를 유발할 수 있습니다.

일반적으로 신뢰할 수없는 (예 : 사용자가 제공한) 입력에 노출 된 시스템의 부분을 샌드 박스로 격리하는 것이 좋습니다.

TensorFlow 그래프가 실행되는 방법에 대한 유용한 비유는 Python과 같은 해석 된 프로그래밍 언어입니다. 사용자가 입력 한 내용에 노출 될 수 있는 
보안 Python코드를 작성할 수는 있지만 (예 : 입력 문자열, 입력 블롭 등의 크기를 신중하게 인용 및 소실), 안전하지 않은 Python 프로그램을 작성하는 
것은 매우 쉽습니다 . 심지어 안전한 Python코드는 Python 인터프리터의 버그 또는 사용 된 Python 라이브러리의 버그로 안전하지 않게 될 수 있습니다.


TensorFlow 서버 실행
TensorFlow는 분산 컴퓨팅을 위한 플랫폼이므로 TensorFlow 서버 (tf.train.Server)가 있습니다. TensorFlow 서버는 내부 통신전용입니다. 
신뢰할 수없는 네트워크에서는 사용할 수 없습니다.

성능상의 이유로 기본 TensorFlow 서버는 인증 프로토콜을 포함하지 않고 암호화되지 않은 메시지를 보냅니다. 그것은 어디서나 연결을 받아들이고, 
검사를 수행하지 않고 전송 된 그래프를 실행합니다. 따라서 네트워크에서 tf.train.Server를 실행하면 네트워크에 액세스 할 수 있는 사람은 
tf.train.Server를 실행하는 프로세스의 권한으로 임의 코드를 고려해야하는 것을 실행할 수 있습니다.

분산 된 TensorFlow를 실행할 때는 클러스터가 있는 네트워크를 격리해야합니다. 클라우드 제공 업체는 격리 된 네트워크를 설정하기 위한 지침을 제공합니다.
이 네트워크는 때때로 "가상 사설 클라우드"로 분류됩니다. 자세한 내용은 GCP 및 AWS 지침 참조).

tf.train.Server는 tensorflow / serving (ModelServer라는 기본 바이너리)에 의해 생성 된 서버와 다릅니다. 기본적으로 ModelServer에는 인증을 위한 
기본 제공 메커니즘이 없습니다. 신뢰할 수없는 네트워크에 연결하면이 네트워크의 모든 사용자가 ModelServer에 알려진 그래프를 실행할 수 있습니다. 
즉, 공격자가 위에서 설명한 것처럼 신뢰할 수없는 입력을 사용하여 그래프를 실행할 수는 있지만 임의의 그래프를 실행할 수는 없습니다. ModelServer가 
신뢰할 수없는 네트워크에 직접 노출 될 수는 있지만, 사용하기 위해 구성된 그래프가 신중하게 감사되어 안전하게 보호 될 수 있습니다.

다른 서버의 모범 사례와 마찬가지로 적절한 권한 (즉, 사용 권한이 낮은 별도의 사용자 사용)으로 ModelServer를 실행하는 것이 좋습니다. 
방위의 정신으로는 신뢰할 수없는 네트워크에 연결된 TensorFlow 서버에 대한 요청을 인증하고 침입으로 인한 악영향을 최소화하기 위해 서버를 샌드 
박싱하는 것이 좋습니다.


TensorFlow의 취약점
TensorFlow는 크고 복잡한 시스템입니다. 또한 타사 라이브러리 (예 : numpy, libjpeg-turbo, PNG 파서, protobuf)의 대규모 세트에 따라 다릅니다. 
TensorFlow 또는 그 종속 라이브러리에 특수하게 조작 된 입력이 예기치 않게 또는 위험한 동작을 유발할 수 있는 취약점이 있을 수 있습니다.


취약점이란 무엇입니까?
TensorFlow의 유연성을 감안할 때 예기치 않은 동작이나 원치 않는 동작을 나타내는 계산 그래프를 지정할 수 있습니다. TensorFlow 모델이 임의의 계산을 
수행 할 수 있다는 사실은 파일 읽기 및 쓰기, 네트워크를 통한 통신, 교착 상태 및 무한 루프 생성 또는 메모리 부족 등을 의미합니다. 
이러한 동작이 관련된 동작의 사양을 벗어난 경우에만 이러한 동작이 취약점이됩니다.

파일을 쓰는 FileWriter는 예기치 않은 동작이 아니므로 TensorFlow의 취약점이 아닙니다. 임의의 바이너리 코드 실행을 허용하는 MatMul은 취약점입니다.

이것은 시스템 관점에서 보면 더 미묘합니다. 예를 들어, TensorFlow 프로세스가 잘못된 tf.tile 작업을 포함하는 계산 그래프를 지정하여 사용 가능한 
것보다 많은 메모리를 할당하도록하는 것은 쉽습니다. 이 경우에는 TensorFlow가 정상적으로 종료되어야합니다 (Python에서 예외를 발생 시키거나 
C ++에서 오류 상태를 반환합니다). 그러나 주변 시스템이 가능성을 기대하지 않는다면 이러한 행위는 서비스 거부 공격 (또는 악화)에서 사용될 수 있습니다.
TensorFlow가 올바르게 작동하기 때문에 TensorFlow의 취약점은 아닙니다 (이 가상 시스템의 취약점 일 수 있음).

일반적으로 Tensorflow가 소유하지 않은 메모리에 액세스하거나 더러운 방식으로 종료하는 것은 잘못된 동작입니다. 그러한 행동을 유도하는 TensorFlow의 
버그는 취약점을 구성합니다.

모든 시스템에서 가장 중요한 부분 중 하나는 입력 처리입니다. 악의적 인 입력이 부작용이나 잘못된 행동을 유발할 수있는 경우 이것은 버그이며 
취약성 일 가능성이 있습니다.


취약점보고
security@tensorflow.org로 메일을 보내주십시오. 이 메일은 소규모 보안 팀에 전달됩니다. 귀하의 이메일은 업무 일 기준 1 일 이내에 승인되며 
7 일 이내에 귀하의 이메일에 대한보다 자세한 응답을 보내 보고서 처리의 다음 단계를 알려줍니다. 중요한 문제의 경우 보고서를 암호화 할 수 있습니다 
(아래 참조).

보고서 이메일을 설명하는 제목을 사용하십시오. 보고서에 처음 회신 한 후 보안 팀은 수정 사항 및 공지 사항에 대한 진행 상황을 지속적으로 
알려 드리기 위해 노력할 것입니다.

또한 보고서와 함께 다음 정보를 함께 보내주십시오.

ㆍ귀하의 성명 및 소속 (있는 경우).
ㆍ취약점에 대한 기술적 인 세부 사항에 대한 설명. 결과를 재현 할 수있는 방법을 알려주는 것이 중요합니다.
ㆍ이 취약점을 악용 할 수 있는 사람과 이를 수행 할 때 얻게 되는 것에 대한 설명은 공격 시나리오를 작성합니다. 이렇게 하면 문제가 복잡한 경우 
특히 신속하게 보고서를 평가하는 데 도움이 됩니다.
ㆍ이 취약점이 공개되었거나 제 3 자에게 알려진 것인지 여부 그렇다면 세부 정보를 제공해주십시오.
기존 (공개) 문제가 보안과 관련 있다고 생각되면 security@tensorflow.org로 전자 메일을 보내주십시오. 전자 메일에는 문제 ID와이 보안 정책에 
따라 처리해야하는 이유에 대한 간략한 설명이 포함되어야합니다.

문제가 보고되면 TensorFlow는 다음 공개 프로세스를 사용합니다.

ㆍ보고서를 받으면 문제를 확인하고 심각도를 결정합니다.
ㆍ게시하기 전에 완화가 필요한 TensorFlow를 기반으로 하는 특정 타사 서비스 또는 소프트웨어를 알면 해당 프로젝트에 알림이 전송됩니다.
ㆍ완화를 위한 문제와 단계에 대해 자세히 설명하는 권고가 준비되어 있지만 게시되지는 않았습니다.
ㆍ가능하면 최신 2 개의 주요 릴리스와 마스터 분기의 마지막 마이너 릴리스에 대한 수정이 준비되어 있습니다. 우리는 가능하면 가깝게 
가능한 빨리 수정을 시도합니다.
ㆍ패치 릴리스는 모든 정식 릴리스 버전에 대해 게시되며, discuss@tensorflow.org로 통지가 전송되고 권고가 게시됩니다.

 지난 보안 권고가 아래에 나열되어 있습니다. 귀하가 요청할 경우 귀하의 이름을 기밀로 유지하기는 하지만, 보안 문제를 확인하기 위해 
기여자를 선정합니다.

security@tensorflow.org의 암호화키

공개가 매우 민감한 경우 아래 키를 사용하여 보고서를 암호화하도록 선택할 수 있습니다. 치명적인 보안 보고서에만 사용하십시오.

-----BEGIN PGP PUBLIC KEY BLOCK-----

mQENBFpqdzwBCADTeAHLNEe9Vm77AxhmGP+CdjlY84O6DouOCDSq00zFYdIU/7aI
LjYwhEmDEvLnRCYeFGdIHVtW9YrVktqYE9HXVQC7nULU6U6cvkQbwHCdrjaDaylP
aJUXkNrrxibhx9YYdy465CfusAaZ0aM+T9DpcZg98SmsSml/HAiiY4mbg/yNVdPs
SEp/Ui4zdIBNNs6at2gGZrd4qWhdM0MqGJlehqdeUKRICE/mdedXwsWLM8AfEA0e
OeTVhZ+EtYCypiF4fVl/NsqJ/zhBJpCx/1FBI1Uf/lu2TE4eOS1FgmIqb2j4T+jY
e+4C8kGB405PAC0n50YpOrOs6k7fiQDjYmbNABEBAAG0LVRlbnNvckZsb3cgU2Vj
dXJpdHkgPHNlY3VyaXR5QHRlbnNvcmZsb3cub3JnPokBTgQTAQgAOBYhBEkvXzHm
gOJBnwP4Wxnef3wVoM2yBQJaanc8AhsDBQsJCAcCBhUKCQgLAgQWAgMBAh4BAheA
AAoJEBnef3wVoM2yNlkIAICqetv33MD9W6mPAXH3eon+KJoeHQHYOuwWfYkUF6CC
o+X2dlPqBSqMG3bFuTrrcwjr9w1V8HkNuzzOJvCm1CJVKaxMzPuXhBq5+DeT67+a
T/wK1L2R1bF0gs7Pp40W3np8iAFEh8sgqtxXvLGJLGDZ1Lnfdprg3HciqaVAiTum
HBFwszszZZ1wAnKJs5KVteFN7GSSng3qBcj0E0ql2nPGEqCVh+6RG/TU5C8gEsEf
3DX768M4okmFDKTzLNBm+l08kkBFt+P43rNK8dyC4PXk7yJa93SmS/dlK6DZ16Yw
2FS1StiZSVqygTW59rM5XNwdhKVXy2mf/RtNSr84gSi5AQ0EWmp3PAEIALInfBLR
N6fAUGPFj+K3za3PeD0fWDijlC9f4Ety/icwWPkOBdYVBn0atzI21thPRbfuUxfe
zr76xNNrtRRlbDSAChA1J5T86EflowcQor8dNC6fS+oHFCGeUjfEAm16P6mGTo0p
osdG2XnnTHOOEFbEUeWOwR/zT0QRaGGknoy2pc4doWcJptqJIdTl1K8xyBieik/b
nSoClqQdZJa4XA3H9G+F4NmoZGEguC5GGb2P9NHYAJ3MLHBHywZip8g9oojIwda+
OCLL4UPEZ89cl0EyhXM0nIAmGn3Chdjfu3ebF0SeuToGN8E1goUs3qSE77ZdzIsR
BzZSDFrgmZH+uP0AEQEAAYkBNgQYAQgAIBYhBEkvXzHmgOJBnwP4Wxnef3wVoM2y
BQJaanc8AhsMAAoJEBnef3wVoM2yX4wIALcYZbQhSEzCsTl56UHofze6C3QuFQIH
J4MIKrkTfwiHlCujv7GASGU2Vtis5YEyOoMidUVLlwnebE388MmaJYRm0fhYq6lP
A3vnOCcczy1tbo846bRdv012zdUA+wY+mOITdOoUjAhYulUR0kiA2UdLSfYzbWwy
7Obq96Jb/cPRxk8jKUu2rqC/KDrkFDtAtjdIHh6nbbQhFuaRuWntISZgpIJxd8Bt
Gwi0imUVd9m9wZGuTbDGi6YTNk0GPpX5OMF5hjtM/objzTihSw9UN+65Y/oSQM81
v//Fw6ZeY+HmRDFdirjD7wXtIuER4vqCryIqR6Xe9X8oJXz9L/Jhslc=
=CDME
-----END PGP PUBLIC KEY BLOCK-----



알려진 취약점
TensorFlow의 알려진 취약점 및 보안 권고 목록을 보려면 여기를 클릭하십시오.

=======================================================================================================================

tensorflow/tensorflow/security/index.md


TensorFlow 보안 권고
우리는 정기적으로 TensorFlow 사용에 관한 보안 권고를 게시합니다.

참고 : 이러한 보안 권고와 관련하여 TensorFlow 사용자는 SECURITY.md에 설명 된 TensorFlow의 보안 모델을 읽고 이해하는 것이 좋습니다.

Advisory       Type	                                Versions     	    Reported 	                 Additional 
Number	    	                                      affected          by                         Information

TFSA-        GIF 파일을 디코딩 할 때 	               <= 1.12           Baidu 보안 연구소
2019-        Null 포인터 Dereference 
001	         오류가 발생합니다.

TFSA-        제작 된 구성 파일로 인해                 <= 1.7           Tencent의 블레이드 팀
2018-        잘못된 메모리 액세스가 발생 함
006	
TFSA-       Memcpy 매개 변수가 겹쳐서 나타나는        <= 1.7           Tencent의 블레이드 팀
2018-       오래 된 적당한 라이브러리 사용
005		

TFSA-       검사 포인트 메타 파일 바운드 읽기          <= 1.7          Tencent의 블레이드 팀
2018-
004

TFSA-       TensorFlow Lite TOCO FlatBuffer          <= 1.7         Tencent의 블레이드 팀
2018-       구문 분석 취약점
003	

TFSA-       GIF 파일 구문 분석 Null 포인터            <= 1.5          Tencent의 블레이드 팀
2018-       Dereference 오류
002

TFSA-       BMP 파일 파서 범위를 벗어남 읽기           <= 1.6          Tencent의 블레이드 팀
2018-
001	

-	          Out of Bounds 읽기                      <= 1.4	         Tencent의 블레이드 팀  

