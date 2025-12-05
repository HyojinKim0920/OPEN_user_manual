# User Guide

## What is Scenario

* 시나리오는 현실 세계에게서 존재하거나 발생할 수 있는 특정 조건이나 상황을 모사하여 모델을 실행하는 하나의 설정을 의미한다. 사용자는 여러 시나리오를 통해 다양한 환경 변화나 정책 조건, 시스템의 구성 요인의 변화에 따른 영향을 분석할 수 있다. OPEN은 다중 시나리오 분석을 유연하게 지원하기 위해, 시나리오별 데이터 의존성에 따라 입력 데이터를 구조적으로 분리하여 관리하고 있다. 예를 들어, 시나리오에 영향을 미치지 않는 데이터는 `System Data` 폴더에, 시나리오별로 값이 달라지는 입력 데이터는 `resources/scenarios` 폴더에 각각 저장된다. 이러한 구조는 사용자로 하여금 여러 시나리오를 보다 명확하고 효율적으로 관리할 수 있도록 지원한다.
* OPEN은 다양한 제약조건과 기능 모듈들을 제공하고 있으며, 사용자는 목적에 맞게 이들을 선택적으로 활성화하거나 비활성화할 수 있다. 예를 들어, 단기 운영만 분석하고자 하는 경우에는 장기 설비계획 모듈을 제외하고 실행할 수 있으며, 온실가스 배출량과 같은 정책 제약을 고려하지 않도록 설정할 수도 있다. 반대로, 특정 정책 효과를 평가하기 위해 새로운 제약조건(예: 최소 설비 건설량)을 사용자 정의로 추가할 수도 있다.
* OPEN은 사용자가 원하는 분석 목적에 따라 시나리오를 유연하게 구성하고 실행할 수 있도록 설계되어 있으며, 시나리오 정의에 필요한 설정 방법과 입력 파일의 구조에 대해서는 이어서 자세히 설명한다.

## OPEN Inputs

* OPEN의 모든 입력 파일들은 CSV(Comma-Separated Values) 파일로 구성하고 있으며, 이는 사용자 친화적이고 다양한 툴에서 쉽게 편집할 수 있는 장점이 있다. 입력 파일은 크게 공통 데이터와 시나리오별 데이터로 구분되며, 폴더 경로에 따라 별도로 관리된다. 사용자의 이해를 돕기 위해 이 문서에서는 예시로 PowerGrid 라는 대상 시스템 내에서 다중 시나리오 중 하나인 ‘sub_scenario_1’를 가정한다.
  - 공통 데이터는 시나리오에 따라 변하지 않는 입력 파일들을 의미하며, 예를 들어 노드 정보, 송전선로 구성, 설비의 기본 특성 파라미터 등이 포함된다. PowerGrid에 대한 해당 파일들은 `System Data` 폴더 내에 위치한다.
  - 시나리오별 데이터는 시나리오마다 다르게 설정되는 데이터로, 연도별 전력수요, 설비 건설계획, 정책 옵션 등 이 여기에 해당된다. 이러한 파일들은 `PowerGrid/resources/scenario/sub_scenario_1`에서 관리되며, 다른 다중 시나리오들은 scenario의 하위 경로에 시나리오 폴더를 추가하면 된다.
  - OPEN은 시나리오에 영향을 주지 않는 입력 파일들은 System Data 폴더에서, 시나리오에 영향을 주는 파일들은 `resources/scenarios` 폴더에서 관리하고 있다. 아래 그림은 모델의 입력데이터에 대한 폴더의 구조를 보여주고 있으며, 사용자는 폴더와 데이터 구조, 파일명, 데이터 형식은 준수해야 한다.
* 사용자는 반드시 정해진 폴더 구조, 파일 이름, 데이터 형식을 준수해야 하며, OPEN은 이 구조를 기반으로 시뮬레이션 실행 시 자동으로 관련 데이터를 불러온다. 만약 구조가 임의로 변경되거나 형식에 맞지 않을 경우, 모델 실행 중 오류가 발생할 수 있으므로 주의가 필요하다. 단, 대상 시스템과 시나리오 이름은 변경할 수 있기 때문에, 해당 폴더명도 변경할 수 있다.

<pre>
examples/
└── PowerGrid/
    ├── System Data/
    │   ├── buses.csv
    │   ├── carriers.csv
    │   ├── generators-month-agc_max_pu.csv
    │   ├── generators-month-agc_min_pu.csv
    │   ├── generators-month-gf_max_pu.csv
    │   ├── generators-month-gf_min_pu.csv
    │   ├── generators-month-p_max_pu.csv
    │   ├── generators-month-p_min_pu.csv
    │   ├── generators-month-sfc.csv
    │   ├── generators.csv
    │   ├── lines.csv
    │   ├── links.csv
    │   ├── loads.csv
    │   └── storages.csv
    └── resources/
        ├── scenario_information.yaml
        └── scenarios/
            └── sub_scenario_1/
                ├── buses-year-lump_downward_reserve.csv
                ├── buses-year-lump_reserve.csv
                ├── carriers-year-capital_cost.csv
                ├── carriers-year-fom.csv
                ├── carriers-year-fuel_cost.csv
                ├── carriers-year-max_built.csv
                ├── carriers-year-max_capacity_2.csv
                ├── carriers-year-max_emission.csv
                ├── carriers-year-min_capacity.csv
                ├── carriers.csv
                ├── generators-hour-factor.csv
                ├── generators.csv
                ├── lines.csv
                ├── links.csv
                ├── loads-snapshots-p_set.csv
                └── storages.csv
</pre>

* 시나리오에 따라 영향을 받지 않는 데이터는 `System Data` 폴더에서 관리하고, 주로 설비의 특성과 지역 구분에 대한 내용을 다루고 있다. 입력 파일들의 구체적인 설명과 데이터 형식은 `open\component_attrs` 폴더에서 다루고 있다.

<table>
  <thead>
    <tr>
      <th style="width: 170px ; text-align:center;">파일명</th>
      <th style="text-align:center;">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>generators</code></td>
      <td>원자력, 석탄, LNG, LNG-CHP, 수력, IGCC, 바이오 등의 발전기의 운영특성 파라미터</td>
    </tr>
    <tr>
      <td><code>storages</code></td>
      <td>양수 발전기, 배터리 등의 저장장치 운영 특성 파라미터</td>
    </tr>
    <tr>
      <td><code>lines</code></td>
      <td>교류 송전선로의 파라미터</td>
    </tr>
    <tr>
      <td><code>links</code></td>
      <td>Power flow에 영향받지 않은 에너지 전달 매개체 (HVDC, 1차 에너지 등)</td>
    </tr>
    <tr>
      <td><code>carriers</code></td>
      <td>연료원별 공통된 이용률, 비용 특성, 배출계수, 수명, 최소운영기간 등 입력</td>
    </tr>
    <tr>
      <td><code>buses</code></td>
      <td>Bus별 전압, 전압 범위, 경도, 위도, Zone 구분</td>
    </tr>
    <tr>
      <td><code>loads</code></td>
      <td>국내 도 단위 지역으로 전력수요 구분</td>
    </tr>
    <tr>
      <td><code>generators-month-p_max_pu</code></td>
      <td>발전기(<code>generators</code>)의 월별 최대 출력값 (p.u.)</td>
    </tr>
    <tr>
      <td><code>generators-month-p_min_pu</code></td>
      <td>발전기(<code>generators</code>)의 월별 최소 출력값 (p.u.)</td>
    </tr>
    <tr>
      <td><code>generators-month-sfc</code></td>
      <td>발전기(<code>generators</code>)의 기동 단위 열량 (GCal)</td>
    </tr>
  </tbody>
</table>

* 시나리오에 따라 변경할 수 있는 데이터와 옵션 설정에 대한 파일들은 `resources/scenarios` 폴더에서 관리하고, `scenarios`에서 다중 시나리오에 따른 여러 하위 폴더들을 생성할 수 있다(e.g., `sub_scenario_1`, `sub_scenario_2`).

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 100px;">
  <col style="width: 600px;">
  <thead>
    <tr>
      <th style="text-align: center;">파일명</th>
      <th style="text-align: center;">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;"><code>generators</code></td>
      <td style="text-align: left;">후보 발전기의 이름, 연료원, 입력 파라미터 정보 입력</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>storages</code></td>
      <td style="text-align: left;">후보 양수 발전기, 저장장치의 입력 파라미터 정보 입력</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>lines</code></td>
      <td style="text-align: left;">건설 예정인 송전선로에 대한 정보 입력</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>links</code></td>
      <td style="text-align: left;">건설 예정인 HVDC 선로 정보 입력</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>carriers</code></td>
      <td style="text-align: left;">사용자가 설정한 제약조건 이름 입력</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>generators-hour-factor</code></td>
      <td style="text-align: left;">재생에너지의 지역별 시간대별 발전 패턴 정보 입력 (%)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>loads-snapshots-p_set</code></td>
      <td style="text-align: left;">지역별 시간대별 전력수요에 대한 정보 입력 (MWh)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>buses-year-lump_reserve</code></td>
      <td style="text-align: left;">연도별 전국 상향예비력 요구량 (MWh)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>carriers-year-min_capacity</code></td>
      <td style="text-align: left;">연도별 연료원별 최소 누적 설비용량 (MW)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>carriers-year-min_capacity_2</code></td>
      <td style="text-align: left;">연도별 연료원별 최소 누적 설비용량 (MW)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>carriers-year-max_capacity</code></td>
      <td style="text-align: left;">연도별 연료원별 최대 누적 설비용량 (MW)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>carriers-year-max_capacity_2</code></td>
      <td style="text-align: left;">연도별 연료원별 최대 누적 설비용량 (MW)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>buses-year-lump_downward_reserve</code></td>
      <td style="text-align: left;">연도별 육지와 제주의 하향예비력 요구량 (MWh)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>carriers-year-capital_cost</code></td>
      <td style="text-align: left;">연료원별 연도별 설비 투자 가격 (원/MW)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>carriers-year-fom</code></td>
      <td style="text-align: left;">연료원별 연도별 고정 운영 가격 (원/MW)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>carriers-year-fuel_cost</code></td>
      <td style="text-align: left;">연료원별 연도별 연료 가격 (원/Gcal)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>carriers-year-max_emission</code></td>
      <td style="text-align: left;">계획기간 내 대표 연도별 배출량 (tCO₂eq)</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>clustered_factor_xxxx_yyyy_z_Cw</code></td>
      <td style="text-align: left;">
        (사용자의 시나리오 설정에 따라 자동 생성) 축약된 지역별 재생에너지 이용률 프로파일<br>
        <small><code>xxxx</code>: 계획 시작년도, <code>yyyy</code>: 계획 종료년도, <code>z</code>: 년 당 대표일 수, <code>w</code>: 연속일 수</small>
      </td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>snapshots_weightings_xxxx_yyyy_z_z’_5_C1</code></td>
      <td style="text-align: left;">
        (사용자의 시나리오 설정에 따라 자동 생성) 축약된 재생에너지 이용률 프로파일<br>
        <small><code>xxxx</code>: 계획 시작년도, <code>yyyy</code>: 계획 종료년도, <code>z</code>: 년 당 대표일 수, <code>z’</code>: 군집 중 상위 z’%, <code>w</code>: 연속일 수</small>
      </td>
    </tr>
  </tbody>
</table>

## What is component of OPEN

* OPEN은 다양한 구성 요소(`component`)를 활용하여 전력 시스템을 표현하고 있다. 모든 구성 요소(e.g., bus, 발전기, 저장장치, 선로, 부하)는 network 객체(`n`)에 저장되며, 사용자는 해당 데이터를 조회, 수정, 시각화 할 수 있다. `component`는 정적인 특성을 가진 데이터와 시계열 특성을 가진 데이터로 구분된다. OPEN의 각 `component`에 대한 메타 데이터(속성명, 설명, 타입 등)는 아래의 표에 정리되어 있다. 또한 사용자는 `n.components` 딕셔너리를 통해 확인할 수 있으며, 예시로 bus의 모든 속성에 대해 확인하려면 `n.components["Bus"]["attrs"]`로 볼 수 있다.

  > **:loudspeaker: 주의사항**
  > <small>
  > - `{}`안에 해당 `component`나 `list_name`을 대입하면 됨
  > </small>


  - 정적인(static) 속성을 가진 `component`(e.g., bus, 발전기, 송전선로)는 n.{list_name} 형태로 저장되며, 예시로 bus는 n.buses에 저장된다. 이 pandas.DataFrame에서 행(index)는 `component`의 고유 문자열 이름에 해당하며, 열(column)은 `component`의 정적인 속성(attribute)에 해당한다. 예를 들어, n.buses.v_nom은 network의 bus 전압을 나타낸다.
  - 시계열(time-varying series) 속성을 가진 `component`는 `{list_name}`에 접미사 `_t`를 붙여 `{list_name}_t`로 표현된다. 예를 들어, 부하는 시간대별로 다른 전력사용량을 가지는데, 이는 `n.loads_t.p_set`로 확인 가능하다.
  
