도움말 및 지원을 받으려면 스택 오버플로로 이동하십시오.

https://stackoverflow.com/questions/tagged/tensorflow

GitHub issue를 열면 다음 정책이 적용됩니다.

  1. 버그, 기능 요청 또는 문서와 관련된 중요한 문제여야 합니다. 작은 문서 수정은 대신 PR을 보내주십시오.
  2. 아래 양식을 작성해야합니다.
  3. TensorBoard issue가 아닙니다.

TensorFlow 개발자가 issue에 대응합니다. 우리는 버그 수정 및 기능 추가와 같이 전체 커뮤니티에 도움이 되는 작업에 중점을 두고자합니다. 
지원은 개인을 돕는 것입니다. GitHub는 또한 문제가 제기 될 때 수천 명의 사람들에게 알립니다. 스택 오버플로로 redirect되는 것이 아니라 재미있는 
문제를 의사소통하는 것을 보길 바랍니다.


시스템 정보
ㆍTensorFlow에서 제공하는 스톡 예제 스크립트를 사용하는 것과는 대조적으로 사용자 지정 코드를 작성했습니다.
ㆍOS 플랫폼 및 배포 (예 : Linux Ubuntu 16.04) :
ㆍ휴대 기기에서 문제가 발생하면 휴대 기기 (예 : iPhone 8, 픽셀 2, 삼성 Galaxy) :
ㆍTensorFlow가 (소스 또는 바이너리)에서 설치되었습니다.
ㆍTensorFlow 버전 (아래 명령 사용) :
ㆍPython 버전 :
ㆍBazel 버전 (소스에서 컴파일하는 경우) :
ㆍGCC / 컴파일러 버전 (소스에서 컴파일하는 경우) :
ㆍCUDA / cuDNN 버전 :
ㆍGPU 모델 및 메모리 :
ㆍ정확한 명령 재현 :

당신은 환경 캡처 스크립트를 사용하여 정보 중 일부를 수집 할 수 있습니다.
https://github.com/tensorflow/tensorflow/tree/master/tools/tf_env_collect.sh

다음과 같이 TensorFlow 버전을 구할 수 있습니다.

python –c "import tensorflow as tf; print (tf.version.GIT_VERSION, tf.version.VERSION)"


문제 설명
문제를 명확하게 여기에 설명하십시오. TensorFlow의 버그 또는 기능 요청이 왜 여기에 전달되었는지 확인하십시오.

소스 코드 / 로그
문제를 진단하는 데 유용한 모든 로그 또는 소스 코드를 포함하십시오. 추적을 포함하는 경우 전체 추적을 포함하십시오. 
큰 로그와 파일을 첨부해야합니다. 문제를 생성하는 데 필요한 최소한의 재현 가능한 테스트 케이스를 제공하십시오.
