```
HTML <HEAD>		
	<--- JS --->
- <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-cookie/1.4.1/jquery.cookie.js"></script>
</HEAD>
	
- function sign_out() {
            $.removeCookie('mytoken', {path: '/'});   
            alert('로그아웃!')		     	<---- 위 상단 스크립트가 없을 시 작동 안함						
            window.location.href = "/login"	<---- 로그인 구현시 반드시 쿠키라는 개념을 사용 브라우저 자체 DB로 이해 
        }					<---- 쿠키로 인해 접속하는 서버에서 지정한 시간동안 다시 로그인을 할 필요가 없음
```	
sha256 방법(=단방향 암호화. 풀어볼 수 없음)

- JWT 토큰 = payload와 시크릿키가 필요

- SECRET_KEY 'SPARTA' <-마스터 키같은 역할

```
	- payload = {
            'id': id_receive,
            'exp': datetime.datetime.utcnow() + datetime.timedelta(seconds=5)
        }
        token = jwt.encode(payload, SECRET_KEY, algorithm='HS256')
```
```
ID와 사용시간을 payload에 담고 시크릿키와 합쳐 토큰을 발행하여 유저에게 지급
- payload = jwt.decode(token_receive, SECRET_KEY, algorithms=['HS256'])
  user_info = db.users.find_one({"username": payload["id"]})              
```
payload값을 보기 위해선 복호화에 열쇠인 시크릿 키('SPARTA')라는 것을 이용해서 복호화를 한다...
	
==============|

로그 아웃 기능을 만들려고 겸사겸사 수업을 들었는데 수업을 다듣고 사용하려하니 내 프로젝트에서 기능을 안해서 이리저리 찾다가
아래 코드를 안써서 체감상 2시간은 날린거 같다. 한줄 넣고 너무 잘되서 기분이 허탈했다...
--->  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-cookie/1.4.1/jquery.cookie.js"></script>   <---
