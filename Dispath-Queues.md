# Dispath Queues

Grand Central Dispath (GDC) dispath queues는 task 수행을 위한 강력한 도구 입니다. Dispath queues는 임의의 코드 블록을 비동기 또는 동기식으로 수행 할 수 있게 해줍니다. 분리된 스레드에서 수행했던 거의 모든 task들을 수행하는데 dispath queues를 사용 할 수 있습니다. dispath queues의 이점은 스레드 코드에 해당되는 것보다 task를 수행하기에 사용하기 간편하고 더욱더 효율적입니다.

이번 챕터는 dispath queues를 당신의 앱에서 general task를 실행 하기 위한 사용 방법과 함께 소개를 제공합니다. 스레드 기반의 코드를 dispatch queues로 교체하고 싶다면, Mirgrating Away from Thread에서 사용 방법에 대한 추가적인 팁을 확인 할 수 있다

## Dispatch Queues에 대하여

Dispatch queues는 앱에서 task를 비동기적이고 동시에 task를 수행 하기 위한 쉬운 방법입니다. task는 단순히 앱에서 수행되어야 하는 어떠한 작업입니다. 예를 들어서, 당신은 어떤 계산을 하는, 자료구조를 생성하거나 수정하는, 파일로부터 데이터를 읽는 과정, 혹은 더 많은 것들을 수행하는  task를 정의 할 수 있습니다. 당신은 함수 또는 블록 객체 안에서 해당 코드를 위치 시키고 dispatch queue에 추가함으로써 task를 정의합니다.

dispatch queue는 전송한 task들을 관리하는 객체와 유사한 구조입니다. 모든 dispatxh queue들은 선입선출(FIFO) 자료 구조 입니다. 그러므로, queue에 추가된 task는 그것들이 추가 된 순서와 항상 같은 순서로 시작됩니다. GCD는 자동으로 일부 dispath queue를 제공하지만, 특정 용도를 위해서 당신이 생성할 수 도 있습니다. 표 3-1은 당신의 앱에서 사용 가능한 dispatch queue의 종류와 사용 방법을 나열하고 있습니다.

### Serial

Serial queue는 (private dispath queue로도 알려진)는 queue에 추가된 순서대로 한번에 한 개의 task를 수행합니다. 현재 실행 중인 task는 dispatch queue에 의해 관리되는 고유한 쓰레드(task마다 달라질 수 있는)에서 작동한다. Serial queue는 보통 특정 자원에 대한 접근을 동기화 하는데 사용됩니다.
당신은 필요한 만큼 많이 serial queue를 생성 할 수 있고, 각각의 queue는 나머지 모든 queue들과 관련하여 동시에 작동됩니다. 다시 말해서, 만약 4개의 serial queue들을 생성한다면, 각각의 queue는 한번에 하나의 task만 실행 하지만 최대 4개 까지의 task가 각 queue에서 동시에 실행 될 수 있습니다. serail queue를 생성하는 방법은, Creating Serial Dispath Queues에서 볼 수 있습니다.

### Concurrent

Concurrent queue는 (global dispatch queue의 한 종류로 알려진)는 하나 또는 이상의 task를 동시에 실행하지만, task들은 여전히 queue에 추가 된 순서대로 시작합니다. 현재 실행 중인 task는 dispatch queue에 의해 관리 되는 고유한 쓰레드에서 작동됩니다. 어떤 주어진 시점에 실행 중인 task의 정확한 개수는 가변적이고 시스템 상태에 의존적입니다.
iOS 5 이상에서, queue의 타입을 DISPATCH_QUEUE_CONCURRENT를 지정함으로써 concurrent dispatch queue를 생성 할 수 있습니다. 또한, 앱에서 사용 할 수 있는 4개의 미리 지정된 global concurrent queue도 있습니다. global concurrent queues를 가져오는 방법에 대한 정보는, Getting the Global Concurrent Dispatch Queues 에서 볼 수 있습니다.

### Main dispatch queue

Main dispatch queue는 메인 쓰레드에서 task를 실행 할 수 있는 전역적으로 사용 가능한 serail queue입니다. 이 queue는 실행 루프에 붙어 있는 다른 이벤트 자원들의 실행과 queue에 있는 task의 실행을 교차로 배치(interleave)하기 위해 앱의 실행 루프에서 작동됩니다.  앱의 메인 쓰레드에서 작동하기 때문에, 메인 queue는 종종 앱의 주요 동기화 시점에 사용됩니다..
dispatch queue를 생성할 필요는 없지만, 그것들이 적절히 빠져 나가는지 꼭 알아야 한다. queue가 어떻게 관리 되는지에 대한  더 많은 정보는, Performing Tasks on the Main Thread 에서 확인 할 수 있습니다.

