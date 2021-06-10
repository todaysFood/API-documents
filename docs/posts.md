
## 피드 목록 보기
> Method: Get  
> URL: /api/post

- Request  
	- None
- Response

  ```json
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
  

- Front URL
	- `Writing Here`

## 피드 상세 보기
> Method: GET  
> URL: /api/post/{post_id:int} 

- Request
	- Header
		```json
		{
    	"Authorization : Bearer {JWT TOKEN VALUE}"
		}
		```
- Response
    - Normal
      ```json
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
      
    - Invalid Token (status: 401)
        ```json
        {
         "detail": "Given token not valid for any token type",
         "code": "token_not_valid",
         "messages": [
          {
            "token_class": "AccessToken",
            "token_type": "access",
            "message": "Token is invalid or expired"
          }]
        }
      ```
    
- Front URL
    - `Writing here`


## 게시글 등록
> Method: Post  
> URL: /api/post/write

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

- Response
  - Normal
    ```json
        {
        "id": 게시글 번호,
        "title": 글 제목,
        "pub_date": 작성 일자(ex. 2021-06-10T19:19:15.043960),
        "modified_date": 수정 일자(기본 값: null),
        "content": 글 내용,
        "rating": 평점,
        "place_id": 장소 id,
        "author": 작성자 uuid 값(ex. "1c52fbe4-f33e-4659-95b9-8bd4eccf6948")
        }
    ```
  - Invalid Token (status: 401)
    
    ```json
      {
         "detail": "Given token not valid for any token type",
         "code": "token_not_valid",
         "messages": [
          {
            "token_class": "AccessToken",
            "token_type": "access",
            "message": "Token is invalid or expired"
          }]
      }
        
    ```
    
## 게시글 수정 / 삭제
> Method: GET   
> URL: /api/post/{post_id}/edit

- Request
	- Header
		```json
		{
    	"Authorization : Bearer {JWT TOKEN VALUE}"
		}
		```
  
- Response
  - Normal
    ```json
        {
        "id": 게시글 번호,
        "title": 글 제목,
        "pub_date": 작성 일자(ex. 2021-06-10T19:19:15.043960),
        "modified_date": 수정 일자(기본 값: null),
        "content": 글 내용,
        "rating": 평점,
        "place_id": 장소 id,
        "author": 작성자 uuid 값(ex. "1c52fbe4-f33e-4659-95b9-8bd4eccf6948")
        }
    ```
  - 글쓴이와 User가 일치하지 않을 때
    ```json
      {
      "detail": "User info. does not match the Author"
      }
    ```
    

> Method: PUT(수정)  
> URL: /api/post/{post_id}/edit
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
  - Normal
    ```json
    "Post edited"
    ```
  - 글쓴이와 User가 일치하지 않을 때
    ```json
      {
      "detail": "User info. does not match the Author"
      }
    ```
    

> Method: DELETE(삭제)  
> URL: /api/post/{post_id}/edit
- Request
	- Header
    ```json
    {
    "Authorization : Bearer {JWT TOKEN VALUE}"
    }
	```

- Response
  - Normal
    ```json
    "Post deleted"
    ```
  - 글쓴이와 User가 일치하지 않을 때
    ```json
      {
      "detail": "User info. does not match the Author"
      }
    ```
    
