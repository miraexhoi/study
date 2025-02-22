# 시스템 콜이란?

운영체제는 사용자가 실행하는 프로그램이 하드웨어 자원에 직접 접근하는 것을 방지해 자원을 보호한다.  
( 왜냐하면, 프로그램이 CPU, 메모리, 하드 디스크에 마음대로 접근하고 조작할 수 있다면,  
자원이 무질서하게 관리 될 수 있으며 한 프로그램의 실수가 전체 컴퓨터에 영향을 주기 때문 )  
운영체제는 프로그램들이 자원에 접근하려 할 때 오직 자신을 통해서만 접근하도록 해 자원을 보호한다.  

따라서, 프로그램은 자원에 접근하기 위해서 운영체제에게 도움을 요청해야 한다.  
그리고, 프로그램의 요청을 받은 운영체제는 응용 프로그램 대신 자원에 접근해 요청한 작업을 수행한다.  
이런 과정은 CPU가 명령을 실행하는 모드를 사용자 모드와 커널 모드로 구분하는 방식인 **이중 모드(Dual Mode)** 로 구현된다.  

- **사용자 모드(User Mode)** 는 운영체제 서비스를 제공받을 수 없는 실행 모드이다.  
CPU가 해당 모드인 경우, 입출력 명령어와 같은 하드웨어 자원 접근 명령을 실행할 수 없다.  
일반 프로그램은 기본적으로 사용자 모드로 실행된다.  

- **커널 모드(Kernel Mode)** 는 운영체제 서비스를 제공받을 수 있는 실행 모드로 커널 영역의 코드를 실행할 수 있다.  
CPU가 커널 모드로 명령어를 실행하면 자원에 접근하는 명령어를 비롯한 모든 명령어를 실행할 수 있으며, 운영체제는 커널 모드로 실행된다.  

사용자 모드로 실행되는 프로그램이 자원에 접근하는 운영체제 서비스를 제공받으려면 운영체제에 요청을 보내 커널 모드로 전환돼야 한다.  
**시스템 콜(System Call)** 은 이때 운영체제 서비스를 제공받기 위한 요청을 의미, 일종의 **소프트웨어 인터럽트**이다.  

시스템 콜을 발생시키는 명령어가 실행되면, CPU는 현재까지의 작업을 백업한 뒤에 커널 영역 내에 시스템 콜을 수행하는  
인터럽트 서비스 루틴을 실행한 이후, 다시 기존 실행하고 있었던 프로그램으로 복귀하여 실행을 계속한다.  