> interleave : 컴퓨터 하드디스크의 성능을 높이기 위해 데이터를 서로 인접하지 않게 배열하는 방식을 말한다. 인터리브(interleave)라는 단어는 ‘교차로 배치하다’라는 뜻이며, 이를 통해 디스크 드라이브를 좀더 효율적으로 만들수 있다. 인터리브는 기억장치를 몇 개의 부분으로 나누어서 메모리 액세스를 동시에 할 수 있게 함으로써 복수의 명령을 처리하여 메모리 액세스의 효율화를 도모하는 것이다. 대부분의 하드디스크는 드라이브의 속도와 운영체제(OS), 응용 프로그램 등에 영향을 받기 때문에 인터리브 값을 미리 설정하지는 않는다. 인터리브 값이 작을수록 하드디스크 드라이브의 속도가 빨라진다.

앱에 동시성을 추가하는 것에 관해서, dispath queue는 쓰레드에 비해 몇가지 장점을 제공합니다. 가장 직접적인 장점은 work-queue(작업 대기열) 프로그래밍 모델의 간결성입니다. 쓰레드에서는, 실행하고 싶은 작업과 쓰레드 자체의 생성과 관리를 위한 코드를 작성해야 합니다. Dispatch queue는 쓰레드의 생성과 관리에 대한 걱정 없이 실제로 실행하고 싶은 작업에만 집중 할 수 있게 해줍니다. 그 대신에, 시스템이 당신을 위해 모든 쓰레드의 생성과 관리를 처리합니다. 어떤 단일 앱에서 할 수 있는 것 보다 시스템이 쓰레드를 훨씬 더 효율적으로 관리 할 수 있다는 것이 장점입니다. 시스템은 사용 가능 한 자원과 현재 시스템의 상태에 기반해 쓰레드의 개수를 동적으로 늘릴 수 있습니다. 또한, 보통 시스템은 쓰레드를 직접 생성했을 때 보다 task의 작동을 더 빠르게 시작 할 수 있습니다.

dispatch queue에 대해 당신의 코드를 재작성 하는 것이 어렵다고 생각 할 수 있지만, 쓰레드에 관한 코드를 작성하는 것보다 dispatch queue로 작성하는 것이 보통 쉽습니다. 코드 작성의 핵심은 독립적이고 비동기로 실행 할 수 있게 task를 설계하는 것입니다. (이것은 사실 쓰레드와 dispatch queue 모두에 해당됩니다.) 하지만, dispatch queue는 예측 가능성이라는 이점을 갖습니다. 만약 두개의 task가 같은 공유 된 자원에 접근 하지만 다른 쓰레드에서 작동 된다면, 쓰레드는 리소스를 먼저 수정할 것 이고, 당신은 두개의 task가 동시에 그 리소스를 수정하지 않도록 보장하기 위해 lock을 해야 필요가 있습니다. dispatch queue로는, 주어진 시간에 하나의  task만 수정 되는 것을 보장해 task를 모두 serial dipatch queue에 추가 할 수 있습니다. 이러한 queue 기반 동기화 타입은 lock보다 더 효율적입니다. lock은 항상 경쟁, 경쟁이 없는 두 케이스에 대해 높은 비용의 kernel trap을 요구하는 반면에, dispatch queue는 주로 앱의 process 공간에서 작동하고 꼭 필요한 경우에만 kernel에 요청하기 때문입니다.

비록 serial queue 에서 작동하는 두개의 task가 동시에 작동 되지 않는 다는 것을 지적 할 수 있겠지만, 두개의 쓰레드가 동시에 lock이 걸리면, 쓰레드가 제공하는 동시성을 잃거나 상당히 감소 할 수 있다는 것을 기억해야 합니다. 더 중요한 것은, 쓰레드 모델은 kernel과 사용자 공간의 메모리 모두 사용하는 두개의 쓰레드 생성을 요구합니다. Dispatch queue는 쓰레드에 대해 동일한 메모리 손실을 요구 하지 않고, 사용 되는 쓰레드는 바쁘게 유지 되고, 차단되지 않습니다.

dispatch queue에 대해 기억 해야하는 중요한 포인트는 다음과 같습니다.

- Dispatch queue는 다른 dispatch queue를 준수하여 동시에 task를 실행합니다. 이 쓰레드의 직렬화는 single dispatch queue의 task로 제한됩니다.
- 시스템이 동시에 실행할 task의 개수를 결정합니다. 그러므로, 100개의 다른 queue의 100개의 task를 갖는 앱은 모든 task를 동시에 실행하지 않을 것 입니다.
- 시스템은 시작할 새로운 task를 선택할 때 queue의 우선순위 레벨을 고려합니다. serial queue의 우선순위를 정하는 법에 대한 정보는, Providing a Clean Up Function For a Queue에서 봅시다.
- queue에 있는 task는 queue에 추가 되는 순간 실행 할 준비가 되어야 합니다. (만약 CoCoa operation object를 전에 사용했다면, model operation에서 사용하던 것과는 다른 방식 입니다.)
- Private dispatch queue는 reference-counted 객체입니다. 당신의 코드에 queue를 유지하는 것에 대해, dipatch source가 queue에 참고 될 수 있으며 또한 retain count를 증가 시킬 수 있다는 것을 유의해야 합니다. 그러므로, 모든 dispatch source가 취소 되었는지 확신 해야하고 모든 reatin call이 적절한 release call과 균형이 맞도록 해야 합니다. queue를 유지, 해제 하는 것에 대한 더 많은 정보는 Memory Mangament for Dispatch Queues에서 보세요. dispatch source에 대한 추가 정보는, About Dispatch Sources를 확인하세요.


