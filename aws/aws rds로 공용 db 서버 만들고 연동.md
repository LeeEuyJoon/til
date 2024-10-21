# < AWS RDS로 고용 db 서버 만들고 MySQL Workbench, Intellij와 연동 >

### RDS -> 새 인스턴스 생성
- 마스터 계정 아이디&비번, VPC, 가용 영역 등등 정하기
- 퍼블릭 액세스는 반드시 허용해야 외부에서 접근 가능
- 보안 그룹 인바운드 규칙에서 MYSQL/Aurora 버전 IPv4와 IPv6로 설정

### MySQL Workbench 연결
- Hostname에 엔드포인트
- Username에 관리자 계정
- port는 변경한 적 없으면 3306

### Intellij 연결
- DB 연결 콘솔에서
  - Name : @ + 엔드포인트
  - Host : 엔드포인트
  - User, pwd : 마스터 게정 아이디&비번

- applicaion.properties
  - spring.datasource.url=jdbc:mysql://<엔드포인트>:3306/<데이터베이스명>?useSSL=false&serverTimezone=UTC
  - spring.datasource.username=<사용자이름>
  - spring.datasource.password=<비밀번호>
  - spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
