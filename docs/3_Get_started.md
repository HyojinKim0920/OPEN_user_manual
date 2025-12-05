# Getting Started

## Start Python

* OPEN은 다양한 하위 폴더로 구성되어 있으며, 이들 간의 파일이 상호 유기적으로 연결되어 있다. 이러한 구조적 특성으로 인해 여러 Integrated Development Environment(e.g., Visual Studio Code, PyCharm, Spyder 등)을 통해 OPEN을 사용할 수 있다. 다만, OPEN의 복잡한 폴더 구조와 연동된 코드의 효율적인 관리를 위해, PyCharm을 권장한다. PyCharm은 프로젝트의 구조를 자동으로 인식하고, 외부 모듈 경로 설정 및 코드 추적 기능 등에서 보다 사용자 친화적인 기능을 하므로 사용자는 OPEN을 원활하게 사용할 수 있다.
* Python을 처음 시작하는 사용자의 경우 패키지 관리를 위해 conda 또는 pip 같은 사용이 편리한 package manager를 추천한다.

## Download OPEN

* OPEN의 최신 버전은 아래의 GitHub 저장소에서 제공된다. 사용자는 Source code를 직접 다운로드 하거나 git clone 명령어를 통해 로컬 저장소에 복제할 수 있다.

```
git clone https://github.com/nextgroup-or-kr/OPEN.git
```

## Install Virtual Environment

* 가상환경은 Python 프로젝트별로 독립적인 패키지 환경을 구성할 수 있는 도구로, 하나의 시스템에 여러 프로젝트가 존재할 때 서로 다른 버전의 패키지나 라이브러리의 충돌을 방지하고자 사용된다. OPEN은 `Python`의 다양한 패키지들을 사용하고 있는데, 앞서 설명한 충돌을 피하고자 가상환경을 구축하는 것을 권고한다. OPEN은 `envs`폴더에 가상환경 구축을 위한 환경 설정 파일인 `environment.yaml`을 제공하고 있다.
* Python 패키지 설치 도구로 `pip`를 설치했다면, 아래의 명령어로 가상환경을 구축할 수 있다.
  
```
pip env create -f environment.yaml
```

* Python 패키지 설치 도구로 `conda`를 설치했다면, 아래의 명령어로 가상환경을 구축할 수 있다.

```
conda env create -f environment.yaml
```

* 운영체계가 OS인 경우에는, apple silicon (macOS arm64)용 conda 채널에 `pyomo==6.0` 패키지가 제공되지 않아 가상환경 설치시 에러가 발생한다. 이를 해결하기 위해 environment.yaml에서 해당 패키지를 주석처리 후 가상환경 생성하고, 해당 가상환경에서 `pyomo`를 설치해야 한다.

## Using Solvers

* OPEN은 구축한 최적화 모델을 외부 솔버로 전달하여 문제 풀이를 수행한다. 이 모델은 상업용, 비상업용 solver에서 모두 사용할 수 있게 지원한다. 참고로 CPLEX는 academic license를 갖고 있다면 무료로 사용할 수 있다.
    - [CPLEX](https://www.ibm.com/products)
    - [GLPK](https://www.gnu.org/software/glpk/)