# Member

## pair11 김태훈 고재원<br><br>
<h2>보안을 고려해 기본 기능을 시간 내에 구현하였습니다.</h2><br>

## Requirements

- 관통 프로젝트
- JavaScript
<br><br>



# 보안 요소

| No. ClassName  | code                                                         |
| ------------------------ | :----------------------------------------------------------- |
| 1 SHA-256     | <img src="/img/1.PNG"> |
| 2 유틸 클래스       | <img src="/img/2.PNG"> |
| 3 디폴트값 클래스  |  <img src="/img/3.PNG"> |
| 4 유효성 검사 인터페이스       |  <img src="/img/4.PNG">|
| 5 vo,dto 유효성 검사 구현    | <img src="/img/5.PNG"> |
| 6 vo,dto 유효성 검사 응용1    | <img src="/img/6.PNG"> |
| 7 vo,dto 유효성 검사 응용2         | <img src="/img/7.PNG">|
| 8 dao에서 디폴트 판별       | <img src="/img/8.PNG"> |
| 9 dao에서 디폴트 판별2           | <img src="/img/9.PNG">|
| 10 세션 관리(다른 곳에서 로그인 시 세션 끊김)       |<img src="/img/10.PNG">|
| 11 세션 관리(다른 곳에서 로그인 시 세션 끊김)2           | <img src="/img/11.PNG"> |
| 12 화면에서 세션 관리 (다른 곳에서 로그인 시 세션 끊김)3           | <img src="/img/12.PNG"> |

# 결과화면

## 회원가입 화면
![회원가입2](https://user-images.githubusercontent.com/81031522/228089965-006a03c6-7b65-4f64-a47f-9004ea05ab68.PNG)

중복 체크<br>
![중복아이디](https://user-images.githubusercontent.com/81031522/228090005-942072d3-c7ec-45f0-aaf4-c06afbbf4780.PNG)
<br><br>

## 로그인 화면
로그인<br>
![로그인전](https://user-images.githubusercontent.com/81031522/228089871-ad74351d-dd93-4564-bcf1-613f78ecfe67.PNG)
로그인 후<br>
![로그인후](https://user-images.githubusercontent.com/81031522/228089760-00f8d358-d0cc-49a1-8a54-1350a16e49bb.PNG)
<br><br>

## 마이페이지
![마이페이지](https://user-images.githubusercontent.com/81031522/228090054-1dab536b-4f55-4bd8-a238-da97595404c7.PNG)

입력이 틀렸을 때<br>
![마이페이지false](https://user-images.githubusercontent.com/81031522/228090082-4537a4c5-e555-4ee7-a4d5-3a76b7362c06.PNG)

입력 완료 시<br>
![마이페이지true](https://user-images.githubusercontent.com/81031522/228090098-aa6d4cd8-195a-443f-b86e-d2a462421796.PNG)

## Kakao Map과 데이터베이스를 활용한 관광지 정보 출력 화면
![여행지검색](https://user-images.githubusercontent.com/81031522/228090184-cd736686-a9ca-4ccd-8a5b-7045d4255bdb.PNG)
![여행지검색결과](https://user-images.githubusercontent.com/81031522/228090202-f70d4044-c689-404b-a638-bf63c578d23c.PNG)

<br><br>

# 소감

## 김태훈
### 구현 이야기
> 
1. JsonArray와 JsonObject 활용
기존의 공공데이터에서 여행 정보를 불러오는 방식에서 DB에서 여행 정보를 불러오는 방식으로 변환했습니다. 진행하는 중에 Servlet 코드에서 Json에 배열을 넣어서 프론트 단으로 전달해주는 방법을 몰라서 고생했지만 결국 JsonArray와 JsonObject를 사용해 전달하는 방식으로 구현해냈습니다.<br>
중복 로그인에 대한 처리도 구현했습니다. 구현 방식은 다음과 같습니다. 예를 들어 사용자 A가 본인 계정으로 로그인하고 사용자 B가 A와 같은 계정으로 로그인한다면, A가 사이트를 이용할 때 사용을 제한하는 방식으로 구현했습니다. 즉, 제일 최근에 로그인한 유저만 로그인 되도록 구현했습니다. 해당 기능을 구현하기 위해서 Servlet 클래스에 ConcurrentHashMap 형식의 hashmap을 멤버변수로 설정해 여기에 <key, value>로 <유저아이디, 세션>를 저장하도록 합니다. 일반적인 HashMap을 사용하지 않은 이유는 동시성 문제가 생길 수 있기 때문에 동시성 문제 방지를 보장하는 ConcurrentHashMap을 사용했습니다. 그런데 B가 로그인할 경우 기존에 hashmap에 존재하는 <ID, A의Session>이 <ID, B의Session>으로 갱신되고, 기존의 A의 Session이 invalidate() 함수에 의해 삭제됩니다. 이런 상태에서 A가 서버로 요청을 보내게 되면 A의 JSESSIONID에 해당하는 Session이 존재하지 않기 때문에 JsonObject 객체에 문제 상황을 담아서 프론트단으로 보냅니다. 세션 정보를 활용해 중복 로그인에 대한 처리를 하는 데 시간이 오래 걸렸습니다. 하지만, 중복 로그인 처리를 구현하면서 세션에 대해 좀 더 깊이 생각해 보고, 더 잘 이해하게 되는  계기가 되었습니다.<br><br>


## 고재원
### 구현 이야기
> 로그인 시 id로 script를 입력하면 XSS에 노출될 수 있기 때문에 이를 방지하기 위해서 입력값에 대해 'script' 태그를 포함한 문자열이 존재한다면 이를 다른 문자로 치환하는 방식으로 XSS에 대한 위험을 방지했습니다.<br>
SQL Injection을 방지하기 위해서 DAO에서 Statement 객체가 아닌 PreparedStatement 객체를 활용해 query를 작성했습니다.<br>
회원가입 진행 시 비밀번호가 노출되어도 알 수 없도록 SHA-256을 활용해 암호화했습니다.<br>
여행지 정보들 중 attribute 값이 null인 값들에 대해서도 default값으로 변환했습니다. 이런 null 값들을 defaultValue로 설정하기 위해 DefaultValues 클래스에 각각의 attribute마다 public static final 멤버변수에 기본값을 설정했습니다. 여행지 정보를 조회할 때 각각의 tuple마다 null인 attribute를 default값으로 설정해 프론트 단으로 전송했습니다.<br>
예외의 종류별로 다른 로직으로 예외처리를 하기 위해서 catch 블록을 Exception 트리의 가장 하단에 있는 예외부터 처리하도록 설계했습니다.<br><br>

