기여 가이드라인

pull Request 체크리스트

pull Request 전에 이 리스트를 반드시 따라야합니다.

ㆍ기여 지침을 읽으십시오.
ㆍ행동 규범을 읽으십시오.
ㆍ기여자 라이선스 계약 (CLA)에 서명했는지 확인하십시오.
ㆍ변경 사항이 가이드라인과 일치하는지 확인하십시오.
ㆍ변경 사항은 코딩 스타일과 일치합니다.
ㆍ단위 테스트를 실행하십시오.

기여자가 되어 자신의 코드를 제출하는 방법

기여자 라이선스 계약

우리는 당신의 패치를(코드) 수락하겠습니다! 우리가 그들을 데리고 가기 전에, 우리는 몇 가지 법적인 장애물을 뛰어 넘어야합니다.

개인 또는 법인 기여자 라이선스 계약 (CLA)을 작성하십시오.

ㆍ개인적으로 원본 소스 코드를 작성하고 지적 자산을 소유하고 있다면, 개별 CLA에 서명해야합니다.
ㆍ당신이 당신의 일에 기여할 수있는 회사를 위해 일한다면, 회사 CLA에 서명해야합니다.

위의 두 링크 중 하나를 따라 적절한 CLA에 액세스하고 서명하고 반환하는 방법에 대한 지시 사항을 따르십시오. 우리가 그것을 받으면 
우리는 당신의 견해 요청을 받아들일 수 있을 것입니다.

참고 : 귀하와 CLA에 서명 한 다른 사람들의 원본 소스 코드 만 기본 저장소로 받아들일 수 있습니다.


기여한 코드
TensorFlow를 개선 한 경우 당신의 pull request를 보내주십시오! 시작하기에 앞서 Github에는 HOWTO가 있습니다.

TensorFlow 팀 구성원은 당신의 pull request를 검토하도록 지정됩니다. pull request(끌어 오기 요청)가 승인되고 지속적인 통합 검사를 통과하면 
TensorFlow 팀 구성원이 변경 사항에 레이블을 붙일 준비를 합니다. 즉, 귀하의 요청을 내부 저장소에 제출하는 작업을 진행 합니다. 
변경 내용이 내부적으로 제출 된 후에는 GitHub에 자동으로 병합 요청이 병합됩니다.

기여하고 싶지만 시작할 곳이 확실하지 않은 경우 "기여 환영"라벨의 문제를 살펴보십시오. 이들은 우리가 외부 공헌에 특히 잘 맞는다고 믿는 이슈들입니다.
왜냐하면 지금 당장은 다가가지 않을 것이기 때문입니다. 이슈로 시작하기로 결정했다면, 다른 사람들이 당신이 그 일을 하고 있다는 것을 알 수 있도록 
코멘트를 남겨 두십시오. 혼자가 아니라 도움을 원한다면, 문제를 논평하는 스레드를 사용하여 조정하십시오.

기여 가이드라인 및 기준
검토 요청을 보내기 전에 변경 사항이 가이드라인과 일치하는지 확인하고 TensorFlow 코딩 스타일을 따르십시오.

기여를 위한 일반 지침 및 철학
ㆍ새로운 기능을 제공 할 때 단위 테스트를 포함하여 a) 코드가 올바르게 작동하는지 확인하고 b) 유지 관리 비용을 낮추기 위해 향후 
변경 사항을 방지하십시오.
ㆍ일반적으로 버그가 있으면 테스트 범위가 충분하지 않기 때문에 버그 수정에는 일반적으로 단위 테스트가 필요합니다.
ㆍ핵심 TensorFlow의 코드 (예 : tensorflow / core 및 tensorflow / python 코드)를 변경할 때 API 호환성을 염두에 두십시오. 
TensorFlow가 버전 1에 이르렀으므로 주요 릴리즈 없이 역방향 호환이 불가능한 API를 변경할 수 없습니다. 
pull request을 검토한 사용자는 API 호환성 문제에 대해 의견을 말합니다.