<table style="width: 100%; table-layout: fixed;">
  <col style="width: 180px;">
  <col style="width: 200px;">
  <col style="width: 520px;">
  <col style="width: 180px;">
  <thead>
    <tr>
      <th style="text-align: center;">component</th>
      <th style="text-align: center;">list_name</th>
      <th style="text-align: center;">설명</th>
      <th style="text-align: center;">type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;"><code>Network</code></td>
      <td style="text-align: center;"><code>networks</code></td>
      <td style="text-align: left;">모든 구성요소 및 기능들을 담고 있는 전체 네트워크 단위</td>
      <td style="text-align: center;"></td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>SubNetwork</code></td>
      <td style="text-align: center;"><code>sub_networks</code></td>
      <td style="text-align: left;">bus 및 passive branch 주1)의 부분집합으로, 서로 연결된 부분들 (e.g., synchronous area)</td>
      <td style="text-align: center;"></td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>Load</code></td>
      <td style="text-align: center;"><code>loads</code></td>
      <td style="text-align: left;">전력을 소비하는 설비로 PQ 부하로 표현</td>
      <td style="text-align: center;"><code>controllable_one_port</code></td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>Generator</code></td>
      <td style="text-align: center;"><code>generators</code></td>
      <td style="text-align: left;">전력을 생산하는 설비</td>
      <td style="text-align: center;"><code>controllable_one_port</code></td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>Storage</code></td>
      <td style="text-align: center;"><code>storages</code></td>
      <td style="text-align: left;">고정된 명판 에너지와 전력 비율을 가진 저장장치</td>
      <td style="text-align: center;"><code>controllable_one_port</code></td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>Bus</code></td>
      <td style="text-align: center;"><code>buses</code></td>
      <td style="text-align: left;">모든 전기적 노드를 의미하며, 발전기·부하·선로 등 모든 요소는 bus에 연결됨</td>
      <td style="text-align: center;"></td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>Carrier</code></td>
      <td style="text-align: center;"><code>carriers</code></td>
      <td style="text-align: left;">에너지 운반체 (e.g., 발전기, 교류/직류 송전선로 등)를 의미. bus는 직접적인 에너지 운반체를 갖고 있으며, 발전기는 주요 에너지 운반체를 표시.</td>
      <td style="text-align: center;"></td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>Line</code></td>
      <td style="text-align: center;"><code>lines</code></td>
      <td style="text-align: left;">가공선로와 케이블을 모두 포함하는 송전선로</td>
      <td style="text-align: center;"><code>passive_branch</code></td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>LineType</code></td>
      <td style="text-align: center;"><code>line_types</code></td>
      <td style="text-align: left;">표준 송전선로의 데이터셋으로 길이당 임피던스 값을 갖는 표준 선로 유형</td>
      <td style="text-align: center;"><code>standard_type</code></td>
    </tr>
    <tr>
      <td style="text-align: center;"><code>Link</code></td>
      <td style="text-align: center;"><code>links</code></td>
      <td style="text-align: left;">
        두 bus 간 제어 가능한 유효전력 연결. 송전 전력 흐름 모델, 손실이 있는 에너지 converter, DC 연결의 간소화된 버전으로 사용할 수 있음.<br>
        <small>※ 손실 없는 양방향 HVDC는 <code>p_min_pu = -1</code>, <code>efficiency = 1</code>로 설정</small><br>
        <small>※ Link는 무효전력을 생성하거나 소비하지 않는 것으로 가정</small>
      </td>
      <td style="text-align: center;"><code>controllable_branch</code></td>
    </tr>
  </tbody>
</table>

  > **:mag_right: 참고사항**
  > <small>
  > - passive_branch는 전압의 차이에 의해 전류가 흐르며, 자체적으로 유효전력 또는 무효전력을 제어할 수 없는 설비  
  > - controllable_branch는 두 버스 간 전력흐름을 직접 제어할 수 있는 설비(HVDC 등)  
  > - controllable_one_port는 최적화를 통해 결정되는 제어 가능한 단일 포트  
  > - standard type는 통상적 설비 규격을 의미
  > </small>

* 각 `component`에 대한 구체적인 속성(attribute)은 순차적으로 제시되어 있다. 기본값은 사용자가 입력하지 않더라도 OPEN에서 제공하는 값으로, 사용자가 목적에 맞게 변경 가능하다. 사용자가 각 attribute에 대한 값을 비워둘 경우 OPEN은 기본값으로 값을 채운다. 속성별 데이터 유형(type)은 크게 문자형(string), 인덱스 기반 참조 데이터(pandas.Index), 실수형(float), 정수형(int), 논리형(boolean)으로 구분된다. 입력 데이터 중에서 사용자가 OPEN에서 반드시 입력해야 하는 경우 ‘Input(필수)’로, 사용자가 입력하지 않으면 기본값이 자동 적용되며 수정할 수 있는 경우에 ‘Input(선택 옵션)’으로 구분하였다. 사용자의 입력을 통해 OPEN에서 결정되는 파라미터나 OPEN의 결정변수는 ‘Output’으로 구분하였다.
* `networks`는 모든 `component`를 포함하는 전체적인 컨테이너(container)다.

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 170px;">
  <col style="width: 450px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <thead>
    <tr>
      <th style="text-align: center;">속성(attribute)</th>
      <th style="text-align: left;">설명</th>
      <th style="text-align: center;">기본값</th>
      <th style="text-align: center;">자료형</th>
      <th style="text-align: center;">입출력 구분</th>
      <th style="text-align: center;">단위</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">name</code></td>
      <td style="text-align: left;">네트워크명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">snapshots</code></td>
      <td style="text-align: left;">OPEN에서 사용하고 있는 time step으로 시계열 데이터는n.snapshots로 인덱싱 됨</td>
      <td style="text-align: center;">[&quot;now&quot;]</td>
      <td style="text-align: center;">pandas.Index</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">candidate</code></td>
      <td style="text-align: left;">후보설비 판단 (T: 후보설비를 의미, F: 후보설비가 아님)</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">boolean</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
  </tbody>
</table>

* `sub_networks`는 OPEN에 의해 결정되므로, 사용자가 직접 입력할 수 없다. `sub_networks`는 bus와 passive_branch(e.g., 선로, 변압기)로 구성된 `network`의 하위 집합으로, 버스의 carrier를 상속받는다. `sub_networks`는 `n.determine_network_topology`를 통해 결정된다.

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 170px;">
  <col style="width: 450px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <thead>
    <tr>
      <th style="text-align: center;">속성(attribute)</th>
      <th style="text-align: left;">설명</th>
      <th style="text-align: center;">기본값</th>
      <th style="text-align: center;">자료형</th>
      <th style="text-align: center;">입출력 구분</th>
      <th style="text-align: center;">단위</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">name</code></td>
      <td style="text-align: left;">sub_networks명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">carrier</code></td>
      <td style="text-align: left;">sub_network의 에너지 유형을 정의하며, bus에 의해 결정됨 (e.g., AC, DC)</td>
      <td style="text-align: center;">AC</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">slack_bus</code></td>
      <td style="text-align: left;">slack bus명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">NaN</td>
    </tr>
  </tbody>
</table>

