# AWS Lambda와 Amazon SNS를 활용한 SMS 발송

## 목표
* AWS Lambda와 Amazon SNS, Amazon EventBridge를 활용하여, 스케줄링을 통한 SMS 발송하기

## 아키텍처
![sending-sms](./sending-sms.png)

## 세부 내용
### SNS 생성
> 1. 문자메세지(SMS)에서 샌드박스 대상 전화번호에 본인의 전화번호 추가

### Lambda 생성
> 1. 신규 Lambda 생성
- 런타임 - Python 3.7 
> 2. 아래 소스 코드 입력
```
import json
import boto3

def lambda_handler(event, context):

    client = boto3.client(
        "sns",
        # 본인의 Region Code입력. ex) region_name="ap-northeast-2"
    	region_name="xx-xxxx-x"
    )
    
    client.publish(
		# SMS 샌드박스에 등록한 본인 전화번호로 수정
        PhoneNumber="+8210xxxxyyyy",
        Message="Hello World!"
    )

    return {
        'statusCode': 200,
        'body': json.dumps('Ok!')
    }
```
> 3. Lambda 실행 역할에 "AmazonSNSFullAccess" 추가
> 4. Test 및 Deploy 실행하여, 정상 동작 확인 
- Test Event는 기본값 그대로 사용
> 5. "phoneNumber", "message"로 구성된 이벤트 JSON 객체로 호출하도록 Test Event 재구성

### EventBridge에서 Cron식 생성
> 1. 신규 규칙 생성(규칙 유형 - 일정)
> 2. 일정 패턴은 아래 규칙에 맞는 Cron식 적용
- 2022년 7월, 매주 목요일 00:00:00 UTC에 실행
> 3. 2번에서 생성한 Lambda 연결

## 제출 결과물
> 1. Lambda ARN	
> 2. EventBridge Cron식
> 3. EventBridge 규칙 ARN
