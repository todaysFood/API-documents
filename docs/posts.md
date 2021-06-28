
## 피드 목록/등록

> URL: /api/feed/
> 
> Method: GET	

- Request  
	- None
- Response
	```json
	HTTP 200 OK
	Content-Type: application/json
	Vary: Accept
	```

- Front URL
	- `Writing Here`

> Method: POST


- Request
  - Header
   ```json
      {
      "Authorization : Bearer {JWT TOKEN VALUE}"
      }
   ```
  - Body
  ```json
    {
    "title" : 글 제목,
    "rating" : 평점(0.0~5.0),
    "place_id" : 장소 id,
    "content" : 글 내용
    }
    ```


## 피드 상세보기/수정/삭제
> Method: GET  
> URL: /api/feed/{post_id:int}/

- Request
	- None
- Response
    - Normal
      ```json
      HTTP 200 OK
      Content-Type: application/json
      {
        "id": 1,
        "title": "글 제목",
        "pub_date": "{timezone_now}",
        "modified_date": "{수정일자, default=Null}",
        "content": "글 내용",
        "rating": "1.0",
        "place_id": 1500,
        "author": "{user.UUID}"
      }
      ```
    
- Front URL
    - `Writing here`




> Method: PUT(수정)  

- Request
	- Header
    ```json
    {
    "Authorization : Bearer {JWT TOKEN VALUE}"
    }
	```
    - Body
    ```json
      {
      "title" : "제목 수정",
      "rating" : 1.0,
      "place_id" : 1500,
      "content" : "수정 테스트"
      }
    ```
    
- Response
  - Normal (status : 200 OK)
    ```json
    "Post edited"
    ```
  - 글쓴이와 User가 일치하지 않을 때 (status : 403 Forbidden)
    ```json
    {
    "detail": "이 작업을 수행할 권한(permission)이 없습니다."
    }
    ```
  - 인증정보가 유효하지 않을 때 (status : 401 Unauthorized)
    ```json
    {
    "detail": "Given token not valid for any token type",
    "code": "token_not_valid",
    "messages": [
        {
            "token_class": "AccessToken",
            "token_type": "access",
            "message": "Token is invalid or expired"
        }
    ]
    }
    ```
 
    

> Method: DELETE(삭제)  
- Request
	- Header
    ```json
    {
    "Authorization : Bearer {JWT TOKEN VALUE}"
    }
    ```

- Response
  - Normal (status : 204 No content)
    ```json
    "Post deleted"
    ```
  - 글쓴이와 User가 일치하지 않을 때 (status : 403 Forbidden)
    ```json
    {
    "detail": "이 작업을 수행할 권한(permission)이 없습니다."
    }
    ```
  - 인증정보가 유효하지 않을 때 (status : 401 Unauthorized)
    ```json
    {
    "detail": "Given token not valid for any token type",
    "code": "token_not_valid",
    "messages": [
        {
            "token_class": "AccessToken",
            "token_type": "access",
            "message": "Token is invalid or expired"
        }
    ]
    }
    ```
