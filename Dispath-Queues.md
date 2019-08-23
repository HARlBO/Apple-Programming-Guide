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
