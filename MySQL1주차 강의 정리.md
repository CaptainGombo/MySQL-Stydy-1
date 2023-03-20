# MySQL-Stydy-1

-Show tables (해당 테이블을 보여달라)

-Sql문 실행 단축키 Ctrl+Enter

-select(셀렉해라) *(모든필드) from(어디서부터)
ex)select * from orders

-특정 필드만 가지고 올 때
ex)select order_no, created_at, user_id, email from orders


*Where 절
-select 쿼리문으로 가져올 데이터에 조건을 걸어주는 것을 의미


ex)SELECT * from orders 
where payment_method = 'kakaopay'
(orders 테이블에서 결제수단이 카카오페이인 데이터만 가져와)

ex)SELECT * from point_users
WHERE point >= 5000
(point_users 테이블에서 포인트가 5000점 이상인 데이터만 가져와)

ex)SELECT * from orders 
WHERE course_title = '앱개발 종합반' and payment_method = 'CARD'
(orders 테이블에서 주문한 강의가 앱개발 종합반이면서, 결제수단이 카드인 데이터만 가져와)


quiz1. 포인트가 20000점 보다 많은 유저만 뽑아보기!
답:SELECT * from point_users 
WHERE point > 20000

quiz2. 성이 황씨인 유저만 뽑아보기
답: SELECT * from users 
WHERE name = '황**'

quiz3. 웹개발 종합반이면서 결제수단이 CARD 주문건만 뽑아보기
답: SELECT * from orders 
WHERE course_title ='웹개발 종합반' and payment_method ='CARD'


*tip 
1) show tables로 어떤 테이블이 있는지 살펴보기
2) 제일 원하는 정보가 있을 것 같은 테이블에 select * from 테이블명 쿼리 날려보기
3) 원하는 정보가 없으면 다른 테이블에도 2)를 해보기
4) 테이블을 찾았다! 조건을 걸 필드를 찾기
5) select * from 테이블명 where 조건 이렇게 쿼리 완성!


* Where 절과 자주 같이쓰는 문법 

-같지 않음: != 
ex)select * from orders
where course_title != '웹개발 종합반'/ (웹개발 종합반과 다른걸 보여줘)

-범위 조건: between
ex)select * from orders
where created_at between '2020-07-13' and '2020-07-15' /(20년7월13일부터 20년7월15일 전까지 보여줘)

-포함 조건: in
ex)select * from checkins 
where week in (1, 3) / (week가 1또는 3인것을 가져와)      

-패턴(문자열규칙) 조건 : like
ex)select * from users 
where email like '%daum.net' /(다음 이메일 사용 유저만 보여줘)
*%는 앞이나 중간에 뭐가있는지 상관없이 범위지정 ex) a%t : a부터 상관없이 t로 끝나는 데이터

*tip:Like는 패턴으로 조건을 거는 문법으로, 사용법이 아주 다양하다.

1) where email like 'a%': email 필드값이 a로 시작하는 모든 데이터
2) where email like '%a' email 필드값이 a로 끝나는 모든 데이터
3) where email like '%co%' email 필드값에 co를 포함하는 모든 데이터
4) where email like 'a%o' email 필드값이 a로 시작하고 o로 끝나는 모든 데이터
5)이 외에도 다양한 문법이 있어서 필요한것을 찾아쓰면됨('how to use like in sql' 구글링)


quiz1. 결제수단이 CARD가 아닌 주문데이터만 추출해보기
답: select * from orders
where payment_method !='CARD'

quiz2. 20000~30000 포인트 보유하고 있는 유저만 추출해보기
답: select * from point_users
where point between 20000 and 30000  / (숫자에는 ' ' 를 넣지않는다)

quiz3. 이메일이 s로 시작하고 com로 끝나는 유저만 추출해보기
답: select * from orders
where email like 's%com'

quiz4. 이메일이 s로 시작하고 com로 끝나면서 성이 이씨인 유저만 추출해보기
답: select * from users
where email like 's%com' and name = '이**'


*유용한 문법
-limit: 테이블에 어떤 데이터가 들어있나 잠깐 보려고 들어왔는데, 데이터를 다 불러오느라 시간이 오래 걸리고 힘들때
ex)select * from orders 
where payment_method = "kakaopay"
limit 5  
(5개만 출력)

-distinct: 중복 데이터는 제외하고 가져올 때 
ex)select distinct(payment_method) from orders

-count: 테이블에 데이터가 몇 개가 있는지 세야 할 때
ex)select count(*) from orders
where payment_method = 'kakaopay' / 결제수단이 '카카오페이' 인것은 몇 개인가?

-응용 (distinct 와 count를 같이 쓰기)
ex) select count(distinct(name)) from users / 스파르타 회원들의 성(family name)씨가 몇개인가?


quiz1. 성이 남씨인 유저의 이메일만 추출하기
답: select email from users
where name = '남**'

quiz2. Gmail을 사용하는 2020/07/12~13에 가입한 유저를 추출하기
답: select * from users
where created_at between '2020-07-12' and '2020-07-14'
and email like '%gmail.com'

quiz3. Gmail을 사용하는 2020/07/12~13에 가입한 유저의 수를 세기
답: select count(*) from users
where created_at between '2020-07-12' and '2020-07-14'
and email like '%gmail.com'

*Main Quiz. naver 이메일을 사용하면서, 웹개발 종합반을 신청했고 결제는 kakaopay로 이뤄진 주문데이터 추출하기
답: select * from orders
WHERE email like '%naver.com'
and course_title = '웹개발 종합반'
and payment_method = 'kakaopay'
