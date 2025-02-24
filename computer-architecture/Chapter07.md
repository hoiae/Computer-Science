# 보조기억장치
## 다양한 보조기억장치
- - -
- 플레시 메모리: usb 메모리, sd카드, ssd와 같은 저장장치
### 하드디스크
- 하드디스크 : 자기적인 방식으로 데이터를 저장하는 보조기억장치  
  - `플래터`는 동그란 원판으로, 데이터가 저장되는 공간입니다. 자기물질로 덮여있으며 N극과S극은 0과 1의 역할을 수행합니다.  
    - 트랙 : 플래터를 동심원으로 나누었을 때 생기는 하나의 원
    - 섹터 : 원의 중심을 기준으로 나누어지는 사다리꼴의 영역, 하나이상의 섹터를 묶어 `블록`이라고 표현하기도함.
    - 실린더: 플래터 상에서 같은 트랙이 위한 곳을 모아 연결한 논리적 단위
      - 연속된 정보는 보통 실린더에 저장되는데, 이는 `디스크암`을 움직이지 않고 바로 데이터에 접근할 수 있기때문.
  - `스핀들`은 플래터를 회전시키는 역할을 합니다. 분당 회전수를 나타내는`RPM`을 속도의 단위로 사용합니다.
  - `헤드`는 데이터를 읽고 쓸때 사용됩니다.
  - `디스크암`은 헤드를 원하는 위치로 이동시킵니다.
  

- 하드디스크가 데이터에 접근하는 방법
  - 탐색 시간(seek time): 접근하려는 데이터가 저장된 트랙까지 헤드를 이동하는 시간
  - 회전 지연(rotational latency) : 헤드가 있는 곳으로 플래터를 회전시키는 시간
  - 전송 시간(transfer time): 하드 디스크와 컴퓨터 간에 데이터를 전송하는 시간

### 플래시 메모리(flash memory)
플래시 메모리는 전기적으로 데이터를 읽고 쓸 수 있는 반도체 기반의 저장 장치입니다.
- 셀(cell) : 플래시 메모리에서 데이터를 저장하는 가장 작은 단위
1개의 셀에 1티를 저장할수 있는 메모리는 SLC타입, 2비트를 저장할수 있는 메모리를 MLC타입, 3비트를 저장할 수 있는 메모리를 TLC라고 합니다.

#### SLC 타입(Single Level Type)
1개의 셀에 1비트를 저장하므로 두개의 정보를 표현할 수 있는 플래시 메모리 타입
- MLC, TLC 타입에 비해 입출력이 빠르다.
- MLC, TLC 타입에 비해 수명이 길다.
- 용량 대비 가격이 높다.

#### MLC 타입
1개의 셀에 2비트를 저장하므로 4개의 정보를 표현할 수 있는 플래시 메로리 타입
- SLC타입에 비해 대용화에 유리하다.
- SLC에 비해 용량대비 가격이 저렴하다.

#### TLC 타입
1개의 셀에 3비트를 저장하므로 8개의 정보를 표현할 수 있다.
- 대용화에 유리하다
- 용량대비 가격이 저렴하다.
- 시중에서 가장 많이 사용되는 타입

- 페이지(page) : 셀들이 모여서 만들어진 단위
- 블록(block) : 페이지가 모여 만들어진 단위
- 플레인(plane) : 블록이 모여 만들어진 단위
- 다이(die) : 플레인이 모여 만들어진 단위  

플래시 메모리의 읽기와 쓰기는 `페이지`단위로 이뤄집니다. 하지만 삭제는 `블록`단위로 이뤄어집니다. 읽기/쓰기와 삭제 단위가 다른것이 큰 특징
- 페이지의 상태
  1. Free상태 : 어떠한 데이터도 저장하고 있지 않아 `새로운 데이터를 저장할 수 있는 상태`
  2. Valid상태 : 이미 유요한 데이터를 저장하고 있는 상태
  3. Invalid상태 : 쓰레기값(유효하지 않은 데이터를) 가지고 있는 상태  
플래시 메모리는 하드디스크와 달리 `덮어쓰기가 불가능` 하여 Valid상태에 새 데이터를 저장할 수 없습니다.

- 가비지 컬렉션(gargabe collection)
유효한 페이지들만 새로운 블록으로 복사한 후 기존 블록을 삭제하여 공간을 정리하는 기능.

## RAID의 정의와 종류
- - -
### RAID의 정의
- RAID(Redundant Array Of Independent Disks)  
주로 하드디스크와 ssd를 사용하는 기술로, 데이터의 안전성 혹은 높은 성능을 위해 여러개의물리적 보조장치를 마치 하나의 논리적 보조장치처럼 사용하는 기술을 의미함.  

### RAID의 종류
1. RAID 0
   - 여러 개의 보조기억장치에 데이터를 단순히 나누어 저장하는 방식.
   - 저장되는 데이터가 하드 디스크의 개수만큼 나뉘어 저장됨
   - 줄무니처럼 분산되어 저장된 데이터를 `스트라입(stripe)`이라고 하고, 분산하여 저장하는 것을 `스트라이핑(striping)`이라고 함.
   - 스프라이핑되면 저장된 데이터를 읽고 쓰는 속도가 빨라진다.
   - 하나의 하드디스크에서 문제가 발생하면 다른 모든 하드디스크의 정보를 읽을 수 없다.
2. RAID 1
    - 복사본을 만드는 방식`미러링(mirroring)`으로 RAID 0의 단점을 보안할 수 있다.
    - 데이터를 쓸때 원본과 복사본을 두고 사용한다.
    - RAID0에 비해 속도가 느리다.
    - 사용가능한 용량이 적어진다.
3. RAID 4
    - RAID 1 처럼 완전한 복사본을 만드는 대신, 오류를 검출하고 복구하기 위한 정보`패리티비트`를 저장한 장치를 두는 구성 방식
    - 패리티를 저장한 장치를 이용해 다른 장치의 오류를 검출하고, 복구한다.
    - 새로운 데이터가 저장될때 마다 패리티를 저장하는 디스크에도 데이터를 써야하므로 `병목현상`이 발생한다.
4. RAID 5
   - RAID 4의 병목현상을 해소하기 위한 방식
   - 패리티 정보를 한곳에 저장하는 것이 아니라 분산하여 저장한다.
5. RAID 6
   - RAID 5와 구성은 같으나, 두개의 패리티비트를 사용한다. 
   - RAID 5보다 안전하다
   - RAID 5보다 쓰기 속도가 느리다.