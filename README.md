# HotelInfo

playdata 16기 1차 팀 프로젝트 백엔드 소스코드 입니다.

야놀자, 여기어때와 같은 호텔 정보 조회 서비스를 구현하였습니다.

## 사용 기술
- Spring Boot 2.5.7
- JAVA 8.0
- JPA 3
- Oracle DB 10g

## 구현 기능
- 호텔 검색 리스트 페이지
  - 호텔 별 별점 평균 점수 전달
  - 호텔 이름 전달
  - 호텔 이미지 경로 전달
  - 호텔 주소 전달

- 호텔 상세 페이지
  - 호텔 상세 정보 전달
  - 호텔 리뷰 리스트 전달

- 

Controller	Method	Mapping 방식	요청 url	설명	전송 url & data 예시	리턴 data 예시
DetailController	getHotelInfo	GET	/detail/hotel/{hotelid}	hotelid 기준으로 호텔 정보 조회	-	호텔 정보
	getAllRoom	GET	/detail/room/{hotelid}	hotelid 기준으로 룸 정보 조회	-	룸 정보
	getHotelAllReview	GET	/detail/review/{hotelid}	hotelid 기준으로 리뷰 조회( 페이징 )	url?page={page값}	리뷰 리스트 / 페이지 존재 5개씩
	getHotelBasic	GET	/detail/adhotel/{hotelid}	hotelid 기준으로 hotel main 데이터 조회	-	호텔 메인 정보
HotelMainController	getAllHotels	GET	/main/allhotel	모든 호텔 리스트	-	모든 호텔
	getHotels	GET	/main/hotel	모든 호텔 리스트( 페이징 )	url?page={page값}	모든 호텔 / 페이지 존재 12개씩
	searchHotel	GET	/main/search	"검색된 모든 호텔 리스트( 페이징 )
keyword1 = 통합 검색( 이름, 지역 )
keyword2 = 지역 고정 필수 검색
keyword1,2 모두 값이 없으면 default로 모두 찾기 됨"	"?keyword1={검색값}
&keyword2={지역명}
&page={page값}"	검색어별 호텔 / 페이지 존재 12개씩
ReviewController	writeReview	POST	/review/write	리뷰 작성하기	"{
        ""userId"": ""hunojung"",
        ""reviewContent"": ""goodgood"",
        ""reviewScore"": 2,
        ""hotelid"": 4
}"	SUCCESS
	deleteReview	DELETE	/review/delete	"리뷰 지우기 /
리뷰 seq와 userid 필요"	?seq={review seq값}&userid={userId}	SUCCESS / FAIL
	getMyOneReview	GET	/review/myReview/{userid}	userid기준 리뷰 조회( 페이징 )	?page={page값}	리뷰 리스트 / 페이지 존재 10개씩
	getHotelReviewScore	GET	/review/hotelReviewScore/{hotelid}	hotelid 기준으로 특정 호텔의 리뷰 평점만 1개 조회	-	1.2
	getAllReview	GET	/review/allReview	모든 리뷰 조회	-	리뷰 리스트
UserController	joinUser	POST	/user/join	"회원 가입
userId 와 password 입력하면 됨
( 관리자는 userId : admin 이며
login_status : 0 이다)"	"{
        ""userId"": ""hunojung2"",
        ""password"": ""1""
}"	SUCCESS
	updateUser	PUT	/user/update	유저 패스워드 변경	"{
        ""userId"": ""hunojung2"",
        ""password"": ""2""
}"	SUCCESS
	loginUser	POST	/user/login	"유저 로그인 기능
아이디와 비밀번호 비교해서 맞는지 확인"	"{
        ""userId"": ""hunojung2"",
        ""password"": ""2""
}"	"{
    ""seq"": 59,
    ""userId"": ""hunojung2"",
    ""password"": ""2"",
    ""login_status"": 1
}"
	deleteMember	DELETE	/user/delete/{userid}	userid 기준으로 유저 삭제	-	SUCCESS / FAIL
	getAllUsers	GET	/user/alluser	모든 유저 조회	-	유저 리스트
![image](https://user-images.githubusercontent.com/78013523/147844755-511ae645-9723-41ee-b9ef-8831aeab82dc.png)

