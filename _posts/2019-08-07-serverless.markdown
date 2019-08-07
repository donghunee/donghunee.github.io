---
layout: post
title:  '[AWS]AWS Lambda HelloWorld 예제'
subtitle:   'AWS Lambda HelloWorld 예제'
categories: 'study'
tags: 'etc'
---

현재 진행중인 프로젝트에서 가장 중심이 되는 부분이 이미지 처리 부분이다. 이미지를 받고 전처리를 한 후 얼굴의 좌표를 따고, 딥러닝 모델에 보낸 후 retrun값을 합산하여 최종 응답을 보내준다.

여기서 딥러닝 모델 코드가 Python으로 작성되어 따로 이미지 서버를 만들어야 하나 고민하던중 Severless의 존재를 알게되었고, 많은 기업중 AWS의 Lambda 서비스를 이용하게 되었다. 

HelloWorld 예제부터 시작해보도록 하겠다.

---

# Lambda만들기

우선 AWS 로그인 후 [AWS Lambda](https://ap-northeast-2.console.aws.amazon.com/lambda/home?region=ap-northeast-2#/functions)에 접속해 준다.

![](/assets/img/posts/2019-08-07-10-24-59.png)

함수 생성 버튼을 눌러준다.

![](/assets/img/posts/2019-08-07-10-25-45.png)

새로 작성을 눌러준 후, 함수의 이름은 HelloWorld로 런타임은 Python 3.7로 설정해주겠다.

![](/assets/img/posts/2019-08-07-10-40-05.png)

역할의 경우엔 람다에 부여하고 싶은 권한을 설정하게 됩니다. 역할을 추가해두면, 이전에 생성한 것을 선택해서 재 사용할 수 있습니다. 저희는 아직 없으므로 사용자 지정 역할을 생성하겠습니다.

![](/assets/img/posts/2019-08-07-10-41-53.png)

다음과 같이 작성하고 함수 생성을 눌러줍니다.

#Lambda 관리하기

![](/assets/img/posts/2019-08-07-11-06-07.png)

다음과 같은 관리 페이지를 확인할 수 있습니다.

밑으로 가면

```python
import json

def lambda_handler(event, context):
    # TODO implement
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }

```
다음과 같은 코드가 나타납니다.

현재 함수는 호출시 'Hello from Lambda"를 응답하게 만들어져 있습니다.

이 함수를 테스트 해보겠습니다. 상단에 테스트 버튼을 눌러보겠습니다.

![](/assets/img/posts/2019-08-07-11-08-43.png)

이벤트 이름을 작성하고 스크롤을 내려서 생성을 해줍니다.

여기서 입력하는 JSON은, lambda함수에서 event로 입력받게 되는 값입니다.

생성 후, 다시 테스트 버튼을 눌러줍니다.

![](/assets/img/posts/2019-08-07-11-10-56.png)

짜잔! 다음과 같이 응답을 받을 수 있습니다.

# Lambda에 HTTP 부여하기

이번에는 특정 주소에 요청이 되면 해당함수가 실행되도록 해보겠습니다.

Lambda 구성부분에서 API Gateway를 선택해보겠습니다.

![](/assets/img/posts/2019-08-07-11-12-52.png)

새 API 생성을 눌러주시고, 보안의 경우 **열기**를 선택해 줍니다. 열기를 선택했을 경우 누구나 해당 주소에 접근할 수 있습니다.

작성이 완료되면 추가 버튼을 눌러줍니다.

![](/assets/img/posts/2019-08-07-11-14-38.png)

그렇다면 다음과 같이 엔드포인트를 확인 할 수 있습니다.

해당 주소에 접근하면

![](/assets/img/posts/2019-08-07-11-15-36.png)

다음과 같은 응답을 받을 수 있습니다.
