# Sign In with Apple

[Introducing Sign In with Apple - WWDC 2019 - Videos - Apple Developer](https://developer.apple.com/videos/play/wwdc2019/706)


> 📌 영상 보면서 Transcript보고 번역 한 것으로, 발표 자료 보며 추후 정리 필요!

## Overview

Sigin In with Apple 은 빠르고 쉬운 계정 설정 및 앱에 가입 방법 입니다.
이것은 사용자들과 당신의 보안에 모두 안전하고, 개인적입니다.

애플은 앱의 사용자들과 당신이 어떻게 관련있는지 알 필요가 없습니다.

그래서 Apple이 그중 무엇도 추적하지 않는다는 확신을 가지고  Sign In with Apple을 구현할 수 있습니다. 그 버튼을 사용자가 눌렀을 때의 경험을 간단히 살펴봅시다. 당신이 요구한 이름과 이메일 같은, 미리 채워져 있는 시트를 보여줍니다. 사용자는 그들이 공유하고 싶은 이메일을 선택할 수 있습니다. Continue 버튼을 누르면 끝입니다. 당신의 앱에 가입 되었습니다.

당신의 앱은 사용자에게 얻을 수 있는 고유하고 안정적인 ID와 이름과 검증된 이메일 주소를 받습니다.  무엇보다도, 이것은 당신의 앱 사용자들에게 안전한 2단계로 인증된 계정입니다. 너무 간단합니다.

심지어 더 좋은 것은,  이 모든 종류의 사용자의 디바이스 간에 원할하게 작동한 다는 것입니다.

새로운 디바이스에서, 간단한 탭으로 그 전과 같은 계정을 제공 받을 수 있고 다시 완벽히 관련 될 수 있게 준비 된다. 매우 빠르고, 매우 쉽다. Sign In with Apple은 당신의 앱에 정말 간결한 계정 설정 경험을 제공한다. 채워야 하는 복잡한 폼이 없는 것에 주목하라. 단지 간단한 탭이면 된다. 유저는 당신의 앱을 앱스토어에서 애플 아이디를 사용해서 이미 다운 받았다. 그리고 Sign In with Apple은 단지 앱에서 탭으로 충분히 활용할 수 있게 도와준다. 당신은 또한 사용자들과 소통할 수 있는 검증된 이메일 주소를 받을 수 있다. 이것은 애플이 소통을 위해 사용하는 이메일 주소이다. 그러므로 이메일을 보내고 사용자가 링크를 클릭하는 복잡한 왕복 여행을 할 필요가 없다. 

애플은 당신을 위해 이미 그 작업을 해놓았다. Sign In with Apple은 추가적인 검증이 요구되지 않는 즉시 사용 가능한 이메일을  제공한다. 몇몇 사용자들은 그들의 실제 이메일 주소를 공유하는 것에 불편함을 느낄 것이다. 그리고 당신은 결국 동작하지 않는 가짜 이메일들을 받게 될지도 모른다.

Sign In with Apple이 도와줄 것이다. 이메일 숨기기 옵션은 사용자들이 검증 된 이메일 함으로 연결되는 숨김 처리 된 이메일 주소를 공유 할 수 있게 해준다.

정말 멋지다. 이것은 사용자에게 검증 된 이메일로 이메일을 보내고 답장도 보낼 수 있는 애플의 Private Email Relay 시스템을 통해 가능하다. 그래서 양방향으로 작동한다. 당신을 이것을 당신의 앱에 모든 종류의 비지니스 커뮤니케이션에 사용 할 수 있다. 애플은 사용자의 받은 메일함에 전송 된 어떠한 메세지도 남기지 않는다. 요약하자면, 당신의 앱에서 사용 할 수 있는 검증된 즉시 사용 가능한 이메일이다. 

Sign In with Apple 을 사용하면 기억해야 하거나 또는 까먹을 수 있는 새로운 비밀번호가 필요 없다. 그래서 이미 더 안전하다. 더 좋은 것은, 앱에서 받는 모든 계정은 두 단계 검증으로 보호 받는 다는 것이다. 

이것은 당신의 앱에 최고의 계정이다. 비밀 번호도 없고, 두 단계 인증, 비용도 들지 않으며 사용자들에게 마찰도 없다. Sign In with Apple을 통해 대단한 built-in 보안을 제공한다. 

요즘 당신의 시스템에서 계정 부정 행위를 방지하는 것은 어려운 문제이고, 애플은 도울 수 있는 고유한 위치에 있다.

Sign In with Apple은 앱의 사용자가 실제로 존재 한다는 확신을 얻을 수 있는 새로운 보안 친화적인 방법을 포함한다. 이것은 정교한 디바이스 내의 정보와 계정 정보를 결합하고, 이를 하나의 비트로 추상화 한다. (실제 사용자 또는 미지의 사용자)
실제 사용자에게는 앱에서 그들이 받을 만한 레드 카펫 대우를 해준다.

이것은 신뢰도가 높은 지표이다. 만약 알 수 없는 사용자를 받았다면, 그것은 사용자일수도, 봇일수도 있다. 이 사용자를 결정을 내릴 충분한 정보가 없는 당신의 시스템의 어떤 다른 새로운 계정 처럼 다뤄라. 이것이 계정 부정 행위에 대항하는데 도움을 줄 실제 사용자 지표이다.

마지막으로, Sign In with Apple은 크로스 플랫폼이다. API 는 모든 모든 애플 플랫폼에서 사용 가능하다.(iOS, MacOS, WatchOS, tvOS) 가입 경험은 각각의 플랫폼에 사용하기 쉽게 맞추어져 있다. JavaScript API는 Sign In with Apple을 웹 뿐만 아니라 윈도우나 안드로이드같은 다른 플랫폼에서 사용 가능하게 해준다.

이것에 대해서 더 자세히 나중에 이야기 해 보겠다. 간결한 계정 설정, 검증된 이메일 주소, 내장된 보안, 부정 행위 방지 그리고 크로스 플랫폼. 이것은 Sign In with Apple 주요 기능들의 간단한 요약이다. 다음, Dima가 스테이지에 올라와 네이티브 앱에 통합 시키는 방법에 대해 이야기 해보겠다.

### Integrating with Your App

여러분은 이제 이 훌륭한 기능들을 보았다. 앱에 통합 되는데 실제로 필요한 것은 무엇 일까? 당신의 앱에서 구동되기 위해 필요한 4가지 핵심이 있다. 첫째로, Auto Sign In with Apple-branded 버튼이다.
그 다음 권한 허가를 설정하고 수행하는 것이다. 사용자가 Sign In with Apple UI를 본 후에 그리고 빠르게 FaceID 체크를 한 후, 허가의 결과가 앱으로 반환 될 것이다. 이 시점에 당신은 Apple ID 서버에 결과를 검증해야 하고 당신의 시스템에 계정을 생성해야 한다. 마지막으로 특히, 당신의 앱에 반환이 된 후에  자격 증명 상태가 바뀌게 될 것이고 당신의 앱은 그 상태들을 적절히 바꿔 주어야 한다. 
```swift
    // Add Sign In with Apple button to your login view
    func setUpProviderLoginView() {
    	let button = ASAutorizationAppleIDButton()
    
    	button.addTarget(self, action: #selector(handleAutorizationAppleIDButtonPress), 
    									 for: . touchUpInside)
    	
    	self.loginProviderStackView.addArrangedSubview(button)
    }
```

첫번째로, Sign In With Apple 버튼에 대해 알아보자. 아주 적은 코드로, AutorizationAppleIDButton을 앱에 추가 할 수 있다. 일단 초기화를 하고, action을 추가해라. 그리고 그게 너가 해야 할 모든 것이다. 그 버튼은 당신의 앱 디자인에 맞게 몇가지 커스터마이징 된 버튼을 제공한다. 시각적인 스타일의 차이와 label의 차이를 사용 할 수 있다. 현재 검증 API를 사용 하고 있는 앱은 매우 친숙 하다는 걸 알 수 있을 것이다. 다음으로, 사용자가 action을 수행하면, 요청을 설정하고 검증을 수행해야 한다. 어떻게 하는지 보자.
```swift
    // Configure request, setup delegates and perform authorization request
    @objc func handleAuthorizationButtonPress() {
    	let request = ASAutoriztionAppleIDProver().createRequest()
    	request.requestedScopes = [.fullName, .email]
    
    	let controller = ASAuthorizationController(autorizationRequests: [reqeust])
    
    	controller.delegate = self
    	controller.presentationContextProvider = self
    
    	controller.performRequest()
    }
```

단지 코드 한 줄로, Apple ID 권한 요청을 초기화 한다.
이것이 당신의 시스템에서 계정을 생성하기 위해 앱에서 해야 할 모든 것이다.
선택적으로, 당신의 앱이 최고의 유저 경험을 위해 요구 된다면, .fullName과 .email을 requestedScopes에 설정 할 수 있다. 당신은 이 정보들이 작은 양의 정보들로 사이드가 있을 때 앱과 에러에 꼭 필요 할 때만 이 정보들을 요청 할 수 있다. 요청이 설정되면, AutorizationController가 초기화 되고, 결과를 받기 위해 delegate를 설정한다.

마지막으로, 요청을 수행한다. 요청을 수행하면, authorization UI가 유저에게 보여지도록 초기화 될 것이다.

빠른 FaceID 체크 후에, 허가 결과가 앱으로 리턴 될 것이다.
```swift
    func authorizationController(controller _: ASAuthorizationController,
    														didCompleteWithAuthorization authorization: ASAutorization) {
    	if let credential = authorization.credential as? ASAuthorizationAppleIDCredential {
    		let userIdentifier = credential.user
    		let identityToken = credential.identityToken
    		let authCode = credential.authorizationCode
    		let realUserStatus = credential.realUserStatus
    
    		// Create account in your system
    }
    
    func authorizationController(_: ASAuthorizationController,
    														didCompleteWithError error: Error) {
    	// Handle error
    }
```

이 결과를 다루는 법에 대해 이야기 해보자. AuthorizationController의 didCompleteWithAuthoization 메소드를 통해, authorization 객체를 받게 될 것이다. 이 객체는 AppleIDCredential 타입의 credential 프로퍼티를 갖고 있다. 진행을 하기 전에 이것이 실제 AppleIDCredential 인지 체크 해봐야 한다. 이 객체는 시스템에서 계정을 생성하기 위해 필요한 모든 정보를 가지고 있다. 사용자가 요청을 취소하거나 어떤 에러가 발생하면, didCompleteWithError 콜백을 통해 앱이 알도록 할 것이다. 이 delegate 콜백 모두 앱의 메인 큐에서 만들어 진다는 것이 보장된다. 이제 우리가 앱에게 보내줄 결과에 대해 더 깊게 알아보자. 먼저, user identifier다. 이것은 고유하고, 안정적이고, 팀 범위의 유저 식별자이다. 이것은 훌륭하다. 다른 플랫폼, 다른 시스템, 웹, 안드로이드에 걸쳐 사용자 시스템에서 정보를 찾을 때 사용된다.
그리고 이것은 당신의 개발 팀과 연관 되어있다. 이것이 당신의 사용자의 키 값이다.

다음으로, 우리는 검증 데이터를 리턴 할 것이다, identity token 과 authorization code.
오래가지 못하는 토큰을 refresh token으로 교환하는데  Apple ID 서버를 사용 할 수 있다.

만약 당신이 이미 존재하는 검증 시스템에 통합한다면, Sign In with Apple을 적용하는 것은 매우 익숙 할 것이다. 선택적으로, 당신이 요청 한다면 우리는 이름과 검증 된 이메일 계정 정보를 반환 할 것이다. 그리고 이메일이 애플에 의해 검증 되었기 때문에, 우리가 이것을 보여준 후에는 당신의 앱은 더이상 인증을 위한 과정을 더이상 수행할 필요가 없다. 마지막으로, 아까 언급 했던 실제 사용자 지표다. 가입 경험을 간소화 하기 위해 사용해라.

자 이제 당신은 시스템에서 계정을 생성 했다. 사용자가 애플 디바이스를 앱에서 사용하는 하면, credential 상태는 변할 것이다. 그리고 이 시나리오를 적절하게 다룰 필요가 있다.

사용자가 앱에서 Apple ID를 사용하는 것을 중단 할 수 있다. 그것은 디바이스에서 로그 아웃 될 것이다. 이런 이벤트 들은 적절하게 다루어져야 한다. 이것을 허용하기 위해서는, authentication servies framework는 이 상태를 질의 하기 위한 빠른 API를 노출 할 것이다.
```swift
    let provider = ASAuthorizationAppleIDProvider()
    
    provider.getCredentialState(forUserID: "currentUserIdentifier") { (credentialState, error) in
    	switch credentialState {
    	case .authorized:
    		// Apple ID Credential is valid
    	case .revoked:
    		// Apple ID Credential revoked, handle unlink
    	case .notFound:
    		// Credential not found, show login UI
    	default: break
    	}
    }
```

이전에 Apple ID Credential을 통해 반환 된 user identifier 를 사용해서, 현재 Apple ID Credential의 상태를 호출해 GetCredentialState를 확인 할 수 있다.

이것은 매우 빠른 API 호출이다. 이것은 세가지를 리턴한다. 우리는 user가 인증 되었는지 알려 줄 수 있고, 당신은 그들에게 앱을 계속 사용 할 수 있도록 해야한다. credential은 폐기 될 수 있다.

당신은 해당 디바에스에서 앱에서 로그아웃 시켜야 한다 그리고 선택적으로 그들에게 다시 로그인 하도록 안내한다. NotFound는 이전에 사용자가 Sign In with Apple을 통해 관계를 맺은 적이 없다는 것이다. 이 API는 매우 빠르다. 이 상태들 각각에 맞는 경험을 제공하기 위해 이것을 앱이 런치 될 때 이것을 호출 해야 한다. 
```swift
    // Register for revocation notification
    let center = NotificationCenter.default
    let name = NSNotificationName.Name
    let observer = center.addObserver(forName: name, object: nil, queue: nil) { (Notification) in
    	// Sign the user out, optionally guide them to sign in again
    }
```

추가적으로, 우리는 credential state가 revoke로 변할 때 NotificationCenter을 통해 notification을 보낸다. 
해당 디바에스에서 로그 아웃 시키고 부가적으로 다시 로그인 하도록 안내해라.

이제 사용자가 앱을 당신의 앱과 관계를 설정 했고, 그들은 앱을 사용하고 계정을 생성한다. 부득이하게 그들은 다른 디바이스를 갖게 될 것이고 당신의 앱에 다시 사용하길 원할 것이다. 이것에 대해 Sign In with Apple이 어떻게 돕는지 이야기 해보자. 사용자가 새로운 디바이스로 당신의 앱에 다시 돌아 왔을 때, 그들은 단 한번의 탭으로 로그인 경험을 하게 될 것이다. 빠른 FaeID 확인 후에, 그들은 당신에 앱에 돌아오는 것이다. 또한 추가적으로, 당신의 시스템에 존재하는 계정이라는 것도 알려 줄 것이다. 이제 같은 API를 통해 iCloud Deychain passwords를 제공한다. Apple ID와 iCloud Keychain을 통해 인증 요청을 할 수 있다. 사용자는 그들이 가지고 있는 이미 존재하는 credential을 사용하도록 제공 받을 것이다. 그리고 에러가 반환 되면, 일반 가입 플로우를 보여줄 것이다.

최고의 유저 경험을 위해, 당신의 앱은 존재하는 로컬 계정이 없다면 이 시작 기능을 호출해야 할 것이다. 이것을 구현하는 쉬운 방법을 보도록 하자.

```swift
    // Prompts the user if an existing iCloud Keychain credential or Apple ID credential exists.
    func performExistingAccountSetupFlows() {
    	// Prepare requests for both Apple ID and password providers.
    	let requests = [ASAuthorizationAppleIDProider().createRequest(),
    									ASAuthorizationPasswordProvider().createReuset()]
    
    	// Create an authorization controller with the given requests.
    	let authorizationController = ASAutorizationController(authorizationReuqeusts: requests)
    	authorizationController.delegate = self
    	authorizationController.presentationContextProvider = self
    	authorizationController.performRequests()
    }
```

처음으로, 존재하는 Apple ID authorization 요청과 Apple ID password 요청 배열을 초기화 한다. 이게 끝이다. 간단하다. request array를 전달하고 요청을 수행한다. 

```swift
    func authorizationController(controller _: ASAuthorizationController, 
    														didCompleteWithAuthorization authorization: ASAuthorization) {
    	switch authorization.credential {
    	case let credential as ASAuthorizationAppleIDCredential:
    		let userIdentifier = credential.user
    		// Sign the user in using the Apple ID credential
    	case let credintial as ASPasswordCredential:
    		// Sign the user in using their existing password credential
    	defaul: break
    	}
    }
```

Sign In with Apple connection이 존재 한다면, AppleIDCredenital은 앱으로 반환 할 것이다.

사용자에게 저장된 iCloud Keychain password가 있다면, credential은 앱으로 리턴 될 것이다. 이 API를 통해 받은 credential을 로그인하는데 사용해야 한다. 만약 사용자에게 존재하는 credential이 없다면, API는 즉시 에러를 반환하고 당신은 표준 로그인 플로우를 보여줘야 한다.

이 요청을 시작단계에서 함으로써, 시스템에서 계정 중복을 막을 수 있고 앱에 다시 돌아와 다시 사용하는 경험을 간결화 할 수 있다.

- 프로젝트 세팅의 Capabilities 섹션에서 좌측 상단의 +Capability 버튼을 눌러 Sign In with Apple을 추가
- 뷰컨에서 import AuthenticationServices 추가

### CrossPlatform

크로스 플랫폼은 중요하고 간단한 JavaScript 라이브러리를 통해 사용 가능하다. 이 라이브러리를 통해, 사용자는 윈도우나 안드로이드 같은 다른 플랫폼에서도 Sign In with Apple을 사용가능하다. 
그리고 친숙한 Sign In with Apple 버튼을 누르면 Apple ID를 입력하고 로그인 할 수 있는 애플로 리다이렉트 된다. 한번 로그인 하면, 그것은 리다이렉트된다. 당신이 받은 호출과 정보는 모두 네이티브 API와 유사하다.  당신이 요청한 ID, 토큰이나 심지어 이름 또는 이메일을 받을 수 있다. 그리고 ID와 토큰을 받게 되면, 당신의 앱에서 앱 영역으로 변환 가능 가능하다. 무엇보다도, 이것을 지원하기 위해 사파리에서도 설계 되어 있다.

사용자가 버튼을 클릭하면, 사파리는 네이티브 애플 페이 같은 시트를 올려 줄 것이다.

사용자는 간단하게 TouchID 할 수 있고 그들은 즉시 로그인 되고 웹사이트를 엄청 빠르게 이용 할 수 있다. 엄청난 경험이다. 그래서 그것은 사파리에 내장되었다. Javacript 라이브러리로 통합하는 것은 간단한 4단계 뿐이다.  당신의 HTML에 보이는 것 과 같이 JavaScript 라이브러리를 포함 시킴으로써 시작 할 수 있다. 간단한 div 가 버튼을 렌더링 한다. stype에 많은 파라미터를 통해 당신의 사이트에 맞게 커스터마이징 할 수 있다. 파라미터를 통해 이름, 이메일 어떤 것을 원하는지 설정하고 URI를 리다이렉트 한다. 그리고 마지막으로, 사용자가 로그인에 성공 하면, 결과가 인코딩 된 폼으로 값이 리다이렉트 URI를 통해 전송된다.

토큰과 auth code를 검증하고 앱 영역으로 전환한다.

그리고 세션을 얼마 동안 살려 놓을지 결정한다. 이것이 매우 빠르게 볼 수 있는 크로스 플랫폼을 지원하는 JavaScript 라이브러리이다. 
마지막으로, 언제 Sign In with Apple로 통합 할 때 모범 사례를 살펴보자.

### Best Practices

여기 따라야 할 몇가지 일반적인 가이드라인들이 있다. 앱스토어 가이드라인으로 시작하자면, 당신의 앱이 중요한 계정 기반의 기능들을 요구 하지 않는다면, 사람들이 로그인 없이 사용 할 수 있게 하라. 예를 들어, 사용자가 구매을 해서 나중에 사용자가 쉽게 돌아오도록 그들의 계정에 구매를 묶어야 할 때 Sign In with Apple 하도록 안내할 수 있다.  만약 유저를 구별하기 위한 고유한 식별자가 필요하다면, 이름과 이메일은 수집하지 마라. 당신은 그것이 필요 없다. 그리고 만약 Sign In with Apple을 통해 이메일을 수집한다면, 사용자의 선택을 존중 해야 한다.

그리고 여기 추가적인 API에 통합할 때 알아야 하나는 모범 사례가 있다.

당신의 앱이 시작할 때, 존재하는 계정이 있는지 확인 하기 위해 API를 사용해라.
이것은 유저가 iCloud Keychain password 또는 존재하는 Apple 계정이던 간에, 이미 앱에 존재하는 계정을 통해 빠르게 진입 할 수 있도록 한다. 

그리고 당신의 앱에 중복 된 계정을 가질 수 없다. 실제 유저에 대한 지표로 유저에게 최고의 경험을 제공하도록 계확해라. 만약 알 수 없음을 반환 한다면, 당신의 시스템에서 새로운 계정을 다룰 때 처럼 해라. 버튼 API를 통해 버튼을 그려라. 그리고 마지막으로, 사용자가 Sign In with Apple을 사용하면, 그들은 당신의 앱이 있는 모든 플랫폼에서 보길 기대 할 것이다. 그러므로 모든 플랫폼에 구현해라. 빠르게 모범 사례에 대해 살펴 봤다.

### Summary

Sign In with Apple은 앱에 빠르고 쉬운 계정 설정과 로그인 하는 방법이다.

간결하고, 복잡한 폼 없이 한번의 탭으로 계정 설정이 가능하다. 이메일 주소 인증은 즉시 작동하고 어떤 소통에도 사용 할 수 있다. 모등 계정에 대한 새로운 비밀번호가 필요 없는 내장된 보안 그리고 두 단계 인증이다.

실제 유저 지표는 계정 부정 방지를 도와준다. 그리고 크로스 플랫폼 지원을 통해 사용자는 당신의 앱이 올라가 있는 모든 플랫폼에서 Sign In with Apple의 장점을 얻는다.
