# ALB 엑세스 로그 / RDS 감사 로그 구성

## 목표
### [ALB]
- ALB 엑세스 로그 활성화 및 로그 파일 다운로드
- https://docs.aws.amazon.com/ko_kr/elasticloadbalancing/latest/application/load-balancer-access-logs.html
### [RDS]
- Amazon RDS MySQL에 대한 Audit 로그 구성 및 CloudWatch를 통한 로그 확인
- https://aws.amazon.com/ko/blogs/korea/configuring-an-audit-log-to-capture-database-activities-for-amazon-rds-for-mysql-and-amazon-aurora-with-mysql-compatibility/

## 세부내용
### [ALB]
#### 로그 저장을 위한 S3 버킷 생성 및 권한 설정
- S3 버킷 생성(ALB와 동일 리전 / 버킷 생성 네이밍 규칙 확인)
- 새로운 버킷 정책 생성(ALB에서 S3 저장을 위한 정책 설정)
#### ALB 엑세스 로그 활성화
- General Immersion Day Workshop > 심화모듈 - 웹어플리케이션 > 컴퓨트 - Amazon EC2에 생성한 Web-ALB에 대하여, 엑세스 로그 활성화
#### ALB 테스트 및 S3내 엑세스 로그 파일 확인 및 다운로드
- ALB 접속 테스트를 통하여 로그 생성후, 해당 로그 파일 다운로드

### [RDS]
#### Audit 플러그인 활성화
- Option 그룹 생성
- MARIADB_AUDIT_PLUGIN 선택
#### Option 그룹 정책 적용
- RDS Databases > Modify > Log exports에서 Audit log 체크(CloudWatch Log Groups에서 확인을 위한 설정)
#### 활성화된 Audit 로그 확인 및 다운로드
- CloudWatch > Logs > Log groups > /aws/rds/instance/'database명'/audit
- Actions > Exports results > Download search results(CSV)

## 제출 결과물
### [ALB]
- ALB 엑세스 로그 파일의 S3 경로 및 해당 파일(1개만)
### [RDS]
- RDS Audit 로그 파일(1개만)

## 발표내용
- 엑세스 로그 / Audit 로그 활성화 관련 작업내용 리뷰
- 발표 직전, 랜덤으로 발표자 선정
