
## 회원가입
> Method: Post  
> URL: /api/register  

- Request  
	- email: 사용자 이메일  
	- password: 사용자 패스워드
	- name: 사용자 이름
	- nick_name: 사용자 닉네임
- Response
	- Normal
		```json
		{
    		"status": 200
		}
		```
	- 이미 가입되어있는 정보인 경우 (status: 400)
		```json
		{
    		"detail": "Already User ID Exist"
		}
		``` 
- Front URL
	- `Writing Here`

## 로그인
> Method: POST  
> URL: /api/login 

- Request
	- email: 사용자 이메일
	- password: 사용자 패스워드
- Response
	- Normal
		```json
		{
    		"status": 200
		}
		```
	- 잘못된 로그인 정보인 경우 (status: 400)
		```json
		{
    		"detail": "Request Credential is invalid."
		}
		```
- Front URL
	- `Writing Here`
		