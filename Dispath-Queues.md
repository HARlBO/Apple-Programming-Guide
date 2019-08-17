# Dispath Queues

Grand Central Dispath (GDC) dispath queues는 task 수행을 위한 강력한 도구 입니다. Dispath queues는 임의의 코드 블록을 비동기 또는 동기식으로 수행 할 수 있게 해줍니다. 분리된 스레드에서 수행했던 거의 모든 task들을 수행하는데 dispath queues를 사용 할 수 있습니다. dispath queues의 이점은 스레드 코드에 해당되는 것보다 task를 수행하기에 사용하기 간편하고 더욱더 효율적입니다.

이번 챕터는 dispath queues를 당신의 앱에서 general task를 실행 하기 위한 사용 방법과 함께 소개를 제공합니다. 스레드 기반의 코드를 dispatch queues로 교체하고 싶다면, Mirgrating Away from Thread에서 사용 방법에 대한 추가적인 팁을 확인 할 수 있다

## Dispatch Queues에 대하여

Dispatch queues는 앱에서 task를 비동기적이고 동시에 task를 수행 하기 위한 쉬운 방법입니다. task는 단순히 앱에서 수행되어야 하는 어떠한 작업입니다. 예를 들어서, 당신은 어떤 계산을 하는, 자료구조를 생성하거나 수정하는, 파일로부터 데이터를 읽는 과정, 혹은 더 많은 것들을 수행하는  task를 정의 할 수 있습니다. 당신은 함수 또는 블록 객체 안에서 해당 코드를 위치 시키고 dispatch queue에 추가함으로써 task를 정의합니다.

dispatch queue는 전송한 task들을 관리하는 객체와 유사한 구조입니다. 모든 dispatxh queue들은 선입선출(FIFO) 자료 구조 입니다. 그러므로, queue에 추가된 task는 그것들이 추가 된 순서와 항상 같은 순서로 시작됩니다. GCD는 자동으로 일부 dispath queue를 제공하지만, 특정 용도를 위해서 당신이 생성할 수 도 있습니다. 표 3-1은 당신의 앱에서 사용 가능한 dispatch queue의 종류와 사용 방법을 나열하고 있습니다.


