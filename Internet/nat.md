# NAT 기능을 사용하는 이유

IP 주소는 **공인 IP 주소(Public IP Address)** 와 **사설 IP 주소(Private IP Address)** 가 존재한다.  
공인 IP 주소는 고유하며, 사설 IP 주소는 고유하지 않고 특정 사설 네트워크에서만 사용된다.  

**\* 사설 네트워크는 외부 네트워크에 공개되지 않은 네트워크를 의미**   

사설 IP는 일반적으로 라우터가 할당하며, 할당받은 사설 IP 주소는 사설 네트워크 상에서만 유효하다.  

그러나 사설 IP 주소만을 가지고는 외부 네트워크와 통신하기 어렵기 때문에  
라우터 혹은 공유기의 IP 주소를 변환하는 기술인 **NAT(Network Address Translation)** 기능을 사용한다.  

해당 기능을 사용하면, 사설 IP 주소를 외부 네트워크에 사용되는 공인 IP 주소로 변환하여 외부 네트워크와 통신한다.  

예를 들어, 사설 네트워크에서 출발한 패킷에 존재하는 사설 IP 주소(송신지)가 라우터를 거쳐 공인 IP로 변경한다.  

그리고, 외부 네트워크로부터 출발한 패킷에 존재하는 공인 IP 주소(수신지)는 NAT 기능을 통해,  
사설 IP 주소로 변경되고 나서 사설 네트워크 속 호스트에게 전달된다.  

NAT에서 주소 변환을 하기 위해서 내부적으로 공인 IP 주소와 사설 IP 주소가 대응되어 있는 NAT 변환 테이블을 사용한다.  

### **NAT 변환 테이블에서 공인 IP 주소와 사설 IP 주소는 일대일로 대응되어 있나?**

일대일 대응은 사설 IP 주소만큼 공인 IP가 필요하기 때문에 한계가 있다.  
그렇기 때문에, 일반적으로 공인 IP와 사설 IP가 일대일로 대응하지 않고,   
**NAPT(Network Address Port Translation)** 이라는 포트 기반의 NAT를 사용한다.  

해당 기능에서는 NAPT 변환 테이블에 IP 주소 쌍과 함께 포트도 함께 기록된다. 

ex. NAPT 변환 테이블의 예시

| **Private IP** | **Private Port** | **Public IP** | **Public Port** |
| --- | --- | --- | --- |
| 192.168.10.2 | 8000 | 1.2.3.4 | 8001 |
| 192.168.10.3 | 8000 | 1.2.3.4 | 8002 |