* `bus`는 `network`의 기본 노드로 발전기, 부하, 송전선로, 저장장치 같은 `component`가 연결된다. 키르히호프 전류 법칙(Kirchhoff's Current Law)에 따라 Bus에 주입되는 전력과 인출되는 전력의 크기는 같아야 한다(에너지 보존 법칙).

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 170px;">
  <col style="width: 450px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">

  <thead>
    <tr>
      <th style="text-align: center;">속성(attribute)</th>
      <th style="text-align: center;">설명</th>
      <th style="text-align: center;">기본값</th>
      <th style="text-align: center;">자료형</th>
      <th style="text-align: center;">입출력 구분</th>
      <th style="text-align: center;">단위</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">name</code></td>
      <td style="text-align:left;">bus명</td>
      <td style="text-align:center;">n/a</td>
      <td style="text-align:center;">string</td>
      <td style="text-align:center;">Input (필수)</td>
      <td style="text-align:center;">n/a</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">v_nom</code></td>
      <td style="text-align:left;">bus의 정격 전압</td>
      <td style="text-align:center;">1</td>
      <td style="text-align:center;">float</td>
      <td style="text-align:center;">Input (선택 옵션)</td>
      <td style="text-align:center;">kV</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">x</code></td>
      <td style="text-align:left;">bus의 x좌표(e.g., 경도). SRID는 <code style="word-break: break-all;">network.srid</code>로 설정됨</td>
      <td style="text-align:center;">0</td>
      <td style="text-align:center;">float</td>
      <td style="text-align:center;">Input (선택 옵션)</td>
      <td style="text-align:center;">n/a</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">y</code></td>
      <td style="text-align:left;">bus의 y좌표(e.g., 위도). SRID는 <code style="word-break: break-all;">network.srid</code>로 설정됨</td>
      <td style="text-align:center;">0</td>
      <td style="text-align:center;">float</td>
      <td style="text-align:center;">Input (선택 옵션)</td>
      <td style="text-align:center;">n/a</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">carrier</code></td>
      <td style="text-align:left;">bus의 전력흐름 유형 (e.g., AC, DC)</td>
      <td style="text-align:center;">AC</td>
      <td style="text-align:center;">string</td>
      <td style="text-align:center;">Input (required)</td>
      <td style="text-align:center;">n/a</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">v_mag_pu_set</code></td>
      <td style="text-align:left;">bus의 전압 설정값(set point). 정격전압 <code style="word-break: break-all;">v_nom</code>의 p.u.</td>
      <td style="text-align:center;">1</td>
      <td style="text-align:center;">static, series</td>
      <td style="text-align:center;">Input (선택 옵션)</td>
      <td style="text-align:center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">control</code></td>
      <td style="text-align:left;">PF 제어전략(P, Q, V). 발전기에서 상속되는 속성이므로 bus에서 설정해도 적용되지 않음</td>
      <td style="text-align:center;">PQ</td>
      <td style="text-align:center;">string</td>
      <td style="text-align:center;">Output</td>
      <td style="text-align:center;">n/a</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">p</code></td>
      <td style="text-align:left;">bus의 유효전력 (양수 = 공급)</td>
      <td style="text-align:center;">0</td>
      <td style="text-align:center;">series</td>
      <td style="text-align:center;">Output</td>
      <td style="text-align:center;">MW</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">q</code></td>
      <td style="text-align:left;">bus의 무효전력 (양수 = 공급)</td>
      <td style="text-align:center;">0</td>
      <td style="text-align:center;">series</td>
      <td style="text-align:center;">Output</td>
      <td style="text-align:center;">MVar</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">v_mag_pu</code></td>
      <td style="text-align:left;">bus의 실제 전압</td>
      <td style="text-align:center;">1</td>
      <td style="text-align:center;">series</td>
      <td style="text-align:center;">Output</td>
      <td style="text-align:center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">v_ang</code></td>
      <td style="text-align:left;">위상각</td>
      <td style="text-align:center;">0</td>
      <td style="text-align:center;">series</td>
      <td style="text-align:center;">Output</td>
      <td style="text-align:center;">radians</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">system_marginal_price</code></td>
      <td style="text-align:left;">계통 한계 가격</td>
      <td style="text-align:center;">0</td>
      <td style="text-align:center;">series</td>
      <td style="text-align:center;">Output</td>
      <td style="text-align:center;">KRW/MWh</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">sub_network</code></td>
      <td style="text-align:left;">Bus에 속한 subnetwork (<code style="word-break: break-all;">network.determine_network_topology()</code>에 의해 설정)</td>
      <td style="text-align:center;">n/a</td>
      <td style="text-align:center;">string</td>
      <td style="text-align:center;">Output</td>
      <td style="text-align:center;">n/a</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">marginal_price</code></td>
      <td style="text-align:left;">모선 한계 가격</td>
      <td style="text-align:center;">0</td>
      <td style="text-align:center;">series</td>
      <td style="text-align:center;">Output</td>
      <td style="text-align:center;">KRW/MWh</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">zone</code></td>
      <td style="text-align:left;">운영 예비력 판단 기준 구역</td>
      <td style="text-align:center;">NaN</td>
      <td style="text-align:center;">string</td>
      <td style="text-align:center;">Input (선택 옵션)</td>
      <td style="text-align:center;">n/a</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">lump_reserve</code></td>
      <td style="text-align:left;">상향 예비력(up spinning reserve) 요구량</td>
      <td style="text-align:center;">0</td>
      <td style="text-align:center;">static, series</td>
      <td style="text-align:center;">Input (선택 옵션)</td>
      <td style="text-align:center;">MW</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code style="word-break: break-all;">lump_downward_reserve</code></td>
      <td style="text-align:left;">하향 예비력(down spinning reserve) 요구량</td>
      <td style="text-align:center;">0</td>
      <td style="text-align:center;">static, series</td>
      <td style="text-align:center;">Input (선택 옵션)</td>
      <td style="text-align:center;">MW</td>
    </tr>
  </tbody>
</table>

* 발전기(`Generator`)는 단일 버스에 연결되어, 발전기의 `carrier`(e.g., coal, nuclear, PV)를 bus의 carrier(e.g., AC)로 변환하여 전력을 공급한다. 발전기는 최소 출력(`p_nom * p_min_pu`)부터 최대 출력(`p_nom * p_max_pu`) 사이의 범위에서 출력량을 조절할 수 있다. 전통적인 발전기처럼 정적인 특성을 가지는 발전기는 고정된 최소 출력과 최대 출력 사이의 값을 가지며, 이 때 `p_max_pu`는 de-rating factor 역할도 수행한다. 반면에, 기상 상황에 의존하는 재생 에너지 설비는 시간에 따라 최대 출력의 범위가 달라진다. 예를 들어, OPEN에서 전통적인 발전기의 최대 출력은 `n.generator.loc[gen_name, "p_max_pu"]`에 저장되지만, 재생에너지의 최대 출력은 `n.generators_t.p_max_pu[gen_name]`에 저장되며 시간에 따라 다른 값을 가진다.

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 170px;">
  <col style="width: 450px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <thead>
    <tr>
      <th style="text-align: center;">속성(attribute)</th>
      <th style="text-align: left;">설명</th>
      <th style="text-align: center;">기본값</th>
      <th style="text-align: center;">자료형</th>
      <th style="text-align: center;">입출력 구분</th>
      <th style="text-align: center;">단위</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">name</code></td>
      <td style="text-align: left;">발전기명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">bus</code></td>
      <td style="text-align: left;">발전기가 연결된 bus명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">control</code></td>
      <td style="text-align: left;">PF를 위한 P, Q, V 제어전략(e.g., PQ, PV, Slack)</td>
      <td style="text-align: center;">PQ</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">carrier</code></td>
      <td style="text-align: left;">발전기 연료원(e.g., coal, nuclear, LNG, hydro )</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">factor</code></td>
      <td style="text-align: left;">snapshots 별 이용률</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">sector</code></td>
      <td style="text-align: left;">재생에너지가 특정 지역의 이용률을 따르기 위한 지역 구분</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">curtailment_ratio</code></td>
      <td style="text-align: left;">snapshots 동안 출력제어 가능한 비율</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">candidate</code></td>
      <td style="text-align: left;">후보설비 판단(T: 후보설비를 의미, F: 후보설비가 아님)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">boolean</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">start_date</code></td>
      <td style="text-align: left;">설비 운영 시작일</td>
      <td style="text-align: center;">2000-01-01 12:00:00</td>
      <td style="text-align: center;">datetime</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">end_date</code></td>
      <td style="text-align: left;">설비 운영 종료일</td>
      <td style="text-align: center;">2100-01-01 12:00:00</td>
      <td style="text-align: center;">datetime</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_nom</code></td>
      <td style="text-align: left;">발전기 설비용량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_min_pu</code></td>
      <td style="text-align: left;">발전기의 최소 출력 p.u.로, committable=False이고 p_min_pu&gt;0인 경우 must-run발전기를 의미 (전통적인 발전기는 시계열에 관계없이 일정한 값을 갖지만, 재생 에너지 발전기의 경우 snapshot에 따라 달라짐)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_max_pu</code></td>
      <td style="text-align: left;">발전기의 최대 출력 p.u. (전통적인 발전기는 고정된 값을 갖지만, 재생 에너지 발전기의 경우 snapshot에 따라 달라짐)</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_up_time</code></td>
      <td style="text-align: left;">설비가 적어도 켜져 있어야 하는 snapshots 수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">int</td>
      <td style="text-align: center;">Input (필수 옵션)</td>
      <td style="text-align: center;">snapshots</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_down_time</code></td>
      <td style="text-align: left;">설비가 적어도 꺼져 있어야 하는 snapshots 수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">int</td>
      <td style="text-align: center;">Input (필수 옵션)</td>
      <td style="text-align: center;">snapshots</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">up_time_before</code></td>
      <td style="text-align: left;">계획기간 이전에 설비가 켜져 있었던 snapshots 수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">int</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">down_time_before</code></td>
      <td style="text-align: left;">계획기간 이전에 설비가 꺼져 있었던 snapshots 수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">int</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">committable</code></td>
      <td style="text-align: left;">급전 가능 여부(T: 급전가능, F: 급전불가능)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">boolean</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">ramp_limit_up</code></td>
      <td style="text-align: left;">최대 출력 증가율</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (필수 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">ramp_limit_down</code></td>
      <td style="text-align: left;">최대 출력 감소율</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (필수 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">ramp_limit_start_up</code></td>
      <td style="text-align: left;">기동 시 최대 출력 증가율</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (필수 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">ramp_limit_shut_down</code></td>
      <td style="text-align: left;">정지 시 최대 출력 감소율</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (필수 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">lifetime</code></td>
      <td style="text-align: left;">설비의 설계수명</td>
      <td style="text-align: center;">100</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">year</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_operation_year</code></td>
      <td style="text-align: left;">설비 최소 가동 기간</td>
      <td style="text-align: center;">100</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">year</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">hurdle_rate</code></td>
      <td style="text-align: left;">최소 이용률</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">parent_unit</code></td>
      <td style="text-align: left;">발전기의 정보가 부족한 경우 기존의 발전기 특성을 가져올 때 해당 발전기 명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">co2</code></td>
      <td style="text-align: left;">이산화탄소(CO2)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">tonne/MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nox</code></td>
      <td style="text-align: left;">질소산화물(NOx)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">tonne/MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">pm2.5</code></td>
      <td style="text-align: left;">초미세먼지(PM2.5)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">tonne/MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">sox</code></td>
      <td style="text-align: left;">황산화물(SOx)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">tonne/MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">tsm</code></td>
      <td style="text-align: left;">총 부유 물질 (Total Suspended Matter)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">tonne/MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">forced_rate</code></td>
      <td style="text-align: left;">고장률</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">maintenance_rate</code></td>
      <td style="text-align: left;">유지보수율</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">fuel_cost</code></td>
      <td style="text-align: left;">열량가격</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/Gcal</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">capacity_factor</code></td>
      <td style="text-align: left;">연간 용량 기여율</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">qhc</code></td>
      <td style="text-align: left;">발전기 출력과 소비열량의 관계를 나타내는 2차 입출력 특성곡선식의 2차계수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">Gcal/MWh^2</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">lhc</code></td>
      <td style="text-align: left;">발전기 출력과 소비열량의 관계를 나타내는 2차 입출력 특성곡선식의 1차계수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">Gcal/MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nlhc</code></td>
      <td style="text-align: left;">발전기 출력과 소비열량의 관계를 나타내는 2차 입출력 특성곡선식의 상수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">Gcal/h</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">agc_max_pu</code></td>
      <td style="text-align: left;">자동발전제어서비스 최대 제공 용량 p.u.</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">agc_min_pu</code></td>
      <td style="text-align: left;">자동발전제어서비스 최소 제공 용량 p.u.</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">gf_max_pu</code></td>
      <td style="text-align: left;">주파수추종서비스 응답가능 최대 용량 p.u.</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">gf_min_pu</code></td>
      <td style="text-align: left;">주파수추종서비스 응답가능 최소 용량 p.u.</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">tlf</code></td>
      <td style="text-align: left;">송전손실계수</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">sfc</code></td>
      <td style="text-align: left;">열량가격당 기동연료비</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input(선택 옵션)</td>
      <td style="text-align: center;">KRW/Gcal</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">u0</code></td>
      <td style="text-align: left;">최초 기동 상태</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">int</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">capital_cost</code></td>
      <td style="text-align: left;">1MW의 용량 당 자본 비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">fom</code></td>
      <td style="text-align: left;">연간 발전기 고정 운영비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_set</code></td>
      <td style="text-align: left;">PF를 위한 유효전력 설정값(set point)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">q_set</code></td>
      <td style="text-align: left;">PF를 위한 무효전력 설정값(set point)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MVar</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">sign</code></td>
      <td style="text-align: left;">부호</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nb_0</code></td>
      <td style="text-align: left;">계획기간 이전에 건설된 있던 설비의 개수</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">no</code></td>
      <td style="text-align: left;">해당 시점까지 운영중인 설비 개수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nb</code></td>
      <td style="text-align: left;">해당 시점에 구축된 설비 개수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nr</code></td>
      <td style="text-align: left;">해당 시점까지 퇴출되어 온 설비 개수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p</code></td>
      <td style="text-align: left;">발전기의 유효전력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">q</code></td>
      <td style="text-align: left;">발전기의 무효전력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MVar</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">status</code></td>
      <td style="text-align: left;">발전기 상태 (1: 기동, 0: 정지)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">status_startup</code></td>
      <td style="text-align: left;">발전기 기동 시작 상태 (1: 기동)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">status_shutdown</code></td>
      <td style="text-align: left;">발전기 정지 시작 상태 (1: 정지)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_ru</code></td>
      <td style="text-align: left;">상향 예비력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_rd</code></td>
      <td style="text-align: left;">하향 예비력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">emission</code></td>
      <td style="text-align: left;">배출량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">ton</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">gen_cost</code></td>
      <td style="text-align: left;">발전비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">maintenance_capacity</code></td>
      <td style="text-align: left;">유지보수 중인 용량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_built</code></td>
      <td style="text-align: left;">최대 구축 가능한 개수 (문제 풀이 step에 대해서)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_units</code></td>
      <td style="text-align: left;">최대로 운영가능한 설비 수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_units</code></td>
      <td style="text-align: left;">최소로 운영가능한 설비 수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_capacity</code></td>
      <td style="text-align: left;">최대 설치용량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_generation</code></td>
      <td style="text-align: left;">지정된 snapshots 동안 최대 발전량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_generation</code></td>
      <td style="text-align: left;">최소 발전량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_emission</code></td>
      <td style="text-align: left;">지정된 snapshots 동안 최대 배출량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ton</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_up_units</code></td>
      <td style="text-align: left;">지정된 snapshots 동안 최소 기동중인 발전기 개수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">marginal_cost</code></td>
      <td style="text-align: left;">1MWh의 한계 비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">curtailed_energy</code></td>
      <td style="text-align: left;">출력제어 된 에너지</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">conversion_code</code></td>
      <td style="text-align: left;">연료전환 식별코드</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">annuity_factor</code></td>
      <td style="text-align: left;">연가화 비율</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">inertia_constant</code></td>
      <td style="text-align: left;">관성상수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">s</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">curtailment_price</code></td>
      <td style="text-align: left;">비중앙발전기 출력제어 단가</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_financing_year</code></td>
      <td style="text-align: left;">금융조달기간</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">year</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">retirement_cost</code></td>
      <td style="text-align: left;">설비폐지 시 요구되는 미납된 설비투자 비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">gen_startup_cost</code></td>
      <td style="text-align: left;">기동 비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">gen_shutdown_cost</code></td>
      <td style="text-align: left;">정지 비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">transition_cost</code></td>
      <td style="text-align: left;">연료 전환 비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">number_of_operation_set</code></td>
      <td style="text-align: left;">계획기간 동안 켜져야 할 must-run 발전기 수</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">build_cost</code></td>
      <td style="text-align: left;">자본 비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">fixed_cost</code></td>
      <td style="text-align: left;">고정 비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">curtailed_cost</code></td>
      <td style="text-align: left;">출력제어 비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">cyclic_state</code></td>
      <td style="text-align: left;">대표일들 사이에서 각 대표일의 초기값과 후기값 연결 여부를 표시 (T : 연결, F : 분리)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">boolean</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
  </tbody>
</table>

* 저장장치(`storage`)는 단일 bus에 연결되며, 전력계통의 수급 불균형이 발생할 경우 연결된 버스에 전력을 공급하거나 흡수하여 수급균형을 지원한다. OPEN에서는 배터리와 양수발전기가 여기에 해당한다. 저장장치는 시간에 따라 에너지 저장량과 충전/방전 전력이 달라진다. 저장장치의 에너지 저장 용량(`p_nom`, 단위: MWh)은 저장장치가 최대출력으로 방전할 수 있는 시간(`max_hours`, 단위: h)과 정격 용량(`p_nom`, 단위: MW)의 곱으로 결정된다.

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 170px;">
  <col style="width: 450px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <thead>
    <tr>
      <th style="text-align: center;">속성(attribute)</th>
      <th style="text-align: left;">설명</th>
      <th style="text-align: center;">기본값</th>
      <th style="text-align: center;">자료형</th>
      <th style="text-align: center;">입출력구분 </th>
      <th style="text-align: center;">단위</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">name</code></td>
      <td style="text-align: left;">저장장치명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">bus</code></td>
      <td style="text-align: left;">저장장치가 연결된 버스명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">control</code></td>
      <td style="text-align: left;">PF를 위한 P, Q, V 제어전략 (e.g., PQ, PV, Slack)</td>
      <td style="text-align: center;">PQ</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">carrier</code></td>
      <td style="text-align: left;">저장장치의 에너지 저장 방식 (e.g., PHS, battery-4h)</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">candidate</code></td>
      <td style="text-align: left;">후보설비 판단 (T: 후보설비를 의미, F: 후보설비가 아님)</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">boolean</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">start_date</code></td>
      <td style="text-align: left;">설비 운영 시작일</td>
      <td style="text-align: center;">2000-01-01 00:00:00</td>
      <td style="text-align: center;">datetime</td>
      <td style="text-align: center;">Input (optional)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">end_date</code></td>
      <td style="text-align: left;">설비 운영 종료일</td>
      <td style="text-align: center;">2100-01-01 00:00:00</td>
      <td style="text-align: center;">datetime</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_nom</code></td>
      <td style="text-align: left;">설비의 정격 출력용량</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">lifetime</code></td>
      <td style="text-align: left;">설비 설계수명</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">years</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_operation_year</code></td>
      <td style="text-align: left;">설비 최소 가동 기간</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">year</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_dch_max_pu</code></td>
      <td style="text-align: left;">각 snapshot에서 최대방전용량 p.u.</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_ch_max_pu</code></td>
      <td style="text-align: left;">각 snapshot에서 최대충전용량 p.u.</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_dch_min_pu</code></td>
      <td style="text-align: left;">각 snapshot에서 최소방전용량 p.u.</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_ch_min_pu</code></td>
      <td style="text-align: left;">각 snapshot에서 최소충전용량 p.u.</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">e_head_max_pu</code></td>
      <td style="text-align: left;">설비의 최대 에너지 저장량 p.u.</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">e_head_min_pu</code></td>
      <td style="text-align: left;">설비의 최소 에너지 저장량 p.u.</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_set</code></td>
      <td style="text-align: left;">PF를 위한 유효전력 설정값(set point)</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">q_set</code></td>
      <td style="text-align: left;">PF를 위한 무효전력 설정값(set point)</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MVar</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">sign</code></td>
      <td style="text-align: left;">부호</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">marginal_cost</code></td>
      <td style="text-align: left;">1MWh에 대한 한계비용</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">capital_cost</code></td>
      <td style="text-align: left;">1MW에 대한 건설비용</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">forced_rate</code></td>
      <td style="text-align: left;">설비 고장률</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">maintenance_rate</code></td>
      <td style="text-align: left;">설비 유지보수율</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">fom</code></td>
      <td style="text-align: left;">연간 용량당 고정 운영비용</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">capacity_factor</code></td>
      <td style="text-align: left;">연간 용량 기여율</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nb_0</code></td>
      <td style="text-align: left;">계획기간 이전에 건설된 설비의 개수</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">no</code></td>
      <td style="text-align: left;">해당 시점까지 운영중인 발전기 개수</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nb</code></td>
      <td style="text-align: left;">해당 시점에 건설된 발전기 개수</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nr</code></td>
      <td style="text-align: left;">해당 시점까지 퇴출되어 온 발전기 개수</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_ru</code></td>
      <td style="text-align: left;">상향 예비력</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_rd</code></td>
      <td style="text-align: left;">하향 예비력</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">maintenance_capacity</code></td>
      <td style="text-align: left;">유지보수 중인 용량</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_built</code></td>
      <td style="text-align: left;">최대 구축 가능한 개수 (문제 풀이 step에 대해서)</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_built</code></td>
      <td style="text-align: left;">최소 구축해야 하는 개수</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_units</code></td>
      <td style="text-align: left;">최대로 운영가능한 설비 수</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_units</code></td>
      <td style="text-align: left;">최소로 운영가능한 설비 수</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">state_of_charge_initial</code></td>
      <td style="text-align: left;">저장장치의 초기 저장량</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">cyclic_state</code></td>
      <td style="text-align: left;">대표일들 사이에서 각 대표일의 초기값과 후기값 연결 여부를 표시 (T : 연결, F : 분리)</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">boolean</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_hours</code></td>
      <td style="text-align: left;">정격 출력으로 방전 가능한 시간</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">hours</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">efficiency_store</code></td>
      <td style="text-align: left;">저장장치의 충전 효율</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">efficiency_dispatch</code></td>
      <td style="text-align: left;">저장장치의 방전 효율</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">standing_loss</code></td>
      <td style="text-align: left;">시간 당 자가 방전 효율</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">state_of_charge_set</code></td>
      <td style="text-align: left;">State of charge set points for snapshots in the OPF.</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p</code></td>
      <td style="text-align: left;">저장장치의 유효전력</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">q</code></td>
      <td style="text-align: left;">저장장치의 무효전력</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MVar</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">state_of_charge</code></td>
      <td style="text-align: left;">저장장치의 에너지 저장량</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">sr</code></td>
      <td style="text-align: left;">속도조정률</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input(선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">gf_max_pu</code></td>
      <td style="text-align: left;">주파수추종서비스 응답가능 최대 용량 p.u.</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input(선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">annuity_factor</code></td>
      <td style="text-align: left;">연가화 비율</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_financing_year</code></td>
      <td style="text-align: left;">금융조달기간</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">year</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">retirement_cost</code></td>
      <td style="text-align: left;">설비폐지 시 요구되는 미납된 설비투자비용</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">inertia_constant</code></td>
      <td style="text-align: left;">관성상수</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">s</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">build_cost</code></td>
      <td style="text-align: left;">건설비용</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">fixed_cost</code></td>
      <td style="text-align: left;">고정비용</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
  </tbody>
</table>

* 부하(`load`)는 단일 bus에 연결되며, PQ부하로서 유효전력과 무효전력을 소비한다. 또한, OPEN 확장에 있어 전력시스템의 부하뿐만 아니라, 수소나 열 등 다른 에너지 수요를 모델링하는 데에도 활용될 수 있다.

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 170px;">
  <col style="width: 450px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <thead>
    <tr>
      <th style="text-align: center;">속성(attribute)</th>
      <th style="text-align: left;">설명</th>
      <th style="text-align: center;">기본값</th>
      <th style="text-align: center;">자료형</th>
      <th style="text-align: center;">입출력 구분</th>
      <th style="text-align: center;">단위</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">name</code></td>
      <td style="text-align: left;">부하명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">bus</code></td>
      <td style="text-align: left;">부하가 접속된 bus명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">carrier</code></td>
      <td style="text-align: left;">부하가 소비하는 에너지 유형(e.g., AC, DC)</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_set</code></td>
      <td style="text-align: left;">PF를 위한 유효전력 설정값(set point)</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">q_set</code></td>
      <td style="text-align: left;">PF를 위한 무효전력 설정값(set point)</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MVar</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p</code></td>
      <td style="text-align: left;">유효전력</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">q</code></td>
      <td style="text-align: left;">무효전력</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MVar</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">sign</code></td>
      <td style="text-align: left;">부호</td>
      <td style="text-align: center;">-1.0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">lost_load</code></td>
      <td style="text-align: left;">공급지장비율</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">voll</code></td>
      <td style="text-align: left;">공급지장 페널티 가격</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">load_shedding</code></td>
      <td style="text-align: left;">부하삭감량</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">penalty_cost</code></td>
      <td style="text-align: left;">공급지장 페널티 비용</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
  </tbody>
</table>

* 션트 임피던스(`shunt impedance`)는 단일 bus에 연결되며, 전압에 의존하는 어드미턴스(voltage-dependent admittance)를 가진다. 션트 임피던스는 어드미턴스로도 표현될 수 있으며, y = G + jB로 나타낸다. 션트 임피던스의 전력 소비는 $s_i=|V_i |^2 y_i^*=p_i+jq_i= |V_i |^2 (g_i-jb_i)$와 같다. 여기서 유효전력($p_i= |V_i |^2 g_i$)이 양의 값을 가지면 션트 임피던스가 bus에서 유효전력을 소비하고, 무효전력($q_i=|V_i |^2 b_i$)가 양의 값을 가지면 캐패시터처럼 동작하며 무효전력을 공급하는 것을 의미한다.

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 170px;">
  <col style="width: 450px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <thead>
    <tr>
      <th style="text-align: center;">속성(attribute)</th>
      <th style="text-align: left;">설명</th>
      <th style="text-align: center;">기본값</th>
      <th style="text-align: center;">자료형</th>
      <th style="text-align: center;">입출력 구분</th>
      <th style="text-align: center;">단위</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">name</code></td>
      <td style="text-align: left;">션트 임피던스 명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">bus</code></td>
      <td style="text-align: left;">발전기가 연결되어 있는 bus명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">g</code></td>
      <td style="text-align: left;">션트 컨덕턴스</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">℧ </td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">b</code></td>
      <td style="text-align: left;">션트 서셉턴스</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">S</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">sign</code></td>
      <td style="text-align: left;">부호</td>
      <td style="text-align: center;">-1.0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p</code></td>
      <td style="text-align: left;">유효전력</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">q</code></td>
      <td style="text-align: left;">무효전력</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MVar</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">g_pu</code></td>
      <td style="text-align: left;">g의 p.u.</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">b_pu</code></td>
      <td style="text-align: left;">b의 p.u.</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">build_cost</code></td>
      <td style="text-align: left;">건설비용</td>
      <td style="text-align: center;">0.0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
  </tbody>
</table>

* 선로(`line`)은 OPEN에서 송전선로를 의미한다. 선로는 AC bus나 DC bus에 연결될 수 있으며, 두 bus(`bus0`, `bus1`)사이를 연결하여 전력을 흐르게 한다. 선로의 전력흐름은 직접적으로 제어할 수 없으며, 키르히호프 전압 법칙에 따라 수동적으로 결정된다.

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 170px;">
  <col style="width: 450px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <thead>
    <tr>
      <th style="text-align: center;">속성(attribute)</th>
      <th style="text-align: left;">설명</th>
      <th style="text-align: center;">기본값</th>
      <th style="text-align: center;">자료형</th>
      <th style="text-align: center;">입출력 구분</th>
      <th style="text-align: center;">단위</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">name</code></td>
      <td style="text-align: left;">선로 명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">bus0</code></td>
      <td style="text-align: left;">선로의 시작점 버스 명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">bus1</code></td>
      <td style="text-align: left;">선로의 종단점 버스 명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">candidate</code></td>
      <td style="text-align: left;">후보설비 판단 (T: 후보설비를 의미, F: 후보설비가 아님)</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">boolean</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">x</code></td>
      <td style="text-align: left;">직렬 리액턴스 (AC 선로에서 x는 0이 될 수 없음)</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">Ω</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">r</code></td>
      <td style="text-align: left;">직렬 저항</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">Ω</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">g</code></td>
      <td style="text-align: left;">션트 컨덕턴스로, 션트 어드미턴스의 실수부</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">S</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">b</code></td>
      <td style="text-align: left;">션트 서셉턴스로, 션트 어드미턴스의 허수부</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">S</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">x_pu</code></td>
      <td style="text-align: left;">리액턴스의 p.u.</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">r_pu</code></td>
      <td style="text-align: left;">저항의 p.u.</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">b_pu</code></td>
      <td style="text-align: left;">션트 서셉턴스의 p.u.</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">g_pu</code></td>
      <td style="text-align: left;">션트 컨덕턴스의 p.u.</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">start_date</code></td>
      <td style="text-align: left;">설비의 운영 시작일</td>
      <td style="text-align: center;">2000-01-01 12:00:00</td>
      <td style="text-align: center;">datetime</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">lifetime</code></td>
      <td style="text-align: left;">설비 수명</td>
      <td style="text-align: center;">100</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">years</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">length</code></td>
      <td style="text-align: left;">선로 길이 (type이 지정된 경우에 사용되며, CAPEX를 계산할 때 활용 됨)</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">km</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">carrier</code></td>
      <td style="text-align: left;">선로 유형(e.g., AC)</td>
      <td style="text-align: center;">AC</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">type</code></td>
      <td style="text-align: left;">선로의 표준 유형</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">v_ang_min</code></td>
      <td style="text-align: left;">선간 최소 위상 차</td>
      <td style="text-align: center;">-inf</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">Degrees</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">v_ang_max</code></td>
      <td style="text-align: left;">선간 최대 위상 차</td>
      <td style="text-align: center;">inf</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">Degrees</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">capital_cost</code></td>
      <td style="text-align: left;">1MVA 용량 당 건설 비용</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/MVA</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">fom</code></td>
      <td style="text-align: left;">고정운영비용</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">KRW/MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">num_parallel</code></td>
      <td style="text-align: left;">병렬 회선 수 (type가 비어 있으면, 이 값은 무시됨)</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">s_nom</code></td>
      <td style="text-align: left;"> 선로의 피상전력 크기로, 실제로 흐를 수 있는 최대 전력량</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MVA</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">s_nom_min</code></td>
      <td style="text-align: left;">s_nom_extendable = True에서 확장 가능한 최소 용량</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MVA</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">s_nom_max</code></td>
      <td style="text-align: left;">s_nom_extendable = True에서 확장 가능한 최대 용량</td>
      <td style="text-align: center;">inf</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MVA</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">bin_install</code></td>
      <td style="text-align: left;">후보 선로의 건설 유무</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">int</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p0</code></td>
      <td style="text-align: left;">bus0에서 선로로 흐르는 유효전력</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">q0</code></td>
      <td style="text-align: left;">bus0에서 선로로 흐르는 무효전력</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MVar</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p1</code></td>
      <td style="text-align: left;">선로에서 bus1 로 흐르는 유효전력</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">q1</code></td>
      <td style="text-align: left;">선로에서 bus1 로 흐르는 무효전력</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MVar</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">x_pu_eff</code></td>
      <td style="text-align: left;">선로의 리액턴스 p.u.</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">r_pu_eff</code></td>
      <td style="text-align: left;">선로의 저항 p.u.</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">s_max_pu</code></td>
      <td style="text-align: left;">선로에 흐를 수 있는 최대 전력의 비율</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">mu_lower</code></td>
      <td style="text-align: left;">선로 용량 하한 제약에 대한 shadow price</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW/MVA</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">mu_upper</code></td>
      <td style="text-align: left;">선로 용량 상한 제약에 대한 shadow price</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW/MVA</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">s_nom_opt</code></td>
      <td style="text-align: left;">최적화된 피상전력</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MVA</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">annuity_factor</code></td>
      <td style="text-align: left;">연가화 비율</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_financing_year</code></td>
      <td style="text-align: left;">금융조달기간</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">year</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">build_cost</code></td>
      <td style="text-align: left;">건설비용</td>
      <td style="text-align: center;">False</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
  </tbody>
</table>

* `link`는 두 버스(`bus0`, `bus1`) 사이에서 제어 가능한 방향성 에너지 흐름을 모델링한다. 여기서 `link`는 다른 `carrier`를 가질 수 있으며, 손실 또는 한계비용을 포함할 수 있다. `link`는 제어 가능한 전력 흐름을 갖는 모든 요소에 사용할 수 있으며, 열 펌프, 전해조, 단방향 HVDC, 양방향 HVDC로 모델링 할 수 있다. `link`는 무효전력을 생산하거나 소비하지 않는다.

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 170px;">
  <col style="width: 450px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <col style="width: 120px;">
  <thead>
    <tr>
      <th style="text-align: center;">속성(attribute)</th>
      <th style="text-align: left;">설명</th>
      <th style="text-align: center;">기본값</th>
      <th style="text-align: center;">자료형</th>
      <th style="text-align: center;">입출력 구분</th>
      <th style="text-align: center;">단위</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">name</code></td>
      <td style="text-align: left;">link 명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">bus0</code></td>
      <td style="text-align: left;">Link의 시작점 버스 명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">bus1</code></td>
      <td style="text-align: left;">Link의 종단점 버스 명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">type</code></td>
      <td style="text-align: left;">Link 표준 유형</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">efficiency</code></td>
      <td style="text-align: left;">bus0에서 bus1로의 전력 흐름 효율 (snapshot에 따라 변할 수 있음</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">carrier</code></td>
      <td style="text-align: left;">Link를 통해 전달되는 전력 흐름 유형 (e.g., HVDC는 DC로 표현)</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">lifetime</code></td>
      <td style="text-align: left;">설비 수명</td>
      <td style="text-align: center;">100</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">year</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_operation_year</code></td>
      <td style="text-align: left;">설비 최소 가동 연도</td>
      <td style="text-align: center;">100</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">year</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_nom</code></td>
      <td style="text-align: left;">Link에 흐를 수 있는 유효전력 용량(limit)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_set</code></td>
      <td style="text-align: left;">PF에서 p0 방향의 급전 설정값</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_min_pu</code></td>
      <td style="text-align: left;">최소 급전 p.u. (음수값이면, 역방향 전력흐름 허용)</td>
      <td style="text-align: center;">-1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u. of p_nom</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_max_pu</code></td>
      <td style="text-align: left;">최대 급전 p.u. (음수값이면, 역방향 전력흐름 허용)</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u. of p_nom</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">marginal_cost</code></td>
      <td style="text-align: left;">bus0에서 bus1방향으로 1MWh 전송시 한계비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u./MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">stand_by_cost</code></td>
      <td style="text-align: left;">전력흐름이 0일 때(link가 대기상태)의 운영비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u./h</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">length</code></td>
      <td style="text-align: left;">Link의 선로 길이(capital cost계산시 사용)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">km</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">terrain_factor</code></td>
      <td style="text-align: left;">지형 요인에 따른 자본비용 증가 요인</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">start_up_cost</code></td>
      <td style="text-align: left;">기동 비용(committable =True에서만 작동)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">shut_down_cost</code></td>
      <td style="text-align: left;">정지 비용 (committable =True에서만 작동)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_up_time</code></td>
      <td style="text-align: left;">설비가 켜져 있어야 하는 최소한의 snapshots 수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">int</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">snapshots</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_down_time</code></td>
      <td style="text-align: left;">설비가 꺼져 있어야 하는 최소한의 snapshots 수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">int</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">snapshots</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">up_time_before</code></td>
      <td style="text-align: left;">계획기간 이전에 발전기가 켜져 있었던 snapshots 수 (committable =True이고, min_up_time ≠0에서만 동작)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">int</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">snapshots</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">down_time_before</code></td>
      <td style="text-align: left;">계획기간 이전에 발전기가 꺼져 있었던 snapshots 수(committable =True이고, min_down_time ≠0에서만 작동)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">int</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">snapshots</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">ramp_limit_up</code></td>
      <td style="text-align: left;">최대 출력 증가율(nan인 경우 미작동)</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">ramp_limit_down</code></td>
      <td style="text-align: left;">최대 출력 감소율(nan인 경우 미작동)</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">ramp_limit_start_up</code></td>
      <td style="text-align: left;">최대 출력 증가율 (committable =True에서만 작동)</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">ramp_limit_shut_down</code></td>
      <td style="text-align: left;">최대 출력 감소율 (committable =True에서만 작동)</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p0</code></td>
      <td style="text-align: left;">bus0에서 link로 흐르는 유효전력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p1</code></td>
      <td style="text-align: left;">link에서 bus1 로 흐르는 유효전력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_nom_opt</code></td>
      <td style="text-align: left;">최적화된 유효전력 용량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">status</code></td>
      <td style="text-align: left;">발전기 상태 (1: 기동, 0: 정지) (committable =True에서만 동작)</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">status_startup</code></td>
      <td style="text-align: left;">기동여부 (1 is on, or 0 is off)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">status_shutdown</code></td>
      <td style="text-align: left;">정지여부 (1 is on, or 0 is off)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">mu_lower</code></td>
      <td style="text-align: left;">p_nom의 하한제약 그림자 가격</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u./MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">mu_upper</code></td>
      <td style="text-align: left;">p_nom의 상한제약 그림자 가격</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u./MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">mu_p_set</code></td>
      <td style="text-align: left;">고정 송전량(p_set)의 그림자 가격</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u./MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">mu_ramp_limit_up</code></td>
      <td style="text-align: left;">최대 출력증가율의 그림자 가격</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u./MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">mu_ramp_limit_down</code></td>
      <td style="text-align: left;">최대 출력증가율의 그림자 가격</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">p.u./MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">candidate</code></td>
      <td style="text-align: left;">후보설비 판단 (T: 후보설비를 의미, F: 후보설비가 아님)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">boolean</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">capital_cost</code></td>
      <td style="text-align: left;">1MW의 용량 당 자본 비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u./MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">start_date</code></td>
      <td style="text-align: left;">설비 운영 시작일</td>
      <td style="text-align: center;">2000-01-01 12:00:00</td>
      <td style="text-align: center;">datetime</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">end_date</code></td>
      <td style="text-align: left;">설비 운영 종료일</td>
      <td style="text-align: center;">2100-01-01 12:00:00</td>
      <td style="text-align: center;">datetime</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">committable</code></td>
      <td style="text-align: left;">급전 가능 여부 (T: 급전가능, F: 급전불가능)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">boolean</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">qhc</code></td>
      <td style="text-align: left;">link 출력과 소비열량의 관계를 나타내는 2차의 입출력 특성곡선식의 2차계수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">Gcal/MWh2</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">lhc</code></td>
      <td style="text-align: left;">link 출력과 소비열량의 관계를 나타내는 2차의 입출력 특성곡선식의 1차계수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">Gcal/MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nlhc</code></td>
      <td style="text-align: left;">발전기 출력과 소비열량의 관계를 나타내는 2차의 입출력 특성곡선식의 상수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (필수)</td>
      <td style="text-align: center;">Gcal/h</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">agc_max_pu</code></td>
      <td style="text-align: left;">자동발전제어서비스 최대 제공 용량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">agc_min_pu</code></td>
      <td style="text-align: left;">자동발전제어서비스 최소 제공 용량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">gf_max_pu</code></td>
      <td style="text-align: left;">주파수추종서비스 응답가능 최대 용량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">gf_min_pu</code></td>
      <td style="text-align: left;">주파수추종서비스 응답가능 최소 용량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nb_0</code></td>
      <td style="text-align: left;">계획기간 이전에 건설된 설비의 개수</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">no</code></td>
      <td style="text-align: left;">해당 시점까지 운영중인 설비 개수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nb</code></td>
      <td style="text-align: left;">해당 시점에 구축된 설비 개수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">nr</code></td>
      <td style="text-align: left;">해당 시점까지 퇴출되어 온 설비 개수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_built</code></td>
      <td style="text-align: left;">최대 구축 가능한 개수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_built</code></td>
      <td style="text-align: left;">최소 구축해야 하는 개수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_units</code></td>
      <td style="text-align: left;">최대 운영가능한 개수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">min_units</code></td>
      <td style="text-align: left;">최소한 운영되어야 하는 개수</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">number</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_capacity</code></td>
      <td style="text-align: left;">최대 설치용량</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">forced_rate</code></td>
      <td style="text-align: left;">고장률</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">maintenance_rate</code></td>
      <td style="text-align: left;">유지보수율</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">sfc</code></td>
      <td style="text-align: left;">열량가격당 기동연료비</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/Gcal</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">fuel_cost</code></td>
      <td style="text-align: left;">열량가격</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/Gcal</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">parent_unit</code></td>
      <td style="text-align: left;">발전기의 정보가 부족한 경우 기존의 발전기 특성을 가져올 때 해당 발전기 명</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">string</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">fom</code></td>
      <td style="text-align: left;">연간 고정 운영비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">KRW/MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_ru</code></td>
      <td style="text-align: left;">상향 예비력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">p_rd</code></td>
      <td style="text-align: left;">하향 예비력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">gen_cost</code></td>
      <td style="text-align: left;">발전비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">won</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">capacity_factor</code></td>
      <td style="text-align: left;">연간 용량 기여율</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">static, series</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">hurdle_rate</code></td>
      <td style="text-align: left;">최소 이용률</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">ratio</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">reserve_reg</code></td>
      <td style="text-align: left;">1차예비력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">reserve_pri</code></td>
      <td style="text-align: left;">주파수제어예비력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">reserve_sec</code></td>
      <td style="text-align: left;">2차 예비력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">reserve_ter</code></td>
      <td style="text-align: left;">3차 예비력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">reserve_frs</code></td>
      <td style="text-align: left;">속응성 예비력</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">MW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">annuity_factor</code></td>
      <td style="text-align: left;">연가화 비율</td>
      <td style="text-align: center;">1</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">p.u.</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">max_financing_year</code></td>
      <td style="text-align: left;">금융조달기간</td>
      <td style="text-align: center;">NaN</td>
      <td style="text-align: center;">float</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">year</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">retirement_cost</code></td>
      <td style="text-align: left;">설비폐지 시 요구되는 미납된 설비투자비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">gen_startup_cost</code></td>
      <td style="text-align: left;">기동비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">gen_shutdown_cost</code></td>
      <td style="text-align: left;">정지비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">build_cost</code></td>
      <td style="text-align: left;">건설비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">fixed_cost</code></td>
      <td style="text-align: left;">고정비용</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">series</td>
      <td style="text-align: center;">Output</td>
      <td style="text-align: center;">KRW</td>
    </tr>
    <tr>
      <td style="text-align: center;"><code style="word-break: break-all;">cyclic_state</code></td>
      <td style="text-align: left;">대표일들 사이에서 각 대표일의 초기값과 후기값 연결 여부를 표시 (T : 연결, F : 분리)</td>
      <td style="text-align: center;">0</td>
      <td style="text-align: center;">boolean</td>
      <td style="text-align: center;">Input (선택 옵션)</td>
      <td style="text-align: center;">NaN</td>
    </tr>
  </tbody>
</table>

## Unit Conventions

* OPEN내에서 광범위하게 사용하고 있는 주요 데이터의 단위는 아래 표와 같다.

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 250px;">
  <col style="width: 300px;">
  <thead>
    <tr>
      <th style="text-align: center;">항목</th>
      <th style="text-align: center;">단위</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;">전력(Power)</td>
      <td style="text-align: center;">MW, MVA, MVar</td>
    </tr>
    <tr>
      <td style="text-align: center;">에너지(Energy)</td>
      <td style="text-align: center;">MWh</td>
    </tr>
    <tr>
      <td style="text-align: center;">시간(Time)</td>
      <td style="text-align: center;">h</td>
    </tr>
    <tr>
      <td style="text-align: center;">전압(Voltage)</td>
      <td style="text-align: center;">kV</td>
    </tr>
    <tr>
      <td style="text-align: center;">위상각(Angle)</td>
      <td style="text-align: center;">rad</td>
    </tr>
    <tr>
      <td style="text-align: center;">임피던스(Impedance)</td>
      <td style="text-align: center;">Ω</td>
    </tr>
    <tr>
      <td style="text-align: center;">온실가스 배출량(CO2-equivalent emissions)</td>
      <td style="text-align: center;">tonCO2/MWh</td>
    </tr>
  </tbody>
</table>

* 단위법(p.u.)은 어떤 양을 나타내는데 절대량이 아닌 기준량에 대한 비로 나타내는 방법이다. OPEN에서는 일부 데이터에 대해 전압, 임피던스, 용량 등을 단위법으로 표현하며, 각 `component`에 따라 기준값이 다르게 적용된다.

## Key naming rule of OPEN
* OPEN은 일반적인 전력시스템에서 사용되는 다양한 연료원(`carrier`)을 지원하며, 사용자는 전력시스템에서 설비에 따른 여러 carrier를 직접 생성 혹은 수정하여 사용할 수 있다. OPEN에서 기본적으로 제공하는 연료원별 코드명은 아래표와 같으며, 사용자는 정의한 `carrier`를 준수하여 입력파일을 사용해야 한다. OPEN에서 정의한 `carrier`에 대한 naming rule을 준수하지 않을 경우 OPEN은 해당 연료원을 인식할 수 없어 오류가 발생한다. 발전기나 저장장치의 `carrier`속성에 입력할 수 있는 모든 연료원은 반드시 아래 명칭을 따라야 한다.

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 250px;">
  <col style="width: 300px;">
  <thead>
    <tr>
      <th style="text-align: center;">연료원</th>
      <th style="text-align: center;">OPEN 코드명 (carrier)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;">원자력</td>
      <td style="text-align: center;">nuclear</td>
    </tr>
    <tr>
      <td style="text-align: center;">소형 원자로</td>
      <td style="text-align: center;">nuclear-smr</td>
    </tr>
    <tr>
      <td style="text-align: center;">석탄</td>
      <td style="text-align: center;">coal</td>
    </tr>
    <tr>
      <td style="text-align: center;">LNG</td>
      <td style="text-align: center;">LNG</td>
    </tr>
    <tr>
      <td style="text-align: center;">LNG 열병합</td>
      <td style="text-align: center;">LNG-chp</td>
    </tr>
    <tr>
      <td style="text-align: center;">수력</td>
      <td style="text-align: center;">hydro</td>
    </tr>
    <tr>
      <td style="text-align: center;">바이오중유</td>
      <td style="text-align: center;">bioheavyoil</td>
    </tr>
    <tr>
      <td style="text-align: center;">바이오에너지</td>
      <td style="text-align: center;">bioenergy</td>
    </tr>
    <tr>
      <td style="text-align: center;">유류</td>
      <td style="text-align: center;">oil</td>
    </tr>
    <tr>
      <td style="text-align: center;">석탄가스화(IGCC)</td>
      <td style="text-align: center;">igcc</td>
    </tr>
    <tr>
      <td style="text-align: center;">태양광</td>
      <td style="text-align: center;">solar</td>
    </tr>
    <tr>
      <td style="text-align: center;">육상풍력</td>
      <td style="text-align: center;">onwind</td>
    </tr>
    <tr>
      <td style="text-align: center;">고정식 해상풍력</td>
      <td style="text-align: center;">offwind-fixed</td>
    </tr>
    <tr>
      <td style="text-align: center;">부유식 해상풍력</td>
      <td style="text-align: center;">offwind-floating</td>
    </tr>
    <tr>
      <td style="text-align: center;">암모니아 혼소</td>
      <td style="text-align: center;">coal-ammonia 50</td>
    </tr>
    <tr>
      <td style="text-align: center;">암모니아 전소</td>
      <td style="text-align: center;">coal-ammonia 100</td>
    </tr>
    <tr>
      <td style="text-align: center;">수소 혼소</td>
      <td style="text-align: center;">LNG-H2 50</td>
    </tr>
    <tr>
      <td style="text-align: center;">수소 전소</td>
      <td style="text-align: center;">LNG-H2 100</td>
    </tr>
    <tr>
      <td style="text-align: center;">양수</td>
      <td style="text-align: center;">PHS</td>
    </tr>
    <tr>
      <td style="text-align: center;">저장장치<small>(방전시간 X시간)</small></td>
      <td style="text-align: center;">battery-Xh<br><small>(X = 최대 방전시간)</small></td>
    </tr>
    <tr>
      <td style="text-align: center;">연료전지</td>
      <td style="text-align: center;">fuelcell</td>
    </tr>
    <tr>
      <td style="text-align: center;">해양</td>
      <td style="text-align: center;">marine</td>
    </tr>
  </tbody>
</table>

## What is scenario file

* 시나리오에 대한 정보로는 대표적으로 계획기간, 입력파일의 경로(고정 입력데이터, 시나리오 입력 데이터), 솔버 옵션, 시나리오의 제약조건 및 후보설비 정보, 연료전환 계획 등을 포함하고 있다. OPEN은 다양한 시나리오의 정보를 yaml 형식으로 하나의 파일을 통해 관리할 수 있도록 지원한다. yaml 형식의 파일은 들여쓰기와 key-value 쌍으로 이루어져 있는데, 사용자는 이를 통해 단순성과 가독성을 높여 손 쉽게 시나리오를 설정할 수 있다. 시나리오 정보에 대한 파일은 PowerGrid/resources 경로에 위치하며, 설명을 위해 시나리오 정보를 담은 예제 파일을 config_test.yaml로 정의한다.
  
    > **:loudspeaker: 주의사항**
    > <small>
    > - 시나리오 정보 파일의 경로는 고정이며, 파일명은 사용자가 정의할 수 있다.
    > - 아래 내용부터는 시나리오 정보 파일에서 시나리오 정보에 따른 key-value를 설명한다. OPEN 실행을 위해 key에 따른 value가 적절한 형식으로 반드시 작성되어야 한다. 그러나 (optional)이라고 적혀 있는 key는 사용자 편의를 위해 추가적으로 제공하는 기능이기 때문에 해당 기능이 필요할 때만 value를 입력하면 된다.
    > </small>

* 계획기간 설정
  - OPEN에서 실행하고자 하는 장기전원계획 혹은 단기운영계획의 계획기간을 설정한다. 계획기간의 시작일 key는 start_date, 계획기간의 종료일은 end_date이다. 이 때 end_date는 계획기간의 종료일에서 1일 뒤의 시점을 작성해야 한다. 두 key의 value를 작성할 때, 사용자는 yyyy-mm-dd형식으로 작성해야 한다.
  
    > **:mag_right: 참고사항**
    > <small>
    > - `inclusive`는 특정시점의 경계값을 포함할지 여부를 지정하는 옵션으로, left는 종료일 당일은 포함하지 않는 것을 의미한다. 앞서 설명했듯이, end_date는 계획기간 종료일에서 1일 뒤의 옵션을 적어야 하므로, 해당 key는 무시하도록 한다.
    > </small>
    ```python
      snapshots:
        start: 2024-01-01
        end: 2051-01-01
        inclusive: 'left'
    ```

* 할인율 설정
  * OPEN에서 필요한 비용을 계산할 때는 미래비용을 현재가치로 환산하는 과정을 거친다. 이를 위해 `discount_rate`에 사용하고자 하는 할인율을 비율값(ratio)로 입력해야 한다.
  ```python
    discount_rate : 0.045
  ```

* 대표년도
  - 할인율 계산을 적용하는 기준년도는 `basis_year`에 입력해야 한다.
  - 장기전원계획에서 계획기간내 대표년도를 year_list에 입력해야 한다. 작성형식은 yyyy이며, 계획기간을 벗어나는 연도를 작성할 수 없다.

* 입력파일 경로 및 시나리오명 지정
  *	입력데이터 중에서 고정 데이터의 폴더명은 `csv_folder_name`에 입력하고, 시나리오 폴더의 경로는 `{input:scenarios}`에 입력한다.
  *	사용자가 정의한 시나리오 명은 scenario_name에 입력해야 하며, 향후 OPEN의 결과는 `scenario_name`과 같은 이름의 폴더에서 제공된다.
 
* *(optional)* 모델 결과를 수신하고자 하는 이메일 계정 입력
  *	OPEN 실행시 진행 상황에 대해 이메일로 수신하고자 하는 경우, 사용자의 Gmail계정 정보를 시나리오 설정 파일에 입력해야 한다. 이메일 주소는 `{send_email:email_address}`에, 비밀번호는 `{send_email:password}`에 입력해야 한다. 이때, `password`에는 일반 로그인용 비밀번호가 아닌, 앱 비밀번호를 입력해야 한다.
    > **:mag_right: 참고사항**
    > <small> Google 계정 → 보안 → [앱 비밀번호 생성](https://support.google.com/accounts/answer/185833)
    > </small>

* *(optional)* 후보 설비 생성
  * 장기전원계획 수립에 있어 후보설비 건설을 결정할 때 후보설비의 목록을 생성하는 방법은 입력파일(csv 형식) 혹은 시나리오 정보 파일(yaml형식)을 이용해야 한다. 후보설비를 설정하는 자세한 방법은 후보설비 시나리오에서 확인할 수 있으며, 여기서는 시나리오 정보 파일을 이용할 때 사용하는 key-value의 의미에 대해서만 다룬다.
  * `{electricity:extendable_carriers}`에 후보설비를 입력하고자 하는 설비별 carrier를 입력해야 한다. 여기서 입력한 후보설비의 carrier는 모든 bus를 대상으로 정의된다.
 
  * 특정 bus에 특정 후보설비를 건설하는 것을 제한할 경우에는 `{electricity:excluded_buses}`에 건설을 희망하지 않는 bus를 입력해야 한다. 예를 들어, slack bus에 발전기 건설을 희망하지 않는 경우에는 아래 그림처럼 해당 bus를 입력해야 한다.
 
  * `{electricity:max_branches}`는 후보 송전선로의 최대 건설 가능 선로 수를 의미한다.
  * 앞서 `{electricity:extendable_carriers}`에서 입력한 후보설비의 `carrier`에 대한 정보를 입력해주는 과정이 반드시 필요하다. 이를 위해 `extendable_carriers`에 정의한 각 후보설비의 `carrier`별 attribute, 제약조건을 `{electricity}` 블록 내에 key-value로 입력해야 한다.

* *(optional)* 연료전환
  * 장기전원계획에서 OPEN은 연료전환 경로 결정을 지원하며, 자세한 설정 방법은 연료전환 시나리오에서 확인할 수 있으며, 연료전환 설정에 있어 사용해야 하는 key-value의 의미에 대해서만 다룬다.
  * `{conversion:scheduled_conversion}`은 사용자가 국가계획이나 발전사의 계획 혹은 사나리오 설정 등 강제적인 연료전환계획 반영 여부를 나타낸다. 해당 key의 value를 True로 입력하면 연료전환 계획을 전원계획 수립에 있어 반드시 반영함을 의미하고, False로 입력하면 연료전환 계획을 전원계획 수립에 반영하지 않는 것을 의미한다.
  * 연료전환을 결정하고자 하는 대상 연료원(`carrier`)을 `{conversion:conversion_carriers}`의 value로 입력해야 한다. OPEN은 여기서 입력한 대상 연료원에 해당하는 발전기의 연료전환 경로를 내생적으로 결정하게 된다.
  * OPEN은 강제적인 연료전환 계획을 반영할 때, 연료전환 전 발전기와 연료전환 후 발전기에 대해 1:1로 매칭하여 연료전환 결정에 반영한다. 사용자의 시나리오 설정 방식에 따라 2개 이상의 호기가 하나의 설비로 연료전환이 되는 경우에는 1:1 매칭이 어려운데, 이 경우 연료전환 전 발전기들에 대해 1호기만 제외하고 남은 호기들은 `{conversion:excluded_units}`에 작성해야 한다(남은 호기는 무작위로 작성하면 됨). 예를 들어, 세 개의 석탄 발전기(A-1, A-2, A-3)가 하나의 LNG 발전소(B-1)로 LNG 발전기로 연료전환 하는 상황을 가정한다. 이 때 OPEN에서는 `{conversion:excluded_units}`에 [A-2, A-3]을 작성하면 된다.
  * 앞서 `conversion_carriers`에서 지정한 연료원의 설비가 연료전환을 할 수 있는 모든 경로를 지정해야 한다. 이를 위해 `{conversion:transferable_states}`의 하위 블록으로 연료전환 대상 연료원을 key값(연료전환 전 연료원)으로, 대상 연료원의 전환 경로를 value(연료전환 후 연료원)로 입력해야 한다. 예를 들어, 석탄이 연료전환 할 수 있는 경로가 암모니아 혼소, LNG, 수소 전소라면 아래 그림처럼 `{coal:[coal-ammonia 50, LNG, H2 100]}`을 입력해야 한다.
  * `{conversion:clustered:activate}`는 개별 설비 단위가 아닌 bus단위로 동일 `carrier` 발전기를 묶어서 연료전환을 고려하고자 할 때 사용한다. `carrier`를 key값으로, bus 단위로 묶고자 할 경우에는 value를 True로 입력한 key-value를 `activate`의 하위블록으로 입력한다(개별 설비 단위로 연료전환을 고려할 때 value는 False를 입력).
  * `{conversion:common}`은 모든 연료전환 후 발전기에 대해 공통적으로 적용하고자 하는 attribute 혹은 제약조건의 key-value를 블록으로 넣어준다. 이를 통해 연료전환 후 설비들은 입력한 key-value를 일괄적으로 적용 받는다.
  * 앞서 `{conversion:transferable_states}`를 통해 작성한 모든 연료전환 경로에 대해 경로별 연료전환 정보를 에 `{conversion:연료전환 전 연료원:연료전환 후 연료원}입력해야 한다. 여기서 연료전환 전 연료원은 `{`conversion:transferable_states}`의 key값(연료전환 전 연료원)을, 연료전환 후 연료원은 `{conversion:transferable_states}`의 value(연료전환 후 연료원)를 의미한다. 주의해야 할 것은 `{conversion:transferable_states}`에서 작성한 방식과 동일하게 key값(`{conversion:연료전환 전 연료원}`)을 중심으로 연료전환 경로의 연료원을 value로 입력하되, 연료전환 정보는 value의 하위로 key-value를 입력해야 한다. 사용자가 입력해야 하는 연료전환 경로에 대한 정보는 아래 표와 같다.

<table style="width: 100%; table-layout: fixed;">
  <col style="width: 200px;">
  <col style="width: 450px;">
  <col style="width: 300px;">

  <thead>
    <tr>
      <th style="text-align: center;">연료전환 정보 key</th>
      <th style="text-align: center;">연료전환 정보 value의 데이터 타입 및 형식</th>
      <th style="text-align: center;">설명</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style="text-align:center;"><code>activate</code></td>
      <td style="text-align:center;">Boolean (True/False)</td>
      <td style="text-align:left;">해당 연료전환 경로 활성화 여부</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code>start_date</code></td>
      <td style="text-align:center;">Datetime (yyyy-mm-dd)</td>
      <td style="text-align:left;">연료전환 후 연료원의 운영 시작일</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code>lifetime</code></td>
      <td style="text-align:center;">Integer (years)</td>
      <td style="text-align:left;">연료전환 후 연료원의 수명</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code>min_operaton_year</code></td>
      <td style="text-align:center;">Integer (years)</td>
      <td style="text-align:left;">연료전환 후 연료원의 최소 운영 기간</td>
    </tr>
    <tr>
      <td style="text-align:center;"><code>parent_unit</code></td>
      <td style="text-align:center;">String</td>
      <td style="text-align:left;">
        연료전환 후 연료원의 속성을 상속받을 기존 설비명을 지정.<br>
        미사용 시 <code>generators.csv</code>처럼 carrier 관련 모든 attribute를 별도로 입력해야 함.
      </td>
    </tr>
    <tr>
      <td style="text-align:center;"><code>capital_cost</code></td>
      <td style="text-align:center;">Integer (KRW/MW)</td>
      <td style="text-align:left;">연료전환에 따른 건설 비용</td>
    </tr>
  </tbody>
</table>

  * 사용자가 강제적으로 지정하고자 하는 특정 설비에 대한 연료전환 계획 정보는 `{conversion:scheduled}`에 입력해야 한다. 지정하고하는 설비를 key로, 해당 설비의 연료전환 정보는 해당 key의 하위에 key-value로 입력해야 한다. Key를 입력할 때 `generators.csv`의 `name`과 반드시 일치해야 한다. 사용자가 입력해야 하는 연료전환 경로 정보는 아래 표와 같다.
    > **:loudspeaker: 주의사항**
    > <small>
    > - 연료원을 `carrier`에 작성할 때, 정의한 naming rule을 반드시 지켜야 한다.
    > </small>

    <table style="width: 100%; table-layout: fixed;">
      <col style="width: 200px;">
      <col style="width: 450px;">
      <col style="width: 300px;">

      <thead>
        <tr>
          <th style="text-align: center;">연료전환 정보 key</th>
          <th style="text-align: center;">연료전환 정보 value의 데이터 타입 및 형식</th>
          <th style="text-align: center;">의미</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="text-align:center;"><code>bus</code></td>
          <td style="text-align:center;">Integer (bus)</td>
          <td style="text-align:left;">연료전환 후 건설되어야 할 설비의 위치</td>
        </tr>
        <tr>
          <td style="text-align:center;"><code>carrier</code></td>
          <td style="text-align:center;">Integer (carrier)</td>
          <td style="text-align:left;">연료전환 후 설비의 연료원</td>
        </tr>
        <tr>
          <td style="text-align:center;"><code>start_date</code></td>
          <td style="text-align:center;">Datetime (yyyy-mm-dd)</td>
          <td style="text-align:left;">연료전환 후 설비의 운영 시작일</td>
        </tr>
        <tr>
          <td style="text-align:center;"><code>p_nom</code></td>
          <td style="text-align:center;">Integer (MW)</td>
          <td style="text-align:left;">연료전환 후 설비의 용량</td>
        </tr>
        <tr>
          <td style="text-align:center;"><code>capital_cost</code></td>
          <td style="text-align:center;">Integer (KRW/MW)</td>
          <td style="text-align:left;">연료전환에 따른 건설 비용</td>
        </tr>
      </tbody>
    </table>

* 클러스터링 - 장기전원계획
  * `{clustering:plannning}`의 하위블록에 해당하는 key-value를 통해 장기전원계획을 위한 계획기간의 대표일 클러스터링을 수행한다. 아래 설명은 클러스터링 설정을 위한 key와 그에 상응하는 value 형식에 대해 다룬다.
  * `clusters_num`은 클러스터링 수를 의미한다. Value는 정수만 입력할 수 있다.
  * `connected_length`는 클러스터링 당 일수를 의미한다. Value는 정수만 입력할 수 있다.
  * `selected_snapshots`는 대표일 추출을 위한 클러스터링 기법을 의미한다. value로는 `min_err_from_mean`과 `extreme` 중에 선택하여 입력해야 한다. `min_err_from_mean`은 clustering 된 날짜 중 평균값에 가장 오차가 작은 날짜를 선택한다. `extreme`은 하루중 최대값과 최소값의 차이가 가장 큰 날짜 중에 상위 x%에 대해 대표일을 선정하는 방법이다. extreme을 사용할 때 x에 대한 값은 rank에 입력해야 한다. rank에 value가 채워져 있더라도, `{selected_snapshots:min_err_from_mean}`이라면 `rank`는 무의미하다.
  * `algorithm` 은 전력수요와 재생에너지를 클러스터링 하는 알고리즘을 의미한다. OPEN은 k-means clustering 기법을 지원하고 있으며, kmeans를 입력해야 한다. 현재 OPEN은 k-means clustering 기법만 지원하고 있으나, 향후 다른 클러스터링 알고리즘을 추가 지원할 예정이다.
  * `specific_dates`는 대표일 추출에 있어 클러스터링 기법이 아닌 모든 연도에 대해 동일하게 특정 시점을 선택하고자 할 때 사용한다. 클러스터링 기법 대신 사용자가 대표일을 직접 선택하기 때문에 clusters_num의 수에 맞게 `specific_dates`에 값을 채워야 한다. value를 작성할 때 월, 일에 대한 정보를 입력해야 하며, mm-dd 형식으로 작성해야 한다.
  * `{clustering:operation}`의 하위블록에 해당하는 key-value를 통해 단기운영계획을 위한 계획기간의 대표일 클러스터링을 수행한다. 아래 설명은 클러스터링 설정을 위한 key와 그에 상응하는 value 형식에 대해 다룬다.
  * `clusters_num`은 클러스터링 수를 의미한다. Value는 정수만 입력할 수 있다.
  * `connected_length`는 클러스터링 당 일수를 의미한다. Value는 정수만 입력할 수 있다.
  * `selected_snapshots`는 대표일 추출을 위한 클러스터링 기법을 의미한다. value로는 `min_err_from_mean`과 `extreme` 중에 선택하여 입력해야 한다. `min_err_from_mean`은 clustering 된 날짜 중 평균값에 가장 오차가 작은 날짜를 선택한다. extreme은 하루중 최대값과 최소값의 차이가 가장 큰 날짜 중에 상위 x%에 대해 대표일을 선정하는 방법이다. `extreme`을 사용할 때 x에 대한 값은 rank에 입력해야 한다. rank에 value가 채워져 있더라도, `{selected_snapshots:min_err_from_mean}`이라면 `rank`는 무의미하다.
  * `based_on_net_load_profiles`은 부하패턴을 클러스터링 할 때 순부하와 총부하를 선택한다. 순부하로 클러스터링 하려면 value가 `True`로, 총부하로 클러스터링 하려면 value가 `False`로 입력되야 한다.
  * `independent_capacity_factor`는 재생에너지 발전의 대표시간을  결정한다. `False`로 입력하면 전력수요가 뽑혔던 대표시간을 그대로 사용하고, `True`는 재생에너지 패턴도 클러스터링 하여 대표시간을 추출한다.

* 최적화 옵션 - 장기전원계획
  * `planning`의 하위블록은 장기전원계획을 위한 옵션들을 나타낸다.
  * `activate`는 장기전원계획 문제의 풀이 유무를 결정한다. `True`를 입력하면 장기전원계획 문제를 풀지만, `False`를 입력할 경우 장기전원계획 문제를 풀지 않는다.
  * `step_length`는 장기전원계획의 문제 풀이 단위를 의미한다. OPEN은 연단위로 장기전원계획 문제를 지원하고 있기 때문에 year로 작성해야 한다.
  * `opt_window_length`는 장기전원계획 문제를 풀이할 때 동시에 문제를 푸는 기간을 의미한다. OPEN은 전체 계획기간에 대해 문제풀이 기간을 나눠서 풀 수 있는데, opt_window_length의 값에 문제 풀이기간이 나뉘어진다. `opt_window_length`는 정수형으로 입력해야 하고, 최대값은 year_list에서 작성한 value의 개수다. 예를 들어 앞서 year_list에 `[2025, 2030, 2035, 2040]`을 적었다면, `opt_window_length`는 4이하의 정수를 적어야 한다. `{opt_window_length:4}`라면, 2025, 2030, 2035, 2040년을 모두 한꺼번에 푸는 것을 의미하고, `{opt_window_length:2}`라면 2025, 2030년과 2035, 2040으로 2번에 나눠서 푸는 것을 의미한다.
  * `rolling_horizon`은 장기전원계획 문제를 풀 때 계획기간에 대해 Rolling horizon 방식 이용 유무를 나타낸다. `True`로 입력하면 Rolling horizon 방식을 이용하고, False로 입력하면 이용하지 않는다. 예를 들어,  `year_list = [2025, 2030, 2035, 2045]`, `opt_window_length =2`, `rolling_horizon=True`로 입력할 경우 [2025,2030], `[2030, 2035]`, [20345,2040]을 순차적으로 풀이하게 된다.
  * *(optional)* `year_list`는 앞서 작성했던 `year_list`(basic_year의 바로 다음줄에 위치) 대신 다른 값을 적용하고자 할 때 사용한다. 앞서 이미 `year_list`를 정의했기 때문에 빈 값으로 둬도 무방하며, 여기서 값을 입력하면 앞서 작성했던 값 대신 새롭게 정의한 연도를 사용하게 된다.
  * `annualized_capex`는 계획기간 동안 설비의 수명과 할인율을 이용해 건설비용의 연가화 적용 유무를 의미한다. `True`로 입력할 경우 연가화가 적용되며, False로 입력할 경우 연가화가 적용되지 않는다.
  * `ignore_screening`은 문제 풀이 과정에 있어 단기운영계획의 결과를 장기전원계획에 피드백을 줄지에 대한 유무를 의미한다. True는 단기운영계획의 결과가 장기전원계획에 영향을 주지 않고, False는 단기운영계획의 결과를 장기전원계획에 반영한다.
  * `flag_generator_screening`는 특정 연료원에 해당하는 발전기의 폐지 결정에 있어 최소 이용률에 따른 경제성 조건에 대해 적용 유무를 나타낸다. `True`면 폐지 결정에 있어 최소 이용률이 영향을 주고, `False`면 영향을 주지 않는다.
  * `flag_startup`은 발전기의 기동 비용 고려 유무를 나타낸다. `True`면 기동 비용을 고려하고, `False`면 기동 비용을 고려하지 않는다.
  * `flag_shutdown`은 발전기의 정지 비용 고려 유무를 나타낸다. `True`면 정지 비용을 고려하고, `False`면 정지 비용을 고려하지 않는다.
  * `flag_mut`는 발전기의 최소기동시간 고려 유무를 나타낸다. `True`면 최소기동시간을 고려하고, `False`면 최소기동시간을 고려하지 않는다.
  * `flag_mdt`는 발전기의 최소정지시간 고려 유무를 나타낸다. `True`면 최소정지시간을 고려하고, `False`면 최소정지시간을 고려하지 않는다.
  * `save_clustered_operation_results`는 단기운영계획의 최종 결과에 대한 저장 유무를 나타낸다. `True`면 결과를 저장하고, `False`면 저장하지 않는다.
  * `line_cap_name`은 입력데이터의 송전선로 용량에 대한 가중치를 나타낸다. Value는 `s_nom_long_term`(1.0배), `s_nom_short_term`(1.2배), `s_nom_emergency_term`(1.5배) 중에 선택하여 입력해야 한다.
  * `curtailment_ratio`는 출력제어 비율을 의미하며, 1 이하의 실수(float)를 입력해야 한다.
  * `curtail_target`에는 출력제어 대상 연료원(`carrier`)를 작성해야 한다.
  * `linearized_ramp_carriers`에는 선형화를 적용하고자 하는 대상 연료원 (`carrier`)을 작성해야 하며, 작성한 연료원의 `ramp_rate`는 `min_up_time`과 `min_down_time`을 고려해서 자동 조정된다.
  * `primary_emission_source_carriers`는 단기운영계획의 배출량 결과를 장기전원계획에서 반영할 때 더 강화된 배출량 제약을 업데이트 하기 위해 배출계수가 가장 높은 연료원(`carrier`)을 작성한다.
  * `secondary_emission_source_carriers`는 `primary_emission_source_carriers`에서 작성한 연료원을 제외한 나머지 온실가스 배출 연료원(carrier)를 작성한다. 
  * `decommission_threshold`는 경제성 확보를 위한 최소 이용률 기준 조건을 적용하여 발전기의 폐지를 결정할 때에 대한 구체적인 정보를 입력한다. 하위 블록에 최소 이용률 조건을 적용하고자 하는 연료원(`carrier`)을 key로, 해당 연료원의 기준 이용률(단위: %)을 value로 입력한다. `year_list`에는 조건을 적용하고자 하는 대표년도를 의미하며, yyyy 형식으로 입력해야 한다.
  * `hurdle_rate`는 장기전원계획에서 적용하고자 하는 연료원(`carrier`)의 최소 이용률을 의미하며, 대상 연료원을 key로 최소 이용률을 value(1이하의 실수형)로 입력해야 한다.
  * `{options:prallel}`은 최적화 문제 풀이에 있어 병렬 처리 선택 유무를 나타낸다. `True`는 병렬로 문제를 풀며, `False`는 병렬로 풀지 않는다. 이 옵션은 `run_GTEP`에서는 동작하지 않으며, `decomposition` 모듈에서만 동작한다.
  * `{options:reset_step_start}`는 대표일 내의 특정 변수의 초기값에 대해 초기화 유무를 나타낸다. `True`는 초기값을 특정 값으로 초기화하고, `False`는 초기화하지 않는다.
  * `{options:linearized_generators_expansion}`는 발전기의 건설, 운영, 폐지와 관련한 변수들의 선형화 유무를 나타낸다. `True`는 선형화를 하고, `False`는 선형화 하지 않는다.
  * `{options:linearized_storages_expansion}`는 저장징치의 건설, 운영, 폐지와 관련한 변수들의 선형화 유무를 나타낸다. `True`는 선형화를 하고, `False`는 선형화 하지 않는다.
  * `{options:linearized_branch_expansion}`는 송전 선로의 건설과 관련한 변수들의 선형화 유무를 나타낸다. `True`는 선형화를 하고, `False`는 선형화 하지 않는다.
  * `{options:linearized_generator_status}`는 발전기의 기동, 정지 상태 관련한 변수들의 선형화 유무를 나타낸다. `True`는 선형화를 하고, `False`는 선형화 하지 않는다.
  * `{options:linearized_storages_status}`는 저장장치의 충전 상태 관련한 변수들의 선형화 유무를 나타낸다. `True`는 선형화를 하고, `False`는 선형화 하지 않는다.
  * `{options:ignore_penalty_for_reserve}`는 예비력 제약에 대한 페널티 반영 여부를 나타낸다. `True`는 예비력 제약에 패널티를 반영하지 않고, `Fasle`는 반영하게 된다.
  * `{options:ignore_penalty_for_p_plus}`는 초과 발전량에 대한 페널티 반영 여부를 나타낸다. `True`는 초과 발전량에 대한 페널티를 반영하지 않고, `Fasle`는 반영하게 된다.
  * `{options:ignore_penalty_for_p_minus}`는 부하 공급 지장량에 대한 페널티 반영 여부를 나타낸다. `True`는 부하 공급 지장량에 페널티를 반영하지 않고, `Fasle`는 반영하게 된다.
  * `{options:simplified_residual_value}`는 설비의 폐지보상비용 산정을 위한 수식의 간소화 여부를 나타낸다. `True`는 수식을 간소화하여 폐지보상비용을 산정하고, `Fasle`는 간소화하지 않고 후보설비의 건설시점에 맞춰 폐지보상비용을 산정한다.
  * `{options:retirement_compensation_scale_down}`은 폐지보상비용의 크기를 줄이기 위한 비율을 나타낸다. Value로 작성한 크기의 역수로 폐지보상비용의 크기가 조정된다.
  * `{options:installed_reserve}`은 설비예비율(단위:p.u.)을 의미한다.
  * `{options:generator_production_cost_resolution}`은 발전기의 비용함수의 처리방식을 의미한다. 비용함수를 2차식으로 고려하면 qudaratic으로, 1차식으로 고려하면 linear로 입력해야 한다.
  * `{options:formulation}`은 조류계산 방식을 나타낸다. OPEN은 DC power flow formulation을 지원하고 있으며, `angle`로 입력해야 한다.
  * `{options:unit_commitment_variables_number}`은 기동정지계획에서 발전기의 상태를 표현하는 변수의 수를 의미한다. OPEN은 기동정지계획에서 상태, 기동, 정지 변수를 모두 사용하고 있기 때문에 `3`을 입력해야 한다.
  * `{options:storage_initial_state}`은 저장장치의 초기상태를 나타낸다. `half`는 저장용량의 50%에 해당하는 크기를 초기상태로 설정하는 것을 의미한다.
  * `{options:base_MVA}`은 단위법를 사용할 때 기준용량(단위: MVA)을 의미한다.
  * `{options:penalty_price_co2}`은 배출량에 대한 페널티 가격(단위: KRW/MtonCO2eq)을 나타낸다.
`{options:penalty_load}`은 부하공급지장비용 산정을 위한 페널티 가격(단위: KRW/MWh)을 나타낸다.
  * `{options:construction_max_delay}`은 연료전환을 고려할 때 최대 건설 지연 기간을 나타내며, 정수형으로 입력해야 한다.
  * `{options:solver_name}`은 최적화 풀이를 위한 solver를 나타낸다. CPLEX(상용 solver)를 사용하려면 `cplex`를 입력하고, GLPK(무료 solver)를 사용하려면 `glpk`를 입력해야 한다.
  * `{options:currency_unit}`는 최적화 풀이를 위해 비용의 크기를 조절할 때 사용한다.
  * `{options:reserve}`는 적용하고자 하는 운영예비력을 입력한다. 상향예비력은 `lump_reserve`, 하향예비력은 `lump_downward_reserve`으로 표기하며, 적용하고자 하는 운영예비력을 value로 작성해야 한다.
  * `{options:capacity_reserve}`는 연도별 설비예비력 요구량(단위:MW)를 나타낸다. 연도를 key(작성형식: yyyy)로, 요구량을 value로 작성해야 한다.
  * `{options:opex_yearly_weighted_coeff}`는 연도별 운영비용에 대한 가중치를 나타낸다. 연도를 key(작성형식: yyyy)로, 가중치를 value로 작성해야 한다.
  * `{options:capex_yearly_weighted_coeff}`는 연도별 건설비용에 대한 가중치를 나타낸다. 연도를 key(작성형식: yyyy)로, 가중치를 value로 작성해야 한다.

* 최적화옵션 - 단기운영계획
  * `operation`의 하위블록은 단기운영계획을 위한 옵션들을 나타낸다.
  * `activate`는 단기운영계획 문제의 풀이 유무를 결정한다. `True`를 입력하면 단기운영계획 문제를 풀지만, `False`를 입력할 경우 단기운영계획 문제를 풀지 않는다.
  * `step_length`는 단기운영계획의 문제 풀이 단위를 의미하며, 시간 단위로 작성해야 한다.
  * `opt_window_length`는 단기운영계획 문제를 풀이할 때 동시에 문제를 푸는 기간을 의미한다. OPEN은 전체 계획기간에 대해 문제풀이 기간을 나눠서 풀 수 있는데, `opt_window_length`의 값에 문제 풀이기간이 나뉘어진다. `opt_window_length`는 정수형으로 입력해야 하고, 최대값은 `year_list`에서 작성한 value의 개수다. 예를 들어 앞서 `year_list`에 `[2025, 2030, 2035, 2040]`을 적었다면, `opt_window_length`는 `4`이하의 정수를 적어야 한다. `{opt_window_length:4}`라면, 2025, 2030, 2035, 2040년을 모두 한꺼번에 푸는 것을 의미하고, `{opt_window_length:2}`라면 2025, 2030년과 2035, 2040으로 2번에 나눠서 푸는 것을 의미한다.
  * *(optional)* `year_list`는 앞서 작성했던 `year_list`(basic_year의 바로 다음줄에 위치) 대신 다른 값을 적용하고자 할 때 사용한다. 앞서 이미 `year_list`를 정의했기 때문에 빈 값으로 둬도 무방하며, 여기서 값을 입력하면 앞서 작성했던 값 대신 새롭게 정의한 연도를 사용하게 된다.
  * `flag_startup`은 발전기의 기동 비용 고려 유무를 나타낸다. `True`면 기동 비용을 고려하고, False면 기동 비용을 고려하지 않는다.
  * `flag_shutdown`은 발전기의 정지 비용 고려 유무를 나타낸다. `True`면 정지 비용을 고려하고, False면 정지 비용을 고려하지 않는다.
  * `flag_mut`는 발전기의 최소기동시간 고려 유무를 나타낸다. `True`면 최소기동시간을 고려하고, False면 최소기동시간을 고려하지 않는다.
  * `flag_mdt`는 발전기의 최소정지시간 고려 유무를 나타낸다. `True`면 최소정지시간을 고려하고, False면 최소정지시간을 고려하지 않는다.
  * `ignore_screening`은 문제 풀이 과정에 있어 단기운영계획의 결과를 장기전원계획에 피드백을 줄지에 대한 유무를 의미한다. `True`는 단기운영계획의 결과가 장기전원계획에 영향을 주지 않고, `False`는 단기운영계획의 결과를 장기전원계획에 반영한다.
  * `line_cap_name`은 입력데이터의 송전선로 용량에 대한 가중치를 나타낸다. Value는 `s_nom_long_term`(1.0배), `s_nom_short_term`(1.2배), `s_nom_emergency_term`(1.5배) 중에 선택하여 입력해야 한다.
  * `set_min_soc_initia`l은 저장장치의 초기값에 대해 최소값 설정 여부를 나타낸다. `True`는 저장장치의 최소값을 초기값으로 설정하고, `False`는 설정하지 않는다.
  * `curtailment_ratio`는 출력제어 비율을 의미하며, 1 이하의 실수(float)를 입력해야 한다.
  * `curtail_target`에는 출력제어 대상 연료원(`carrier`)를 작성해야 한다.
  * `linearized_ramp_carriers`에는 선형화를 적용하고자 하는 대상 연료원 (`carrier`)을 작성해야 하며, 작성한 연료원의 `ramp_rate`는 `min_up_time`과 `min_down_time`을 고려해서 자동 조정된다.
  * `distribution_method`는 전력수요의 설정 방식을 의미한다. 총 부하를 사용하고자 할 때 load를 입력하고, 순 부하를 사용할 때 netload를 입력한다.
  * `hurdle_rate`는 장기전원계획에서 적용하고자 하는 연료원(`carrier`)의 최소 이용률을 의미하며, 대상 연료원을 key로 최소 이용률을 value(1이하의 실수형)로 입력해야 한다.
  * `{options:prallel}`은 최적화 문제 풀이에 있어 병렬 처리 선택 유무를 나타낸다. `True`는 병렬로 문제를 풀며, `False`는 병렬로 풀지 않는다. 이 옵션은 `run_GTEP`에서는 동작하지 않으며, Decomposition 모듈에서만 동작한다.
  * `{options:reset_step_start}`는 대표일 내의 특정 변수의 초기값에 대해 초기화 유무를 나타낸다. `True`는 초기값을 특정 값으로 초기화하고, `False`는 초기화하지 않는다.
  * `{options:activate_LMP }`는 LMP(Locational Marginal Price)를 계산 여부를 나타낸다. `True`는 LMP를 계산하고, `False`는 계산하지 않는다.
  * `{options:activate_SMP}`는 SMP(System Marginal Price)를 계산 여부를 나타낸다. `True`는 SMP를 계산하고, `False`는 계산하지 않는다.
  * `{options:overlap_front}`는 SMP산정을 위해 대상일에서 포함할 앞 시간의 수를 의미한다.
  * `{options:overlap_behind}`는 SMP산정을 위해 대상일에서 포함할 뒷 시간의 수를 의미한다
  * `{options:storage_initial_state}`은 저장장치의 초기상태를 나타낸다. half는 저장용량의 50%에 해당하는 크기를 초기상태로 설정하는 것을 의미한다.
  * `{options:linearized_generators_expansion}`는 발전기의 건설, 운영, 폐지와 관련한 변수들의 선형화 유무를 나타낸다. `True`는 선형화를 하고, `False`는 선형화 하지 않는다.
  * `{options:linearized_storages_expansion}`는 저장징치의 건설, 운영, 폐지와 관련한 변수들의 선형화 유무를 나타낸다. `True`는 선형화를 하고, `False`는 선형화 하지 않는다.
  * `{options:linearized_branch_expansion}`는 송전 선로의 건설과 관련한 변수들의 선형화 유무를 나타낸다. `True`는 선형화를 하고, `False`는 선형화 하지 않는다.
  * `{options:linearized_generator_status}`는 발전기의 기동, 정지 상태 관련한 변수들의 선형화 유무를 나타낸다. `True`는 선형화를 하고, `False`는 선형화 하지 않는다.
  * `{options:linearized_storages_status}`는 저장장치의 충전 상태 관련한 변수들의 선형화 유무를 나타낸다. `True`는 선형화를 하고, `False`는 선형화 하지 않는다.
  * `{options:ignore_penalty_for_reserve}`는 예비력 제약에 대한 페널티 반영 여부를 나타낸다. `True`는 예비력 제약에 패널티를 반영하지 않고, Fasle는 반영하게 된다.
  * `{options:ignore_penalty_for_p_plus}`는 초과 발전량에 대한 페널티 반영 여부를 나타낸다. `True`는 초과 발전량에 대한 페널티를 반영하지 않고, Fasle는 반영하게 된다.
  * `{options:ignore_penalty_for_p_minus}`는 부하 공급 지장량에 대한 페널티 반영 여부를 나타낸다. `True`는 부하 공급 지장량에 페널티를 반영하지 않고, Fasle는 반영하게 된다.
  * `{options:simplified_residual_value}`는 설비의 폐지보상비용 산정을 위한 수식의 간소화 여부를 나타낸다. `True`는 수식을 간소화하여 폐지보상비용을 산정하고, `Fasle`는 간소화하지 않고 후보설비의 건설시점에 맞춰 폐지보상비용을 산정한다.
  * `{options:generator_production_cost_resolution}`은 발전기의 비용함수의 처리방식을 의미한다. 비용함수를 2차식으로 고려하면 `qudaratic`으로, 1차식으로 고려하면 `linear`로 입력해야 한다.
  * `{options:formulation}`은 조류계산 방식을 나타낸다. OPEN은 DC power flow formulation을 지원하고 있으며, `angle`로 입력해야 한다.
  * `{options:unit_commitment_variables_number}`은 기동정지계획에서 발전기의 상태를 표현하는 변수의 수를 의미한다. OPEN은 기동정지계획에서 상태, 기동, 정지 변수를 모두 사용하고 있기 때문에 3을 입력해야 한다.
  * `{options:base_MVA}`은 단위법를 사용할 때 기준용량(단위: MVA)을 의미한다.
  * `{options:penalty_price_co2}`은 배출량에 대한 페널티 가격(단위: KRW/MtonCO2eq)을 나타낸다.
`{options:penalty_load}`은 부하공급지장비용 산정을 위한 페널티 가격(단위: KRW/MWh)을 나타낸다.
  * `{options:solver_name}`은 최적화 풀이를 위한 solver를 나타낸다. CPLEX(상용 solver)를 사용하려면 `cplex`를 입력하고, GLPK(무료 solver)를 사용하려면 `glpk`를 입력해야 한다.
  * `{options:currency_unit}`는 최적화 풀이를 위해 비용의 크기를 조절할 때 사용한다.
  * `{options:reserve}`는 적용하고자 하는 운영예비력을 입력한다. 상향예비력은 `lump_reserve`, 하향예비력은 `lump_downward_reserve`으로 표기하며, 적용하고자 하는 운영예비력을 value로 작성해야 한다.
  * `{options:capacity_reserve}`는 연도별 설비예비력 요구량(단위:MW)를 나타낸다. 연도를 key(작성형식: yyyy)로, 요구량을 value로 작성해야 한다.
  * `{options:opex_yearly_weighted_coeff}`는 연도별 운영비용에 대한 가중치를 나타낸다. 연도를 key(작성형식: yyyy)로, 가중치를 value로 작성해야 한다.
  * `{options:capex_yearly_weighted_coeff}`는 연도별 건설비용에 대한 가중치를 나타낸다. 연도를 key(작성형식: yyyy)로, 가중치를 value로 작성해야 한다.


## How to set scenario
 시나리오 우당탕탕 써야함!!!!!!!!!!!!!!!!!

* 최적화 문제에서 제약조건(Constraint)은 결정변수(Decision variable)들이 반드시 만족해야 하는 조건을 의미하며, 등식 또는 부등식으로 나타낼 수 있다. 현실의 물리적, 기술적, 정책적, 자원적 한계 등을 제약조건으로 모델링함으로써 최적화 문제의 현실성을 높일 수 있다. OPEN Inputs에서 설명했듯이, OPEN은 사용자가 장기 전원계획 문제에서 사용자가 다양한 제약조건 옵션을 선택하여 문제에 반영할 수 있도록 지원한다. 또한, 사용자는 OPEN이 제공하고 있는 옵션 이외의 제약들을 반영하고 싶다면 모델을 확장하여 충분히 반영할 수 있다. 사용자는 입력 데이터와 시나리오 파일을 추가하거나 수정하여 다양한 제약조건을 설정할 수 있다. 이 장에서는 OPEN이 제공하고 있는 여러 시나리오와 제약조건 옵션을 소개하며, 이를 모델에 옵션을 반영하는 방법을 다룬다.

  > **:loudspeaker: 주의사항**
  > <small>
  > - 방법에 대한 순서는 상관없음 (좀 다듬어져야 함! to-do)
  > </small>


## How to execute OPEN

* OPEN은 코드 편집기(PyCharm, VSCode 등) 또는 PowerShell을 이용해 실행할 수 있으며, 시뮬레이션 진행 상황에 대한 이메일 알림 기능을 설정할 수 있다. 두 실행 방식 모두 실행에 앞서 입력 데이터 및 시나리오 설정 파일이 준비되어 있어야 한다.
* 코드 편집기를 사용하는 경우에는 다음과 같이 OPEN의 함수를 호출하여 실행할 수 있다. (VScode를 사용하는 경우 코드 내에 지정된 시나리오 이름과 경로 설정이 사용자의 환경에 맞게 수정되어야 함)

  ```python
  import os
  from open import Network
  from open._helpers import call_config

  if __name__ == '__main__':
      yaml_file_name = (
          "resources/"
          "sub_scenario_1.yaml"
      )

      config = call_config(
          yaml_file_name
      )

      kwargs = {}

      n = Network()
      n = n.module.run_GTEP(
          config = config,
          **kwargs
      )
  ```