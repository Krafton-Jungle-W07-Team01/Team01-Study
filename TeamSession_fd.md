# File Descriptor(FD)

- 파일 디스크립터(FD, File Descriptor)
  - 네트워크 소켓과 같은 파일이나 기타 입/출력 리소스에 액세스하는 데 사용되는 추상표현
  - ‘0이 아닌 정수’ (’Non-negative Integer’) : 음수가 아닌 0과 양수인 정수 값
    - 음수는 오류 조건을 나타내기 위해 예약된다.
  - 시스템으로부터 할당받은 파일이나 소켓을 대표하는 정수

<br>

- POSIX API
  | 정수 값 | 이름 |
  | ------- | ----------------- |
  | 0 | 표준 입력(stdin) |
  | 1 | 표준 출력(stdout) |
  | 2 | 표준 에러(stderr) |

<br>
위의 3가지 디스크립터는 프로그램이 프로세스로 메모리에서 실행을 시작할 때 언제나 열린 채로 동작한다.

⚠️ 프로그램에서 파일 디스크립터를 참조할 때는 번호를 쓸 수도 있지만 가능하면 ‘UNISTD.h’ 에 POSIX 이름을 쓰는 편이 좋다.

<br>

![Untitled]

1. **[file descriptor table]**
   FD 테이블의 인덱스를 통해 파일 디스크립터 테이블에 접근한다.
2. **[open file description]**
   인덱스가 가리키는 객체는 `dentry` 라는 객체를 가리킨다. 1. dentry(directory entry) : 디렉토리에 접근을 빠르게 하기 위한 구조체
3. **[inode table]**
   dentry 구조체는 관련된 inode 구조체를 가리키는 필드를 포함한다.

<br>

<br>

## 파일 디스크립터와 열려 있는 파일의 관계

- 각 프로세스 별로 커널은 ‘open file descriptor table’을 갖고 있다.
- entry 에 담긴 정보
  - 해당 파일의 offset
  - 동작 제어 flag
  - 접근 모드
  - i/o 관련 설정
  - 파일의 i-node를 가리키는 참조

<br>

<br>

## i-node

- linux 명령어로 `ls -al` 를 쳤을 때 나타나는 정보가 i-node 정보다.

<br>

- 파일에 일종의 번호를 부여했다.
- 파일에 대한 정보(메타데이터)를 가진, 일종의 데이터
- 파일 시스템 내에서 파일이나 디렉토리는 고유한 i-node를 가지고 있으며, i-node 번호를 통해 구분이 가능하다.
- 하나의 파일이 여러 데이터 블록(data blocks)을 가질 수 있다.
  이때 아이노드는 그 모든 블록의 주소를 가리키는 포인터들에 대한 정보를 포함하며 아이노드는 이 data block들을 연결해준다.

<br>

- 아이노드가 가지고 있는 정보
  - 파일 모드(퍼미션)
  - 링크 수
  - 소유자명
  - 그룹명
  - 파일 크기
  - 파일 주소
  - 마지막 접근 정보
  - 마지막 수정 정보
  - 아이노드 수정 정보

<br>

- inode table 이미지

![Untitled]

<br>

- direct block : 실제 파일의 내용을 담고 있는 디스크의 데이터 블록을 가리키는 포인터 변수
- 만약 데이터 블록 12개 만큼을 한 파일에서 저장공간으로 사용할 수 있다면 4KB \* 12 = 48KB 밖에 저장할 수 없다.
- But, indirect block을 지정해서 추가로 데이터 블록의 공간을 확장 해서 사용할 수 있다.
  - 만약 single indirect block을 사용한다면 1024(개의 포인터) \* 4(KB) 로 최대 파일의 크기가 4MB가 된다.

<br>

## 심볼릭 링크 🆚 하드 링크

- 심볼릭 링크
  - 원본 파일의 inode를 가리키는 또다른 파일(inode) 가 생성된다.
- 하드 링크
  - 원본 파일의 inode에 대한 직접적인 포인터이다.

<br>

<br>

<br>

## 🔗 Reference

- 파일 디스크립터(File Descriptor)란?
  ([https://code4human.tistory.com/123](https://code4human.tistory.com/123))
- 리눅스 - 파일 디스크립터
  ([https://dev-ahn.tistory.com/96](https://dev-ahn.tistory.com/96))
- [Linux] 리눅스 시스템의 아이노드(inode), 심볼릭 링크(Symbolic Link), 하드 링크(Hard Link)에 대해서.
  ([https://i5i5.tistory.com/341](https://i5i5.tistory.com/341))
- [Linux Kernel Concept, File System] (1) 유닉스 파일시스템과 Inode구조체
  ([https://jiming.tistory.com/359](https://jiming.tistory.com/359))