### Queue 기반 기술들

dispatch queue 뿐만 아니라, Grand Central Dispatch는 몇가지 기술들을 제공합니다.

표 3-2 dipatch queue를 사용하는 기술들

- Dispatch groups
dispatch group은 completion을 위한 블록 객체의 집합을 모니터링 하기 위한 방법입니다. (블록들을 필요에 따라 동기적으로 또는 비동기적으로 모니터링 할 수 있습니다.) Group은 다른 task의 completion에  따라 코드의 유용한 동기화 매커니즘을 제공합니다. group을 사용하는 더 많은 정보는, Waiting on Groups of Queued Tasks에서 확인 할 수 있습니다.
- Dispatch semaphores
dispatch semaphore은 전통적인 semaphore와 비슷하지만 일반적으로 더 효율 적입니다. Dispatch semaphore은 semaphore를 사용 할 수 없어 calling thread가 차단 될 필요가 있을 경우에만     kernel로 호출됩니다. semaphore가 사용 가능하다면, kernel 호출은 수행되지 않습니다. dispatch semaphore 사용 방법에 대한 예시는, Using Dispatch Semaphores to Regulate the Use of Finite Resources를 확인하세요.
- Dispatch sources
dispatch source는 시스템 이벤트의 특정한 타입에 대한 응답 notification을 생성합니다. dispatch source를 notification, signal, descriptor 같은 이벤트들을 다른 것들 사이에서 처리하는 이벤트 모니터링 하는데에 사용 할 수 있습니다. 이벤트가 발생하면, dispatch source는  특정 dispatch queue 처리를 위해 비동기적으로 task 코드를 전송합니다. dispatch source를 사용하고 생성하는 더 자세한 내용은, Dispatch Sources를 확인하세요.

### Block을 사용해서 task를 구현하기

Block object는 C, Objective-C 그리고 C++ 코드에서 사용 할 수 있는 C 기반 언어의 기능입니다. Block은 자신을 포함한 작업 단위를 쉽게 정의할 수 있게 해줍니다. 비록 함수 포인터와 유사하게 보일 수 있지만, block은 실제로 객체와 유사한 기본 자료 구조로 표현되고 컴파일러에 의해 생성되고 관리됩니다. 컴파일러는 당신이 제공한 코드를 (관련 데이터와 함께) 패키지화 하고 그것을 heap에 들어 갈 수 있는 형식으로 캡슐화 하고 앱으로 전달합니다.

block의 중요한 장점 중 하나는 lexical scope(정적 범위) 외부에서도 변수를 사용 할 수 있는 능력입니다. block을 함수나 메소드 내부에 정의하면, block은 어떤면에서 전통적인 code block 같이 작동됩니다. 예를 들어, block은 부모 scope에 정의된 변수의 값을 읽을 수 있습니다. block에 의해 접근 된 변수는 heap에 있는  block 데이터 구조에 복사되어 block이 추후에 접근 할 수 있습니다. block이 dispatch queue에 추가 되면, 이 값들은 일반적으로 읽기전용 타입으로 남아 있어야합니다. 하지만, 동기적으로 실행되는 block은 _block 키워드가 붙은 변수 사용하여 부모의 호출 scope로 데이터를 반환하기 위해서도 사용 할 수 있습니다.

> lexical scope : 정적 범위라고도 하며, 프로그램 작성시 프로그램 내에서 선언된 변수의 위치에 의하여 그 변수가 사용될 수 있는 범위가 결정되는 것을 말한다. 변수가 선언된 부프로그램 내에서는 그 변수를 사용할 수 있지만 선언된 부프로그램 밖에서는 사용할 수 없다. (컴퓨터인터넷IT용어대사전)

함수 포인터에 사용되는 문법과 유사한 문법을 사용 하여 code에 inline으로 block을 정의 합니다. block과 함수 포인터의 주요 차이점은 block 이름 앞에 * 대신 ^가 옵니다. 함수 포인터처럼, 인수를 block에 전달하고 그것으로 부터 반환 값을 받습니다. 리스트 3-1은 코드에 block을 선언하고 동기적으로 실행하는 법을 보여줍니다. aBlock 변수는 단일 integer 파라미터를 받고 아무 값도 반환 받지 않도록 선언되어 있습니다. 그 프로토타입과 일치하는 실제 block이 aBlock에 할당되고 inline으로 선언됩니다. 마지막 줄은 표준화 할 지정된 integer를 출력하며 block을 즉시 실행합니다.

리스트 3-1 간단한 block 예제

    int x = 123;
    int y = 456;
    
    //Block declaration and assignment
    void (^aBlock)(int) = ^(int z) {
    	printf("%d %d %d\n", x, y, z);
    }
    
    //Excute the block
    aBlock(789); // prints : 123, 456, 789