TensorFlow에 새로운 기능을 제공하면 유지 관리 부담이 (기본적으로) TensorFlow 팀으로 이전됩니다. 즉, 기여의 이점과 기능을 유지 관리하는 비용을 비교해야합니다.
최첨단 알고리즘을 구현하는 새로운 기능과 같은 완전히 새로운 기능은 코어로 마이그레이션을 해야하는지 여부를 결정하기 전에 일반적으로 텐서 플로우 / 애드온 (addor)에 있으며 대기 시간을 갖습니다.




특허
새 파일의 상단에 라이선스를 포함하십시오.

ㆍC / C ++ 라이선스 예제
ㆍPython 라이선스 예제
ㆍ자바 라이선스 예제
ㆍGo 라이선스 예제
ㆍBash 라이선스 예제
ㆍHTML 라이선스 예제
ㆍJavaScript / TypeScript 라이선스 예제

Bazel BUILD 파일에는 BUILD 예제와 같은 라이선스 섹션도 포함해야합니다.

C ++ 코딩 스타일
TensorFlow의 변경 사항 C ++ 코드는 Google C ++ 스타일 가이드를 준수해야합니다.
clang-tidy를 사용하여 C / C ++ 변경 사항을 확인하십시오. 우분투에 clang-tidy를 설치하려면 : 16.04, 다음과 같이하십시오.

apt-get install -y clang-tidy

다음을 수행하여 C / C ++ 파일을 확인할 수 있습니다.

clang-format <my_cc_file> --style = google> /tmp/my_cc_file.cc
diff <my_cc_file> /tmp/my_cc_file.cc


파이썬 코딩 스타일
TensorFlow의 변경 사항 Python 코드는 Google Python 스타일 가이드를 준수해야합니다.

pylint
를 사용하여 파이썬 변경 사항을 확인하십시오. 
pylint
를 설치하고 TensorFlow의 사용자 정의 스타일 정의를 검색하려면 다음을 수행하십시오.

pip install pylint
wget –O /tmp/pylintrc 
https://raw.githubusercontent.com/tensorflow/tensorflow/master/tensorflow/tools/ci_build/pylintrc


pylint
로 파일을 검사하려면,

pylint --rcfile = / tmp / pylintrc myfile.py


다른 언어의 코딩 스타일
ㆍGoogle Java 스타일 가이드
ㆍGoogle 자바 스크립트 스타일 가이드
ㆍGoogle 쉘 스타일 가이드
ㆍGoogle Objective-C 스타일 가이드

단위 테스트 실행
TensorFlow 단위 테스트를 실행하는 데는 두 가지 방법이 있습니다.

1. 시스템에 직접 설치된 도구 및 라이브러리 사용.

필요한 패키지는 CPU 전용 개발자 Dockerfile 및 GPU 개발자 Dockerfile을 참조하십시오. 
택일 적으로 시스템에 패키지를 설치하는 것을 피하기 위해 개발을 위해 tensorflow / tensorflow : nightly-devel 및 
tensorflow / tensorflow : nightly-devel-gpu와 같은 Docker 이미지를 사용하십시오 (이 경우 / root에서 / root로 디렉토리를 변경해야 함). 
/ 실행 된 컨테이너에 들어가면 텐셀 플로로 바젤이 텐서 흐름 작업 공간을 찾을 수 있습니다.


패키지가 설치되면 다음과 같이 bazel에서 특정 단위 테스트를 실행할 수 있습니다.

export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH"

export flags="--config=opt --config=cuda -k"


예를 들어 tensorflow / python으로 모든 테스트를 실행하려면 다음을 수행하십시오.

bazel test ${flags} //tensorflow/python/...

2. Docker 및 TensorFlow의 CI 스크립트 사용.

# Install Docker first, then this will build and run cpu tests
tensorflow/tools/ci_build/ci_build.sh CPU bazel test //tensorflow/...

자세한 내용은 TensorFlow 빌드를 참조하십시오.
