# Chapter07 보조기억장치

## 다양한 보조기억장치

1. **하드 디스크** : 자기적인 방식으로 데이터를 저장하는 보조기억장치

   하드 디스크의 구성 요소

   1. 플래터 : 실질적으로 데이터가 저장되는 공간 (수많은 N극과 S극을 저장)
      - 트랙 : 플래터를 여러 동심원으로 나누었을 때 그 중 하나의 원
      - 섹터 : 여러 조각으로 나누어진 트랙의 한 조각 -> 하드 디스크의 가장 작은 전송 단위
      - 실린더 : 여러 겹의 플래터 상에서 같은 트랙이 위치한 곳 (연속된 정보 저장)
   2. 스핀들 : 플래터를 회전시키는 구성 요소 (RPM : 분당 회전수 - 스핀들이 플래터를 돌리는 속도의 단위)
   3. 헤드 : 플래터를 대상으로 데이터를 읽고 쓰는 구성요소
   4. 디스크 암 : 헤드를 원하는 위치로 이동시키는 구성 요소

   하드 디스크가 저장된 데이터에 접근하는 시간

   1. 탐색 시간 : 접근하려는 데이터가 저장된 트랙까지 헤드를 이동시키는 시간
   2. 회전 지연 : 헤드가 있는 곳으로 플래터를 회전시키는 시간
   3. 전송 시간 : 하드 디스크와 컴퓨터간에 데이터를 전송시키는 시간

2. **플래시 메모리** : 전기적으로 데이터를 읽고 쓸 수 있는 반도체 기반의 저장 장치 (USB 메모리, SD카드, SSD)

   셀 : 플래시 메모리에서 데이터를 저장하는 가장 작은 단위

   플래시 메모리 종류

   1. SLC타입 : 한 셀에 1비트를 저장 - 속도 빠름, 수명 김, 용량 대비 가격 높음, 한 셀로 두개의 정보 표현(0과 1)

      --> 데이터를 읽고 쓰기가 매우 많이 박복되며 고성능의 빠른 저장 장치가 필요한 경우

   2. DLC타입 : 한 셀에 2비트를 저장 - SLC보다 대용화 하기 유리, 한 셀로 4개의 정보 표현

   3. TLC타입 : 한 셀에 3비트를 저장 - 수명/ 속도 낮음, 용량 대비 가격 저렴, 한 셀로 8개의 정보 표현

      -->저가의 대용량 장치 

   페이지 : 셀들이 모여 만들어진 단위 -> 플래시 메모리에서 읽기와 쓰기

   1. Free 상태 : 새로운 데이터를 저장할 수 있는 상태 (어떠한 데이터도 저장되지 않은 상태)

   2. Valid 상태 : 이미 유효한 데이터를 저장하고 있는 상태 (새로운 데이터 저장/덮어쓰기 불가능)

   3. Invalid 상태 : 쓰레기값(유효하지 않은 데이터)를 저장하고 있는 상태

      가비지 컬렉션 : 유효한 페이지들만 새로운 블록으로 복사한 후 기존 블록을 삭제하여 공간을 정리하는 기능

   블록 : 페이지들이 모여 만들어진 단위 -> 플래시 메모리에서 삭제 

   ***읽기/쓰기 단위와 삭제 단위가 다름**

   플레인 : 블록들이 모여 만들어진 단위

   다이 : 플레인들이 모여 만들어진 단위

   

   ## RAID의 정의와 종류

   **RAID** : 데이터의 안정석 혹은 높은 성능을 위해 여러개의 물리적 보조기억장치를 하나의 논리적 보조기억장치처럼 사용하는 기술

   - RAID 레벨 : RAID 구성방법 (RAID **0**/**1**/2/3/**4**/**5**/**6**/10/50)

   - RAID 0 : 여러개의 보조기억장치에 데이터를 단순히 나누어 저장하는 구성 방식

     --> 저장되는 데이터가 하드 디스크의 개수만큼 나뉘어 저장됨

     스트라입 : 줄무늬처럼 분산되어 저장된 데이터 , 스트라이핑 : 분산하여 저장하는 것

     but 하드 디스크 하나에 문제가 생기면 문제 생김 -> 저장된 정보가 안전하지 않음

   - RAID 1 : 복사본을 만드는 방식(=미러링) --> 쓰기 속도는 RAID 0 보다 느림

     but 하드 디스크 개수가 한정되면 사용 가능한 용량이 적어지는 단점이 있을 수 있음 -> 많은 양의 하드 디스크 필요 -> 비용 증가

   - RAID 4 : 완전한 복사본을 만드는 대신/ 오류를 검출하고 복수하기 위한 정보를 저장한 장치(패리티 비트)를 둠

     --> 새로운 데이터가 저장될 때마다 패리티를 저장하는 디스크에도 데이터를 쓰게 됨 => 병목현상 발생

   - RAID 5 : 패리티를 분산해서 저장하는 방식 --> 병목현상 해소

     *** 병목현상 : **전체 시스템의 성능이나 용량이 하나의 구성 요소로 인해 제한을 받는 현상

   - RAID 6 : RAID 5 + 서로 다른 두 개의 패리티를 두는 방식 -> 데이터 저장 속도를 조금 희생하더라도 데이터를 더 안전하게 보관

   

   

   