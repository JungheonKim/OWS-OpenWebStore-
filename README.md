OWS(Open Web Store)
================================

Table of Contents　　　　　　　　　　<a id="top">　</a>
-------------------------
<dd>1	Introduction</dd>
<dd><a href="#2.OWS Resarch">2   OWS(Open Web Store)Resarch</a></dd>
<dd>　　2.1	OWS Requirement</dd>
<dd>　　2.2	OWS Use Case</dd>
<dd>　　2.3	OWS Architecture</dd>
<dd>　　　　2.3.1    Architecture 전체 구상도</dd>
<dd>　　　　2.3.2    Storefront의 모듈 관계 및 정의</dd>
<dd>　　　　2.3.3    SAM(Shared App Management)의 모듈 관계 및 정의</dd>
<dd>　　　　2.3.4    Policy의 모듈 관계 및 정의</dd>
<dd>　　2.4	OWS API List</dd>
<dd>　　　　2.4.1    OWS-1</dd>
<dd>　　　　2.4.2    OWS-2</dd>
<dd>　　　　2.4.3    OWS-3</dd>
<dd>　　　　2.4.4    OWS-4</dd>
<dd>　　　　2.4.5    OWS-5</dd>
<dd><a href="#3.OWS Reference Arch">3	OWS Reference Architecture</a></dd>
<dd>　　3.1	Storefront</dd>
<dd>　　3.2	SAM(Shared App Management)</dd>
<dd>　　3.3	Policy</dd>
<dd><a href="#4.OWS Interworking Scen">4	OWS Interworking Scenario</a></dd>
<dd>　　4.1	Application List Shared Procedure</dd>
<dd>　　4.2	Application Shared Procedure</dd>
<dd>　　4.3	Reaudition Result Transfer Procedure</dd>
<dd>　　4.4	Reaudit Shared Success Procedure</dd>
<dd>　　4.5	Application Charging Procedure</dd>
<dd>　　4.6	Application Deletion Procedure</dd>
<dd>　　4.7	Transfer Malicious & Bug Report From OriginStore Procedure</dd>
<dd>　　4.8	Transfer Malicious & Bug Report From RemoteStore Procedure</dd>
<dd>　　4.9	Application Update Procedure</dd>
<dd><a href="#5.OWS Manifest List">5	OWS Manifest List</a></dd>
<dd>　　5.1	W3C Widget, Chrome, Firefox Comparison</dd>
<dd>　　5.2	Manifest Standard Suggestions</dd>
<dd>　　　　5.2.1    Manifest표준제안</dd>
<dd><a href="#6.OWS Lifecycle Mana">6	Lifecycle Management</a></dd>
<dd>　　6.1	Lifecycle Requirement</dd>
<dd>　　6.2	Lifecycle Use Case</dd>
<dd>　　6.3	Lifecycle State Diagram</dd>
<dd>　　6.4	Lifecycle Sequence Diagram</dd>
<dd>A   References</dd>

1.Introduction
-------------------------------
<dd>
　스마트폰 등장과 함께 애플리케이션을 판매하는 마켓플레이스들이 통신사업자, 단말사업자, 플랫폼 사업자 구별 없이 우후죽순으로 생겨나고 있다. 전 세계 통신사업자와 국내 단말기 회사가 모여 통신사 및 장비 업체들이 사업자간 모바일 앱 콘텐츠를 공유, 활용하기 위해 WAC이 구성되었고, 각 플랫폼 별로 애플리케이션을 개발해야 하는 단점을 해결하기 위해 애플리케이션 플랫폼에 종속적이지 않은 웹 애플리케이션 스토어가 등장 하였다. 하지만 현재 WAC은 기술에만 집중하여 앱 개발자 커뮤니티를 활성화하지 못하였고, 애플과 구글의 운영체제가 빠르게 성장한 탓에 실패 하였다. 애플리케이션 스토어는 애플 앱 스토어와 같이 앱을 다운받아 설치 후 작동하는 네이티브 앱 스토어 와 HTML5, Javascript, CSS3등과 같은 표준 언어로 제작되어 ‘웹브라우저’에서 작동되는 웹 기반 애플리케이션인 설치형 웹 앱 스토어가 있다. 클라이언트의 운영 체제의 종류나 버전에 상관없이 작동되도록 표준 브라우저 기능을 사용하여 모든 스마트폰을 지원하기 위해 설치형 웹 애플리케이션이 등장 하였고, 브라우저 뿐 아니라 페이스북이 만든 앱 센터처럼 웹사이트 기반으로 운영되는 스토어도 생겨나기 시작하였다.

 
　웹사이트에서 애플리케이션을 다운받는 경우 브라우저에 상관없이 애플리케이션을 다운 받을 수 있다면 개발자 입장에서 브라우저별로 작업할 필요가 없다. 이를 위해 OWS는 웹 애플리케이션 스토어를 연동해 어떠한 애플리케이션을 사용하든 웹 애플리케이션이 플랫폼에 구속 받지 않고 모든 브라우저에서 동작 하도록 해야할 것이다. 따라서 본 연구는 OWS 상세 Architecture에 대한 변동사항을 더 자세히 알아보고 연동을 위한 Manifest표준제안 이나 Lifecycle에 대해 새롭게 살펴볼 것이다.


　그리고 나서 작년과 비교하여 Telco’s Application Store 의 요구사항에는 변동사항이 없는지에 대해 살펴볼 것이다. 그리고 작년에는 설치형 웹 애플리케이션 스토어간의 연동 요구사항과 시나리오로써 어떤 것이 필요한지 살펴보았다면, 이번에는 OWS의 참조모델이나 Manifest 표준 제안에 대한 관련연구를 분류해보고 향후 전망을 살펴보려 한다. 또한 작년과 비교하여 Mozilla, W3C, Chrome의 Manifest 분석 비교와 웹 스토어 비교도 살펴볼 것이다.


</dd>
<a id="2.OWS Resarch">2.OWS(Open Web Store)Resarch</a>
-------------------------------
###<dd>   　2.1	OWS Requirement</dd>
　본 연구에서 제안하는 OWS 는 TAS 의 기본 Requirement 에 연동에 대한 Requirement 를 추가하여 구성한다. 아래그림은 연동에 필요한 모듈을 나타낸 그림으로 기존 TAS 의 Storefront 모듈 내부에 타 Storefront 모듈과 애플리케이션 및 정보를 연동하기 위해 필요한 모듈과 Interface 를 추가한 확장된 Extended Storefront 이다. 클라이언트에게 직접적인 서비스를 제공하는 Storefront 를 연동을 위한 SAM(Shared App Management)과 정책에 관련된 Policy 모듈, Policy Provider 로 구성되어있다.
<center>
<img src="https://f.cloud.github.com/assets/5456705/1245165/153acfa6-2a99-11e3-9e98-3f27af831cf6.png" align="center"> 
</center>
　　
###<dd>　　2.2	OWS Use Case</dd>
<center>
![image](https://f.cloud.github.com/assets/5456705/1245131/3dab7bda-2a98-11e3-9103-83d07aa3f5fc.png)
</center>
　
###<dd>　　2.3	OWS Architecture</dd>
###<dd>　　　　2.3.1    Architecture 전체 구상도</dd>
<center>
![2 3 1](https://f.cloud.github.com/assets/5457979/1459052/7b27e2d2-43bb-11e3-913f-7a2d856da485.JPG)
</center>

　
###<dd>　　　　2.3.2    Storefront의 모듈 관계 및 정의</dd>
<center>
<dd>![2 3 2](https://f.cloud.github.com/assets/5457979/1474119/221761ca-4629-11e3-853f-cf7024b34e47.JPG)
</dd>
</center>

　
<h5><dd>●SAM Adapter</dd></h5>
<dd>　Storefront의 중앙 처리 장치로, Client로부터 요청받은 정보를 App Manager와 User Account Manager, Fee Manager로 보내고, 필요에 따라 다른 WebStore와 연동을 하기 위해 SAM(Shared App Management)의 RemoteStore Connector에게 정보를 보낸다.

　
</dd>
<h5><dd>●App Manager</dd></h5>
<dd>　App Repository에 App Data 추가, 삭제, 업데이트, 검색을 위한 전반적인 연산 처리를 담당한다.

　
</dd>
<h5><dd>●User Account Manager</dd></h5>
<dd>　Client의 개인 정보, 장바구니 리스트, 즐겨 찾기 리스트와 같은 정보를 Repository에 추가, 삭제변경, 업데이트 하기 위한 전반적인 연산 처리를 담당한다.

　
</dd>
<h5><dd>●Fee Manager</dd></h5>
<dd>　App 구매 시 결제를 담당하는 부분으로 Origin App과 Remote App의 구매 모두 관여한다. Client가 Origin App을 구매할 경우 일반적인 결제가 이루어지고, Remote App을 구매 할 경우는 일부 수수료를 제외하고 연동되어온 원래의 Store에게 나머지 금액을 전달한다.


　</dd> 
<h5><dd>●Origin App Repository</dd></h5>
<dd>　Origin Store에서 개발된 App Data들을 저장하고 있는 Repository로, Origin Developer가 App을 개발할 경우 그 App의 Data가 저장되는 부분이다.

　
</dd>
<h5><dd>●Remote App Repository</dd></h5>
<dd>　Remote Store에서 개발된 App Data들을 저장하고 있는 Repository로, Other Developer로부터  App이 개발되어 연동되어 왔을 경우 그 App의 Data가 저장되는 부분이다.

　
</dd>
<h5><dd>●User Account Repository</dd></h5>
<dd>　User Account Manager에서 연산의 결과로 생긴 Data들이 저장되는 Repository이다. Client의 개인 정보, 장바구니 정보, App 구매 기록 등의 Data가 저장된다.

　　
</dd>

###<dd>　　　　2.3.3    (SAM)Shared App Management의 모듈 관계 및 정의</dd>
<center>
![2 3 3](https://f.cloud.github.com/assets/5457979/1474129/5a5985ae-4629-11e3-901d-642b7c761604.JPG)
</center>

　
<h5><dd>●RemoteStore Connector</dd></h5>
<dd>　Storefront의 Information Processor로부터 요청을 받아 연동이 약속되어 있는 다른 Store로 통신을 하는 부분이다. App Data나 List에 대한 수신, 발신 모두 담당하며, 통신을 위해 필요한 Data를 Repository에서 추가, 삭제, 변경, 검색하는 연산 처리 작업도 함께 수행한다. 또한 수신, 발신 시 Policy에 App 검수 요청을 위해 Policy Information Exchanger에게 App ID를 전달한다.</dd>

　
<h5><dd>●OriginStore AppList Repository</dd></h5>
<dd>　Origin Developer에 의해 Storefront에 App이 등록되면 App에 대한 ID값을 넘겨받아 저장하고 있는 List Repository이다.</dd>

　
<h5><dd>●Remote Store AppList Repository</dd></h5>
<dd>　Remote Developer에 의해 개발된 App의 리스트가 RemoteStore로부터 연동되어 저장된 Repository이다. Policy에 의해 등록이 거부된 rejectedOtherApp List를 함께 보관한다.</dd>

　
<h5><dd>●Policy Connector</dd></h5>
<dd>　App 검수를 위해 RemoteStore Connector로부터 App ID를 넘겨받아 Policy의 SAM Connector에게 값을 전달한다.</dd>

　
###<dd>　　　　2.3.4    Policy의 모듈 관계 및 정의</dd>
<center>
![2 3 4policy](https://f.cloud.github.com/assets/5457979/1459093/374b5044-43c0-11e3-8e3b-db97523fbdfe.JPG)
</center>

　
<h5><dd>●Compare Unit</dd></h5>
<dd>　SAM에게 App ID를 넘겨 받아 OriginStore의 Policy와 App을 비교하여 검수를 수행하는 부분이다. Compare Unit에서 수행되는 검수의 결과에 따라 Origin App의 발신 가능 여부와 Other App의 등록 가능 여부를 결정한다. 또한 이미 등록이 거부됐던 rejectedOtherApp에 대해서 주기적으로 재검수를 수행하고 결과를 SAM에게 통보한다.</dd>

　
<h5><dd>●OriginStore Policy Repository</dd></h5>
<dd>　OriginStore의 Policy가 저장되어있는 Repository로, Policy Provider에 의해 관리되며 검수 시 필요한 Policy 정보를 보관하고 있다.</dd>

　
<h5><dd>●SAM Connector</dd></h5>
<dd>　SAM의 Policy Connector로부터 검수를 요청할 App ID를 넘겨받아 Compare Unit에게 전달한다.</dd>
<dd><a href="#top">top</a></dd>
###<dd>　　2.4	OWS API List</dd>


###<dd>　　　　2.4.1    OWS-1</dd>
<dd>　Storefront에서 수신 측 OWS로 전송할 애플리케이션 및 애플리케이션 리스트를 Shared App Management 모듈로 보내는데 사용되는 Interface이다.</dd>
<center>
![2 4 1](https://f.cloud.github.com/assets/5457979/1474139/904c5024-4629-11e3-8b59-b927e0c3bb7a.JPG)
</center>

　　　
<h5><dd>●Shared App Deletion ( Req. 4.2.8 )</dd></h5>
<dd>　개발자는 Storefront에 삭제요청을 한다. 삭제요청은 개발자가 속해있는 OWS뿐만 아니라 애플리케이션이 연동된 다른 OWS에게도 요청을 해야 하기 때문에 Shared App Management를 통한 연동을 필요로 한다. 다른 OWS (연동 된 OWS는 다수일 수 있다.)는 해당 애플리케이션을 삭제한 후에 기존 개발자가 속해있는 OWS에 결과를 통보 한다.)</dd>
<center>
<dd>![2 4 1-1](https://f.cloud.github.com/assets/5457979/1474155/c5e3cd66-4629-11e3-96d5-8453092c3f33.JPG)
</dd>
</center>
　　　　　　　　　　　**-SharedAppDeleteRequest**
<center>
<dd>![2 4 1 ows-1-2](https://f.cloud.github.com/assets/5457979/1459111/c4fe4f08-43c1-11e3-80fe-93ad5e8f7d90.JPG)</dd>
</center>
　　　　　　　　　　　**-SharedAppDeleteResponse**
<center>
<dd>![2 4 1 ows-1-3](https://f.cloud.github.com/assets/5457979/1459114/e65cfd5c-43c1-11e3-8f40-8a93dc94fa12.JPG)</dd>
</center>


　
<h5><dd>●Shared App Update( Req. 4.2.11)</dd></h5>
<dd>　개발자에 의해 업데이트 된 애플리케이션은 연동된 OWS에도 알려야 하므로 Shared App Management를 통한 연동이 필요하다.</dd>
<center>
<dd>![2 4 1 ows-1 -2](https://f.cloud.github.com/assets/5457979/1459119/4270f800-43c2-11e3-972e-68507e2bb611.JPG)</dd>
</center>
　　　　　　　　　　　**-SharedAppUpdateNotify**
<center>
<dd>![2 4 1 ows-1 -2-1](https://f.cloud.github.com/assets/5457979/1459120/9ac560d6-43c2-11e3-830b-27d8e40fbb80.JPG)</dd>
</center>
　　　　　　　　　　　**-SharedAppUpdateRequest**
<center>
<dd>![2 4 1 ows-1 -2-2](https://f.cloud.github.com/assets/5457979/1459121/9d0af7b6-43c2-11e3-955a-7ee978bacbd8.JPG)</dd>
</center>
　　　　　　　　　　　**-SharedAppUpdateResponse**
<center>
<dd>![2 4 1 ows-1 -2-3](https://f.cloud.github.com/assets/5457979/1459122/9f00e0c6-43c2-11e3-9ea8-4c5388b21a55.JPG)</dd>
</center>


　
<h5><dd>●Other OWS App List Request( Req. 4.2.1 )</dd></h5>
<dd>　Storefront는 다른 OWS에 있는 애플리케이션을 연동하기 위하여 애플리케이션 List를 요청해야 한다. 다른 OWS에 있는 애플리케이션 List는 Shared App Management에서 broadcasting 방식으로 뿌려주기 때문에 자신의 Shared App Management에 애플리케이션 List를 요청한다.</dd>
<center>           
<dd>![4 2 1](https://f.cloud.github.com/assets/5457979/1474201/7a31bf1c-462a-11e3-8a4d-c513704629f9.JPG)
</dd>
</center>
　　　　　　　　　　　　**-OtherOwsAppListRequest**
<center>
<dd>![4 2 1-1](https://f.cloud.github.com/assets/5457979/1474179/260cd2be-462a-11e3-9bd2-0e447bef9ea8.JPG)
</dd>
</center>
　　　　　　　　　　　　**-OtherOwsAppListResponse**
<center>
<dd>![4 2 1-2](https://f.cloud.github.com/assets/5457979/1474186/3eeb4f22-462a-11e3-9408-1ce18fbaed0b.JPG)
</dd>
</center>


　
<h5><dd>●Other OWS App Share (Req. 4.2.1 )</dd></h5>
<dd>　전송 받은 애플리케이션 List를 보고 자신의 스토어로 연동하고 싶은 애플리케이션을 골라 Shared App Management로 연동 요청을 하면 Shared App Management는 타 OWS에게 애플리케이션을 요청한 후 Policy에서 검수를 받은 뒤 Storefront에게 애플리케이션을 전송한다.</dd>
<center>
<dd>![2 4 1 ows-1 -4](https://f.cloud.github.com/assets/5457979/1459136/be6fdf6a-43c3-11e3-8538-72ca0b74d7d9.JPG)</dd>
</center>
　　　　　　　　　　　**-OtherOwsAppShareRequest**
<center>
<dd>![2 4 1 ows-1 -4-1](https://f.cloud.github.com/assets/5457979/1459137/bfce42a2-43c3-11e3-8209-dabed851078a.JPG)</dd>
</center>
　　　　　　　　　　　**-OtherOwsAppShareResponse**
<center>
<dd>![2 4 1 ows-1 -4-2](https://f.cloud.github.com/assets/5457979/1459138/c11399e6-43c3-11e3-89cd-fa761d7dc2a1.JPG)</dd>
</center>

　
<h5><dd>●Shared App Payment(Req. 4.2.12)</dd></h5>
<dd>　애플리케이션 과금 과정에서 Shared App Management 과정을 거치는 경우는 다른 OWS에서 연동한 애플리케이션을 Client가 구매했을 경우이다. 이 경우 다른 OWS에 있는 개발자에게 돈을 지불해야 하기 때문에 Client가 속한 OWS는 애플리케이션 판매금액 중 자신의 판매 수수료를 제외한 나머지를 애플리케이션을 연동해온 OWS에게 보내야 한다.</dd>
<center>
<dd>![2 4 1 ows-1 -5](https://f.cloud.github.com/assets/5457979/1459163/4ed4f6ca-43c5-11e3-8f1f-ac08920afa4b.JPG)</dd>
</center>
　　　　　　　　　　　**-SharedAppPaymentSend**
<center>
<dd>![2 4 1 ows-1 -5-1](https://f.cloud.github.com/assets/5457979/1459164/50a0be26-43c5-11e3-9a9f-813693aff8d3.JPG)</dd>
</center>
　　　　　　　　　　　**-SharedAppPaymentResult**
<center>
<dd>![2 4 1 ows-1 -5-2](https://f.cloud.github.com/assets/5457979/1459165/5353b45c-43c5-11e3-9200-29198af21fcd.JPG)</dd>
</center>

　
<h5><dd>●Shared App Refund (Req. 4.2.13)</dd></h5>
<dd>　연동을 해온 애플리케이션에 대해 소비자의 환불요청이 들어오면 Shared App Management를 통해 타 OWS에게도 환불요청을 해야 한다.</dd>
<center>
<dd>![2 4 1 ows-1 -6](https://f.cloud.github.com/assets/5457979/1459170/c23b53c0-43c5-11e3-94ae-e75e3926179b.JPG)</dd>
</center>
　　　　　　　　　　　**-SharedAppRefundRequest**
<center>
<dd>![2 4 1 ows-1 -6-1](https://f.cloud.github.com/assets/5457979/1459171/c37bc5f8-43c5-11e3-9594-eaff63dc4cdb.JPG)</dd>
</center>
　　　　　　　　　　　**-SharedAppRefundResponse**
<center>
<dd>![2 4 1 ows-1 -6-2](https://f.cloud.github.com/assets/5457979/1459172/c5bb0388-43c5-11e3-87e0-441b604f9b9b.JPG)</dd>
</center>

　
<h5><dd>●Shared App Feedback(Req. 4.2.6)</dd></h5>
<dd>　Client에 의해 제출된 피드백이 다른 OWS에서 연동한 애플리케이션에 대한 피드백인 경우 이 피드백은 Shared App Management를 통해 broadcasting된 후 다른 OWS에 있는 개발자에게 피드백 요청이 들어가게 된다.</dd>
<center>
<dd>![2 4 1 ows-1 -7](https://f.cloud.github.com/assets/5457979/1459178/24b0a852-43c6-11e3-9b5e-e8bb8b6e98e4.JPG)</dd>
</center>
　　　　　　　　　　　**-SharedAppRefundResponse**
<center>
<dd>![2 4 1 ows-1 -7-1](https://f.cloud.github.com/assets/5457979/1459179/260eccd8-43c6-11e3-9420-d42df386b3f2.JPG)</dd>
</center>
　　　　　　　　　　　**-SharedAppRefundResponse**
<center>
<dd>![2 4 1 ows-1 -7-2](https://f.cloud.github.com/assets/5457979/1459180/272d324e-43c6-11e3-978c-af9ad915ec23.JPG)</dd>
</center>

　
<h5><dd>●Shared App Selection</dd></h5>
<dd>　전달될 애플리케이션의 정보가 Storefront에서 SAM으로 전송되는 인터페이스이다. 주로 타인에게 애플리케이션을 추천, 선물 등에 쓰이는 API가 필요하다.</dd>
<center>
<dd>![2 4 1 ows-1 -8](https://f.cloud.github.com/assets/5457979/1459185/a6268db6-43c6-11e3-9a75-68d7d9e05b67.JPG)</dd>
</center>
　　　　　　　　　　**-Shared App Selection  Request**
<center>
<dd>![2 4 1 ows-1 -8-1](https://f.cloud.github.com/assets/5457979/1459186/a7884050-43c6-11e3-8651-5c855f9a6a50.JPG)</dd>
</center>
　　　　　　　　　　**-Shared App Selection  Response**
<center>
<dd>![2 4 1 ows-1 -8-2](https://f.cloud.github.com/assets/5457979/1459187/a87c643c-43c6-11e3-8f9b-321657f8dbef.JPG)</dd>
</center>

　
<h5><dd>●User Report Application</dd></h5>
<dd>　사용자가 애플리케이션에 대해 이상한 점을 발견하거나 건의할 사항을 Storefront에서 SAM으로  쓰이는 전달하는 API가 필요하다.</dd>
<center>
<dd>![2 4 1 ows-1 -9](https://f.cloud.github.com/assets/5457979/1459194/00e81986-43c7-11e3-9a2e-0feab84505b0.JPG)</dd>
</center>
　　　　　　　　　　**-User Report Application  Request**
<center>
<dd>![2 4 1 ows-1 -9-1](https://f.cloud.github.com/assets/5457979/1459195/01d42736-43c7-11e3-8aad-c53599aa2095.JPG)</dd>
</center>
　　　　　　　　　　**-User Report Application  Response**
<center>
<dd>![2 4 1 ows-1 -9-2](https://f.cloud.github.com/assets/5457979/1459196/03e57836-43c7-11e3-9ef7-179ab07a7cbb.JPG)</dd>
</center>

###<dd>　　　　2.4.2    OWS-2</dd>
<dd>　OWS간의 연동을 위한 모듈인 Shared App Management를 통해 애플리케이션 관련 다양한 정보들의 전송을 위한 Interface 이다.</dd>
<center>
<dd>![2 4 1 ows-2](https://f.cloud.github.com/assets/5457979/1459199/5a25131e-43c7-11e3-898e-cdaa99972967.JPG)
</dd>
</center>

　
<h5><dd>●Application registration (Req. 4.2.1)</dd></h5>
<dd>　Origin OWS에 새로운 애플리케이션이 등록이 되면 이 정보를 연결되어 있는 다른 여러 OWS들에게 애플리케이션 정보를 전달한다.</dd>
<center>
<dd>![4 2 1](https://f.cloud.github.com/assets/5457979/1474225/beb0c002-462a-11e3-807b-f9d47e41b592.JPG)
</dd>
</center>
　　　　　　　**-Application registration Request**
<center>
<dd>![2 2 1](https://f.cloud.github.com/assets/5457979/1474260/40289510-462b-11e3-9068-1453d35a86f1.JPG)
</dd>
</center>
　　　　　　　**-Application registration Response**
<center>
<dd>![2 1 2](https://f.cloud.github.com/assets/5457979/1474259/3ba18984-462b-11e3-8556-665546c1ca41.JPG)</dd>
</center>

　
<h5><dd>●Application Deletion transfer (Req. 4.2.8)</dd></h5>
<dd>　Origin OWS에서 어떠한 이유가 생겨서 애플리케이션이 삭제가 되면 공유된 애플리케이션이 삭제가 되었다고 연결된 모든 OWS들에게 전달해야 한다.</dd>
<center>
<dd>![2 2](https://f.cloud.github.com/assets/5457979/1474270/832cac84-462b-11e3-9a8b-84bb13558b3a.JPG)</dd>
</center>
　　　　　　　**-Application Deletion Request**
<center>
<dd>![2 2 1](https://f.cloud.github.com/assets/5457979/1474271/832d49fa-462b-11e3-8d68-add413ceae36.JPG)</dd>
</center>
　　　　　　　**-Application Deletion Response**
<center>
<dd>![2 2 2](https://f.cloud.github.com/assets/5457979/1474272/832da92c-462b-11e3-881e-dbd9c9e1cc9d.JPG)
</dd>
</center>

　
<h5><dd>●Application Download Request (Req. 4.2.10)</dd></h5>
<dd>　Origin OWS에서 애플리케이션 정보에 맞는 애플리케이션 내용을 다운로드 할 수 있도록 URL등의 애플리케이션을 넘겨준다.</dd>
<center>
<dd>![2 3](https://f.cloud.github.com/assets/5457979/1474295/bbe30aaa-462b-11e3-9e56-61b197ab3ba2.JPG)
</dd>
</center>
　　　　　　　**-Application download Request**
<center>
<dd>![2 3 1](https://f.cloud.github.com/assets/5457979/1474294/bbe3012c-462b-11e3-9074-9d4462654a8f.JPG)</dd>
</center>
　　　　　　　**-Application download Request**
<center>
<dd>![2 3 2](https://f.cloud.github.com/assets/5457979/1474293/bbe05b70-462b-11e3-8a8c-07bda091b6cb.JPG)</dd>
</center>

　
<h5><dd>●Application feedback transfer (Req. 4.2.6)</dd></h5>
<dd>　하나의 애플리케이션에 대하여 애플리케이션을 공유 받은 OWS에서 등록한 평점과 댓글을 원래 애플리케이션이 등록되어 공유를 시작한 OWS로 전송을 한다.</dd>
<center>
<dd>![2 4](https://f.cloud.github.com/assets/5457979/1474313/edb16af4-462b-11e3-9d55-18061b2c4985.JPG)</dd>
</center>
　　　　　　　　**-Application feedback Request**
<center>
<dd>![2 4 1](https://f.cloud.github.com/assets/5457979/1474312/edb10960-462b-11e3-8a8c-3ff1848af72b.JPG)</dd>
</center>
　　　　　　　　**-Application feedback Response**
<center>
<dd>![2 4 2](https://f.cloud.github.com/assets/5457979/1474314/edb8210a-462b-11e3-9f88-c669820add2f.JPG)
</dd>
</center>

　
<h5><dd>●Application Total Feedback Information (Req. 4.2.14)</dd></h5>
<dd>　하나의 애플리케이션에 대해서 공유된 각각의 OWS들에서 전달된 평점과 댓글을 가지고 총 평점을 계산하고 댓글을 정리한 뒤에 이 정보를 다시 각각의 OWS들에게 전달한다.</dd>
<center>
<dd>![2 5](https://f.cloud.github.com/assets/5457979/1474325/19fdca1c-462c-11e3-9208-75fca778e58f.JPG)</dd>
</center>
　　　　　　　**-Application total feedback Request**
<center>
<dd>![2 5 1](https://f.cloud.github.com/assets/5457979/1474324/19fd6ee6-462c-11e3-9602-834d2a6c9ba8.JPG)</dd>
</center>
　　　　　　　**-Application total feedback Response**
<center>
<dd>![2 5 2](https://f.cloud.github.com/assets/5457979/1474323/19fcd0b2-462c-11e3-8015-914389c829e3.JPG)</dd>
</center>

　
<h5><dd>●Malicious & Bug Report (Req. 4.2.6)</dd></h5>
<dd>　Origin OWS에서 어떠한 이유가 생겨서 애플리케이션이 삭제가 되면 공유된 애플리케이션이 삭제가 되었다고 연결된 모든 OWS들에게 전달해야 한다.</dd>
<center>
<dd>![2 6](https://f.cloud.github.com/assets/5457979/1474337/454c9068-462c-11e3-9aa4-3131c09cbd03.JPG)</dd>
</center>
　　　　　　**-Malicious & Bug Report Request**
<center>
<dd>![2 6 1](https://f.cloud.github.com/assets/5457979/1474338/4552feb2-462c-11e3-983e-dec1e58317ee.JPG)</dd>
</center>
　　　　　　**-Malicious & Bug Report Response**
<center>
<dd>![2 6 2](https://f.cloud.github.com/assets/5457979/1474336/454a3e58-462c-11e3-864d-13d83c8d61f4.JPG)</dd>
</center>

　
<h5><dd>●Application charge delivery (Req. 3.2.2)</dd></h5>
<dd>　애플리케이션을 공유 하는 OWS에 있는 애플리케이션 개발자에게 수익을 분배해야 함으로 애플리케이션을 공유 받는 OWS는 판매금액 중 자신의 판매 수수료를 제외한 나머지 수익을 애플리케이션을 공유 하는 OWS로 전달해야 한다.</dd>
<center>
<dd>![2 4 2 ows-2 -7](https://f.cloud.github.com/assets/5457979/1459241/c98887c0-43c9-11e3-8bab-4428ef212d0c.JPG)</dd>
</center>
　　　　　　　　**-Malicious & Bug Report Request**
<center>
<dd>![2 4 2 ows-2 -7-1](https://f.cloud.github.com/assets/5457979/1459242/cae48b64-43c9-11e3-9d33-ededc3e46628.JPG)</dd>
</center>
　　　　　　　　**-Malicious & Bug Report Request**
<center>
<dd>![2 4 2 ows-2 -7-2](https://f.cloud.github.com/assets/5457979/1459243/ce8c533c-43c9-11e3-872c-317ea5e4f218.JPG)</dd>
</center>

　
<h5><dd>●Application List Request Transfer ( Req. 4.2.1 )</dd></h5>
<dd>　Origin Storefront에서 애플리케이션 리스트를 Other Storefront까지 전송하기 위해 중간에 Origin Shared App Management에서 Other Shared App Management로 전송해야 하는 API가 필요하다.  </dd>
<center>
<dd>![2 4 2 ows-2 -8](https://f.cloud.github.com/assets/5457979/1459247/1d0b8dfc-43ca-11e3-9878-189d23adefbb.JPG)</dd>
</center>
　　　　　　　**-ApplicationListRequest**
<center>
<dd>![2 4 2 ows-2 -8-1](https://f.cloud.github.com/assets/5457979/1459248/1ec64d3a-43ca-11e3-9456-ae716084192e.JPG)</dd>
</center>
　　　　　　**-ApplicationListResponse**
<center>
<dd>![2 4 2 ows-2 -8-2](https://f.cloud.github.com/assets/5457979/1459249/1fcaad8e-43ca-11e3-8468-5d0c5f89240d.JPG)</dd>
</center>

　
<h5><dd>●Application Policy Report Transfer </dd></h5>
<dd>　Remote Storefront는 검수 결과로 인해 거부되었던 App에 대해서 주기적으로 재검수를 실시한다. 이 때 재검수에 대한 결과를 개발자에게 전달하는 API가 필요하다.</dd>
<center>
<dd>![2 4 2 ows-2 -9](https://f.cloud.github.com/assets/5457979/1459253/7986dc94-43ca-11e3-843c-a081f8c34fe3.JPG)</dd>
</center>
　　　　**-ApplicationPolicyReportRequest**
<center>
<dd>![2 4 2 ows-2 -9-1](https://f.cloud.github.com/assets/5457979/1459254/7c6c9f02-43ca-11e3-8612-bb4072b47361.JPG)</dd>
</center>
　　　　**-ApplicationPolicyReportResponse**
<center>
<dd>![2 4 2 ows-2 -9-2](https://f.cloud.github.com/assets/5457979/1459255/80761830-43ca-11e3-99f9-cae9f6fdd02a.JPG)</dd>
</center>

　
<h5><dd>●Application Selected Transfer</dd></h5>
<dd>　사용자가 선택한 애플리케이션들을 모아 SAM에서 SAM으로 전달하는 API가 필요하다.</dd>
<center>
<dd>![2 4 2 ows-2 -10](https://f.cloud.github.com/assets/5457979/1459260/dab06c9c-43ca-11e3-8271-f4a06fbe9c36.JPG)</dd>
</center>
　　　　**-Application Selected Transfer Request**
<center>
<dd>![2 4 2 ows-2 -10-1](https://f.cloud.github.com/assets/5457979/1459261/dc2f6b2c-43ca-11e3-829e-bc9a73fff1b2.JPG)</dd>
</center>
　　　　**-Application Selected Transfer Response**
<center>
<dd>![2 4 2 ows-2 -10-2](https://f.cloud.github.com/assets/5457979/1459262/ddbf25c2-43ca-11e3-8ab0-7fcb2e14047f.JPG)</dd>
</center>

　
<h5><dd>●Application Update Report</dd></h5>
<dd>　업데이트 할 애플리케이션이 있음을 Remote SAM에게 알리는 API가 필요하다.</dd>
<center>
<dd>![2 4 2 ows-2 -11](https://f.cloud.github.com/assets/5457979/1459264/1cdd3f3c-43cb-11e3-949b-a0eb022db7e3.JPG)</dd>
</center>
　　　　**-Application Update ReportRequest**
<center>
<dd>![2 4 2 ows-2 -11-1](https://f.cloud.github.com/assets/5457979/1459265/1f43bbfc-43cb-11e3-9957-af879ed1881a.JPG)</dd>
</center>
　　　　**-Application Update ReportResponse**
<center>
<dd>![2 4 2 ows-2 -11-2](https://f.cloud.github.com/assets/5457979/1459266/1fa30558-43cb-11e3-8af1-e65962490e02.JPG)</dd>
</center>

　
###<dd>　　　　2.4.3    OWS-3</dd>
<dd>　검수 받은 애플리케이션 및 인접 OWS에게 전송 받은 애플리케이션을 등록하기 위해 Storefront에 전송하는데 사용되는 Interface 이다.</dd>
<center>
<dd>![2 4 3 ows-3](https://f.cloud.github.com/assets/5457979/1459268/a6b11fda-43cb-11e3-93f5-479daafd7a02.JPG)
</dd>
</center>

　
<h5><dd>●Shared App List( Req. 4.2.1 )</dd></h5>
<dd>　스토어에 공유할 애플리케이션 목록을 전달받는다. 여러 애플리케이션을 동시에 받아서 수행 할 수 있으며 전달하는 목록에는 애플리케이션이 등록된 원래 스토어의 주소와 애플리케이션 이름, URL등이 저장된다.</dd>
<center>
<dd>![2 4 3 ows 3 -1](https://f.cloud.github.com/assets/5457979/1459270/ee8f7ba8-43cb-11e3-95c7-0c6b0c7549dc.JPG)</dd>
</center>
　　　　　　**-SharedAppListRequest**
<center>
<dd>![2 4 3 ows 3 -3](https://f.cloud.github.com/assets/5457979/1459271/f02a9d12-43cb-11e3-8cc4-12348bf10177.JPG)</dd>
</center>
　　　　　　**-SharedAppListResponse**
<center>
<dd>![2 4 3 ows 3 -2](https://f.cloud.github.com/assets/5457979/1459272/f083c5cc-43cb-11e3-9d37-3953f433d5ff.JPG)</dd>
</center>

　
<h5><dd>●Shared App Transfer( Req.4.2.1 )</dd></h5>
<dd>　공유할 애플리케이션에 대해서 애플리케이션 정보를 요청한 스토어와 애플리케이션이 원래 등록된 스토어간에 어떤 애플리케이션이 공유 될 것이며 어느 스토어끼리 공유할 것인가를 정해준다. 또한 애플리케이션을 연동된 상황이 아닌 전달받은 상황에서도 인터페이스가 사용되어 데이터가 전달된다.</dd>
<center>
<dd>![2 4 3 ows-3-2](https://f.cloud.github.com/assets/5457979/1459281/479c8a1a-43cc-11e3-9b65-0d642f4a22e1.JPG)</dd>
</center>
　　　　　　**-SharedAppListResponse**
<center>
<dd>![2 4 3 ows-3-2-1](https://f.cloud.github.com/assets/5457979/1459279/479632d2-43cc-11e3-8636-7843410a11d9.JPG)</dd>
</center>
　　　　　　**-SharedAppListResponse**
<center>
<dd>![2 4 3 ows-3-2-2](https://f.cloud.github.com/assets/5457979/1459280/479647e0-43cc-11e3-8709-923f6a62ed07.JPG)</dd>
</center>

　
<h5><dd>●Malicious Shared App Report( Req. 4.2.6 )</dd></h5>
<dd>　다른 OWS에서 연동해 간 애플리케이션을 사용하는 Client로부터 불량 애플리케이션 신고가 들어올 경우에 불량 애플리케이션에 대한 정보는 Shared App Management를 통해 현재 OWS에 있는 개발자에게 전해져야 한다.</dd>
<center>
<dd>![2 4 3 ows-3-3](https://f.cloud.github.com/assets/5457979/1459282/99cf09e8-43cc-11e3-8257-818dace65b12.JPG)</dd>
</center>
　　　　　　**-MaliciousSharedAppReport**
<center>
<dd>![2 4 3 ows-3-3-1](https://f.cloud.github.com/assets/5457979/1459283/9a53ec1c-43cc-11e3-8464-3d719b81f3ce.JPG)</dd>
</center>
　　　　　　**-MaliciousSharedAppResponse**
<center>
<dd>![2 4 3 ows-3-3-2](https://f.cloud.github.com/assets/5457979/1459285/9e1593aa-43cc-11e3-8786-432d04e8512e.JPG)</dd>
</center>

　
<h5><dd>●Shared App Refund( Req. 4.2.13 )</dd></h5>
<dd>　개발자는 현재 OWS에 있지만 환불요청이 다른 OWS에 있는 Client에서 왔을 경우 현재 OWS에서 환불이 시작 되야 하기 때문에 Shared App Management를 통해 환불요청이 들어온다.</dd>
<center>
<dd>![2 4 3 ows-3-4](https://f.cloud.github.com/assets/5457979/1459289/fbd15de4-43cc-11e3-87cf-db1f0ff66c32.JPG)</dd>
</center>
　　　　　　**-SharedAppRefundRequest**
<center>
<dd>![2 4 3 ows-3-4-1](https://f.cloud.github.com/assets/5457979/1459288/fbcd7080-43cc-11e3-9b6a-44420dda8d6c.JPG)</dd>
</center>
　　　　　　**-SharedAppRefundResponse**
<center>
<dd>![2 4 3 ows-3-4-2](https://f.cloud.github.com/assets/5457979/1459287/fbcb2fbe-43cc-11e3-982a-5d3b77f49a92.JPG)</dd>
</center>

　
<h5><dd>●Last App Pay Request ( Req. 4.2.12 )</dd></h5>
<dd>　Other OWS에서 구매한 애플리케이션이 Origin Storefront에서 연동한 애플리케이션일 경우 Other OWS에서 판매수수료를 제외한 나머지를 Shared App Management를 통해서 Origin Storefront로 전송해야 한다.</dd>
<center>
<dd>![2 4 3 ows-3-5](https://f.cloud.github.com/assets/5457979/1459292/458131da-43cd-11e3-8f48-bc3d68fda529.JPG)</dd>
</center>
　　　　　　**-LastAppPayRequest**
<center>
<dd>![2 4 3 ows-3-5-1](https://f.cloud.github.com/assets/5457979/1459294/4585da78-43cd-11e3-8f1c-cf340d81c653.JPG)</dd>
</center>
　　　　　　**-LastAppPayRequest**
<center>
<dd>![2 4 3 ows-3-5-2](https://f.cloud.github.com/assets/5457979/1459293/45818c16-43cd-11e3-96df-a171d1444396.JPG)</dd>
</center>

　
<h5><dd>●Application Policy Report Transfer </dd></h5>
<dd>　Remote Storefront는 검수 결과로 인해 거부되었던 App에 대해서 주기적으로 재검수를 실시한다. 이 때 재검수에 대한 결과를 개발자에게 전달하는 API가 필요하다.</dd>
<center>
<dd>![2 4 3 ows-3-6](https://f.cloud.github.com/assets/5457979/1459295/87906ba4-43cd-11e3-88d3-c32936b9705f.JPG)</dd>
</center>
　　　　　　**-ApplicationPolicyReportRequest**
<center>
<dd>![2 4 3 ows-3-6-1](https://f.cloud.github.com/assets/5457979/1459297/8792f7ac-43cd-11e3-8dea-a994ff8831cd.JPG)</dd>
</center>
　　　　　　**-ApplicationPolicyReportResponse**
<center>
<dd>![2 4 3 ows-3-6-2](https://f.cloud.github.com/assets/5457979/1459296/8792262e-43cd-11e3-98e2-17c9dcce7566.JPG)</dd>
</center>

　
<h5><dd>●Shared App Info Deletion  </dd></h5>
<dd>　공유된 애플리케이션들 중에서 삭제되어야 할 애플리케이션의 정보를 SAM이 Storefront로 전달한다.</dd>
<center>
<dd>![2 4 3 ows-3-7](https://f.cloud.github.com/assets/5457979/1459305/d3106a16-43cd-11e3-85dd-cac2a099e7ab.JPG)</dd>
</center>
　　　　　**-Shared App Info DeletionRequest**
<center>
<dd>![2 4 3 ows-3-7-1](https://f.cloud.github.com/assets/5457979/1459306/d3109798-43cd-11e3-82d8-461abf0e7476.JPG)</dd>
</center>
　　　　　**-Shared App Info DeletionResponse**
<center>
<dd>![2 4 3 ows-3-7-2](https://f.cloud.github.com/assets/5457979/1459304/d30942a4-43cd-11e3-9667-34c337a3426e.JPG)</dd>
</center>

　
###<dd>　　　　2.4.4    OWS-4</dd>
<dd>　OWS-4는 수신 측 OWS에서 전송 받은 애플리케이션을 검수하는데 사용되는 Interface이다.</dd>
<center>
<dd>![ows-4](https://f.cloud.github.com/assets/5457979/1473595/186d9460-461e-11e3-8bd6-4db1c8ea1f22.JPG)
</dd>
</center>

　
<h5><dd>●ReceiveApplication Check ( Req. 4.2.2 )</dd></h5>
<dd>　애플리케이션의 심의 기준이 나라, 혹은 OWS마다 다를 수 있기에 OWS간에 연동되어진  애플리케이션을 수신 시 애플리케이션을 검수한다.</dd>
<center>
<dd>![2 4 4 ows-4-1](https://f.cloud.github.com/assets/5457979/1459313/61f8c8f4-43ce-11e3-9c35-b899e789f639.JPG)</dd>
</center>
　　　　　**-ReceiveApp Info Check Request**
<center>
<dd>![2 4 4 ows-4-2](https://f.cloud.github.com/assets/5457979/1459314/61f98ef6-43ce-11e3-96aa-39f04c89612f.JPG)</dd>
</center>
　　　　　**-ReceiveApp Info Check Response**
<center>
<dd>![2 4 4 ows-4-3](https://f.cloud.github.com/assets/5457979/1459315/61fab4d4-43ce-11e3-9402-8be4ea6e2fa8.JPG)</dd>
</center>

　　
<h5><dd>●RejectedApplicationList Transfer </dd></h5>
<dd>　App Data를 연동했을 시 정책에 맞지 않아 등록이 거부될 수 있다. 그 때 거절된 App 리스트에 관하여 주기적으로 재검수가 이루어지는데, 이때 SAM이 저장하고 있던 거절된 App 리스트를 Policy에게 전송하는 API가 필요하다.</dd>
<center>
<dd>![2 4 4 ows-4-3](https://f.cloud.github.com/assets/5457979/1459330/54de309a-43cf-11e3-8f74-d8f1d8597efe.JPG)</dd>
</center>
　　　　　**-TransferApp Info Check Request**
<center>
<dd>![2 4 4 ows-4-3-1](https://f.cloud.github.com/assets/5457979/1459329/54dc9c44-43cf-11e3-96a1-5abb485a1005.JPG)</dd>
</center>
　　　　　**-TransferApp Info Check Request**
<center>
<dd>![2 4 4 ows-4-3-2](https://f.cloud.github.com/assets/5457979/1459328/54dba85c-43cf-11e3-9ad6-32c973354f88.JPG)</dd>
</center>

　
###<dd>　　　　2.4.5    OWS-5</dd>
<dd>　OWS-5는 OWS-4를 통한 애플리케이션 검수가 통과 되지 않은 경우 지속적으로 해당 애플리케이션에 대한 Report를 보내는데 사용되는 Interface 이다.</dd>
<center>
<dd>![2 4 5 ows-5](https://f.cloud.github.com/assets/5457979/1459334/9589c726-43cf-11e3-814d-03633c9a8cee.JPG)</dd>
</center>

　
<h5><dd>●Application Policy Report ( Req. 4.2.2 ) </dd></h5>
<dd>　개발자에게 Policy 정책을 반영한 결과를 통보해 주기 위해 OWS의 Policy가 애플리케이션을 검수하고 주기적으로 애플리케이션 Policy Report를 보낸다.</dd>
<center>
<dd>![2 4 5 ows-5-1](https://f.cloud.github.com/assets/5457979/1459339/d868295c-43cf-11e3-8452-ab2a261ab708.JPG)</dd>
</center>
　　　　　　　　　　**-Application policy Report**
<center>
<dd>![2 4 5 ows-5-1-2](https://f.cloud.github.com/assets/5457979/1459338/d85f9878-43cf-11e3-9d26-7ea3a43c7a34.JPG)
</dd>
</center>
　　　　　　　　**-Application policy Response**
<center>
<dd>
![2 4 5 ows-5-1-3](https://f.cloud.github.com/assets/5457979/1459337/d85eaa9e-43cf-11e3-8655-16be298e8d06.JPG)
</dd>
</center>

　
<a id="3.OWS Reference Arch">3.OWS Reference Architecture</a>
-------------------------------
###<dd>　　3.1	Storefront</dd>
　Storefront 모듈의 중앙 처리 내부 모듈로, 클라이언트 또는 개발자로부터 요청 받은 정보를애플리케이션 관리자(App Manager)나 계정 관리자(Account Manager)로 전달한다. 또한,애플리케이션 연동 정보 전달을 위해 SAM에게 정보를 전달한다. 애플리케이션의 추가, 삭제,
업데이트, 검색 연산을 수행하는 애플리케이션 관리자는 애플리케이션을 카테고리에 따라 분류한다. 계정 관리자는 클라이언트의 개인 정보, 장바구니 리스트, 즐겨 찾기 리스트와 같은 정보를 사용자 계정 저장소(User Account Repository)에 추가, 삭제, 변경 등의 연산을
수행한다. 이 뿐만 아니라 클라이언트가 애플리케이션을 구매할 때 발생하는 요금이나 연동된 애플리케이션으로부터 애플리케이션으로부터 애플리케이션으로부터 발생하는 발생하는 수수료에 수수료에 관한 처리를 처리를 수행한다 수행한다.

　애플리케이션 애플리케이션 저장소 (App Repository)는OriginStore 에서 개발되었거나 RemoteStore에서 연동되어온 애플리케이션을 저장하고 있는 저장소이며, 사용자 계정 저장소는 개발자를 포함한 사용자의 계정 정보를 보관하는 저장소이다.
<center> 
<dd>
![3 1storefront](https://f.cloud.github.com/assets/5457979/1245068/9fac29c6-2a96-11e3-9492-bb89692dcc1f.PNG)
</dd>
</center>

　
###<dd>　　3.2	SAM(Shared App Management)</dd>
　SAM(Shared App Management)은 RemoteStore 커넥터(Connecter) 모듈과 저장소 2개로 이루어져 있다. 

　RemoteStore커넥터는 Storefront 의 SAM어댑터로부터 요청을 받아 연동이 약속되어 있는 다른 스토어로 통신을 하는 부분이다. 애플리케이션이나 애플리케이션 리스트에 대한 수신, 발신을 모두 담당하며, Policy 모듈에 검수를 요청할 수 있다. RemoteStore커넥터는 통신에 관련된 부분 이외에도 저장소의 값을 추가, 삭제, 변경하는 연산도 함께 수행한다.

　애플리케이션 리스트 저장소(App List Repository)는 OrignStore에서 개발되었거나 RemoteStore에서 연동되어 온 애플리케이션 리스트를 저장하는 저장소이며, Storefront는 SAM의 애플리케이션 리스트 저장소로부터 애플리케이션  ID를 참조 받아 다른 스토어에게 연동을 요청한다. 애플리케이션 리스트 저장소에는 Policy 모듈로부터 연동이 미승인된 애플리케이션 리스트가 포함되어 있다. 또한 SAM에는 연동 요청을 위해서  연동이 약속된 다른 애플리케이션 스토어의 URL를 보관하는 RemoteStore URL리스트 저장소(RomoteStore URL List Repository)를 가지고 있다.
<center>
<dd>
![3 2sam](https://f.cloud.github.com/assets/5457979/1245083/0542975c-2a97-11e3-8d99-8a6c300372ca.PNG)
</dd>
</center>

　
###<dd>　　3.3	Policy</dd>
　애플리케이션 검수를 수행하는 Policy 모듈은 SAM으로부터 애플리케이션 ID를 전달받아 검수를 실시하는 검수 모듈(Compare Unit)과 
정책을 보관하고 있는 정책 저장소(Policy Repository)를 가지고 있다. 검수 모듈에서는 연동과 관련하여 다른 스토어로 발신이 가능한가, 수신한 애플리케이션이 등록 가능한가 등에 대해서 검수를 실시하고 이에 따른 승인 및 미승인 정보를 SAM에게 전달한다. 
<center>
<dd>
![3 3polish](https://f.cloud.github.com/assets/5457979/1245086/16d66ed0-2a97-11e3-990b-04b91aba849e.PNG)
</dd>
</center>
<dd><a href="#top">top</a></dd>

<a id="4.OWS Interworking Scen">4.OWS Interworking Scenario</a>
-------------------------------
###<dd>　　4.1	Application List Shared Procedure</dd>
　애플리케이션 연동을 위해서 평상시에 각 스토어는 애플리케이션 리스트를 연동한다. OriginStore에서 개발된 애플리케이션은 SAM에 있는 애플리케이션 리스트 저장소에 리스트를 보관하고 있는데, RemoteStore 커넥터가 RemoteStore URL 리스트 저장소로부터 연동이 약속된 스토어의 URL를 참조하여 각 스토어로 리스트를 연동한다. RemoteStore SAM 내부에 있는 RemoteStore 커넥터는 애플리케이션 리스트를 전달받아 애플리케이션 리스트 저장소에 저장한다. 
<dd>
![4 1app list shared procedure](https://f.cloud.github.com/assets/5457979/1245117/dbe96772-2a97-11e3-9f99-16ea956df445.PNG)
</dd>

　
###<dd>　　4.2	Application Shared Procedure</dd>
　RemoteStore로 애플리케이션 리스트 연동이 완료되면 Remote Storefront는 SAM을 통해서 연동하고자 하는 애플리케이션을 OriginStore로 요청한다. 연동을 요청받은 OriginStore는 해당 애플리케이션을 발신하기 전에 Policy 모듈에게 검수를 요청한다. 이 때 Policy 모듈은 애플리케이션이 연동에 적합한 지에 대해서 버전이나 상태 등을 검수한다. 검수에서 통과된 애플리케이션은RemoteStore
로 전송을 하고, 이를 전달받은 RemoteStore의 SAM은 연동된 애플리케이션을 Policy로 검수를 요청한다. 모든 검수가 완료된 애플리케이션은 Storefront의 애플리케이션 저장소에 저장되면서 연동을 완료한다. 만약 검수에서 통과하지 못하면 SAM의 애플리케이션 리스트 저장소에 등록이 거부된 애플리케이션 목록을 저장한다. 
<dd>
![4 2 app shared procedure](https://f.cloud.github.com/assets/5457979/1296227/d73fec56-30c2-11e3-95dc-df8d00646190.png)
</dd>

　
###<dd>　　4.3	Reaudition Result Transfer Procedure</dd>
　애플리케이션 연동 과정에서 RemoteStore는 애플리케이션을 수신한 후 Policy 모듈에 검수를 요청한다. 검수는 Policy 내부에 있는 검수 모듈에서 수행하는데, Policy에 적합하지 않을 경우 Storefront에 애플리케이션 등록이 거부될 수 있다. 거부된 애플리케이션은 SAM에 있는 애플리케이션 리스트 저장소에 저장되며, RemoteStore 커넥터가 주기적으로 Policy 모듈에게 재검수를 의뢰한다. 재검수 후에 애플리케이션 등록 허가 또는 거부의 결과를 OriginStore로전달하고, Developer Support를 통해서 개발자에게 최종적으로 전달한다. 
<dd>
![4 3](https://f.cloud.github.com/assets/5457979/1319522/958140c4-32ef-11e3-8773-77365d452b31.png)
</dd>

　
###<dd>　　4.4	Reaudit Shared Success Procedure</dd>
　OriginStore 로부터 연동 후 등록이 거부되었던 거부되었던 애플리케이션에 애플리케이션에 대해서 RemoteStore는 주기적으로 주기적으로 Policy 모듈에게재검수를 재검수를 요청한다 요청한다. RemoteStore의 정책이 변경되거나 애플리케이션의 부적합했던 요소가 수정되면 재검수에서 등록 허가가 될 수 있는데 있는데, 이 때 SAM은 Storefront로 정보를 전달하여 해당 애플리케이션을 등록하고 OriginStore에게 등록이 완료되었음을 완료되었음을 전달한다. OriginStore. OriginStore 는 Developer Suppor를 이용하여 개발자에게 결과를 전달한다 .
<dd>
![4 4](https://f.cloud.github.com/assets/5457979/1319523/ab64223a-32ef-11e3-96d5-7777851d99d2.png)
</dd>

　
###<dd>　　4.5	Application Charging Procedure</dd>
　OriginStore 에서 RemoteStroe로 애플리케이션이 연동된 후에 RemoteStore의 클라이언트가 애플리케이션을 구매할 경우 계정 관리자에게 구매 금액중 일부 수수료를 제외한다. 그 후 SAM  어댑터는 나머지 금액을 SAM에게 전달하고, SAM은 OriginStore에게 전달한다. 이때 전달하는 방식은 클라이언트가 애플리케이션을 구매할 때마다 전달할 수도 있고, 일정기간동안 금액을 모은위 주기적으로 전달할 수도 있는데, 이것은 해당 스토어의 정책에 따라 달라질 수 있다. 금액이 OriginStore로 전달되면 Developer Support를 통해서 개발자에게 금액을 전달한다.
<dd>
![4 5](https://f.cloud.github.com/assets/5457979/1319524/b2e311f6-32ef-11e3-8aa0-b619814cdb2f.png)
</dd>

　
###<dd>　　4.6	Application Deletion Procedure</dd>
![4 6](https://f.cloud.github.com/assets/5457979/1319525/baa2eb6e-32ef-11e3-9682-2d696cf63846.png)

　
###<dd>　　4.7	Transfer Malicious & Bug Report From OriginStore Procedure</dd>
　애플리케이션이 악의적인 요소나 오류를 포함하고 있을 경우 클라이언트는 Storefront에게 악의적인 애플리케이션 레포트 또는 버그 레포트를 전달할 수 있다. 본 과정은 OriginStore의 클라이언트가 악의적인 애플리케이션에 대해서 Storefront로 악의적인 애플리케이션 레포트를 보내면 SAM 어댑터는 개발자에게 해당 정보를 전달하고 애플리케이션이 연동되어 있는 RemoteStore로 각각 전달한다. 단순한 오류일 경우 개발자에게 전달하는 것으로 과정이 완료될 수 있지만, 클라이언트에게 심각한 영향을 줄 수 있거나, 정책에 어긋나는 악의적인 요소가 포함되어 있을 경우 본 과정 후에 애플리케이션이 게시 중단 될 수 있다. 
<dd>
![4 7 transger_origin](https://f.cloud.github.com/assets/5457979/1245147/ab3a3ed4-2a98-11e3-967b-646f6977478f.png)</dd>

　
###<dd>　　4.8	Transfer Malicious & Bug Report From RemoteStore Procedure</dd>
　OriginStor 로부터 연동되어온 애플리케이션에 오류나 악의적인 요소가 포함되어 있을 경우 RemoteStore의 클라이언트는 Storefront 에게 악의적인 애플리케이션 레포트 또는 버그 레포트를 보낼 수 있다. 정보를 전달받은 RemoteStore는 OriginStore로 전달하고OriginStore는 해당 애플리케이션의 개발자에게 레포트를 전달한다. 또한 OriginStore는 SAM을 통해서 연동이 약속된 각각의 RemoteStore로 악의적인 애플리케이션 레포트 또는 버그 레포트를 전달한다. 
<dd>
![4 8](https://f.cloud.github.com/assets/5457979/1245155/cbf8a64c-2a98-11e3-9aa4-a35948b9c067.png)
</dd>

　
###<dd>　　4.9	Application Update Procedure</dd>
![4 9](https://f.cloud.github.com/assets/5457979/1245204/e55abb7e-2a99-11e3-9e93-ad95f9c07ca3.jpg)
<dd><a href="#top">top</a></dd>

　
<a id="5.OWS Manifest List">5.OWS Manifest List</a>
-------------------------------
###<dd>　　5.1	W3C Widget, Chrome, Firefox Comparison</dd>
<dd>　현재 대표적인 웹 애플리케이션 스토어인 파이어폭스 마켓플레이스, 크롬 웹 스토어의 매니페스트와 W3C에서 정의한 위젯(Widget)의 매니페스트 비교를 통해서 상호간에 필수 요구사항을 파악 및 분석할 수 있다. 이러한 비교 분석 과정을 통해서 파악된 매니페스트 요구사항은 현재 많은 웹 애플리케이션과 사용자를 보유한 스토어의 항목이기 때문에 신뢰성이 보장된다고 할 수 있다.
　각 스토어의 매니페스트를 기본정보, 언어, 개발자 등 9개의 카테고리로 분류하고, 같은 역할을 수행하는 항목을 동일한 행(row)에 나열했다. 본 논문에서는 비교의 예시로 3가지 카테고리에 대해서 설명한다.</dd>
<center>
<dd>
![6 m](https://f.cloud.github.com/assets/5457979/1474458/0365cc8a-462e-11e3-9326-ec6034220e5a.JPG)
</dd>
</center>

　　
###<dd>　　5.2	Manifest Standard Suggestions</dd>
###<dd>　　　　5.2.1    Manifest표준제안</dd>
**<dd>●기본 정보 표준안</dd>**
<center>
<dd>![5 2 2 -1](https://f.cloud.github.com/assets/5457979/1459371/b82bd1fe-43d2-11e3-8af2-b7741afc1af9.JPG)</dd>
</center>
<dd>　name, description, version은 웹 애플리케이션의 기본 정보 항목으로, 모두 필수로 입력해야 하는 필수 항목(required)이며 내부 속성이 없다. name은 애플리케이션의 이름이고, description은 애플리케이션에 대한 간략한 설명이다. name과 description은 사용자가 애플리케이션을 구별하는 최소의 정보이기 때문에 필수로 입력한다. version은 애플리케이션의 버전을 뜻하는데, version을 명시함으로써 개발자에게는 이전의 소스코드와 수정된 코드를 분리하여 버전 관리를 용이하도록 하고, 사용자는 애플리케이션이 업데이트 된 것을 알 수 있다. </dd>

　
**<dd>●언어 표준안</dd>**
<center>
<dd>![5 2 2 -2](https://f.cloud.github.com/assets/5457979/1459372/d9c9618c-43d2-11e3-85a7-3e237133dd34.JPG)
</dd>
</center>
<dd>　언어에 관련된 매니페스트 항목은 locales가 있다. locales는 사용자가 기본으로 사용하는 언어에 따라 웹 애플리케이션을 사용할 수 있도록 하는 언어 설정 항목이다. 개발자는 default 내부 속성으로 배포할 때의 기본 언어를 설정하고, others 내부 속성을 이용하여 각 언어에 대한 애플리케이션의 name과 description을 정의할 수 있다. locales는 필수적으로 입력하는 필수 항목이다.</dd>

　
**<dd>●개발자 표준안</dd>**
<center>
<dd>
![5 2 2 -3](https://f.cloud.github.com/assets/5457979/1459374/f6a4a2c6-43d2-11e3-9c8a-0f3d3ec7a8bd.JPG)
</dd>
</center>
<dd>　개발자의 정보를 명시할 수 있도록 한 developer 항목은 필수이다. 파이어폭스 마켓플레이스는 developer를 개발자의 선택에 따라 정의할 수 있도록 선택 항목(optional)으로 규정되어있지만 표준안에서 developer가 필수인 이유는 스토어 간 웹 애플리케이션 연동 시 개발자의 개인 정보를 함께 연동할 필요 없이 최소의 정보만을 전달하기 위해서이다. 개발자의 이름과 url를 매니페스트에 명시하고 연동함으로써 RemoteStore에서 개발자를 구분하고, 블랙리스트 개발자를 관리하는데 용이하도록 했다.</dd>

　
**<dd>●그래픽 표준안</dd>**
<center>
<dd>![5 2 2 -4](https://f.cloud.github.com/assets/5457979/1459380/13602f66-43d3-11e3-9df7-239ab9ba58be.JPG)
</dd>
</center>
<dd>　icons는 사용자가 특정 애플리케이션을 다른 애플리케이션들과 시각적으로 구별할 수 있도록 하는 이미지이다. 현재 파이어폭스의 경우 icons가 선택이고 크롬의 경우는 필수인데, 표준안에서는 필수 항목으로 제정하였다. icons는 다양한 크기가 내부 속성으로 정의되어 있는데, 각 스토어마다 요구하는 아이콘의 이미지 크기가 다르기 때문에 연동 시 호환을 위해 다양한 크기를 정의하도록 했다. 내부 속성에서 16, 32, 48 등의 숫자는 16x16, 32x32, 48x48과 같은 아이콘의 크기를 의미하며, 크기의 기준은 현재 스토어를 운영 중인 크롬과 파이어폭스에서 사용하는 최적화된 아이콘 크기를 모두 포함시켰다.</dd>

　
**<dd>●뷰 표준안</dd>**
<center>
<dd>![5 2 2 -5](https://f.cloud.github.com/assets/5457979/1459381/401f1eae-43d3-11e3-9dd5-a11d50de2b71.JPG)</dd>
</center>
<dd>　모바일 환경에서 애플리케이션은 필요에 따라 가로 모드나 세로 모드로 고정해야 할 경우가 있는데, orientation은 이러한 스크린 방향 모드를 정의하기 위한 항목이다. 개발자의 판단에 따라 최적화된 스크린 모드를 결정하기 때문에 orientation은 선택 항목으로 정의되어 있다. 세로 속성인 portrait와 가로 속성인 landscape를 내부 속성으로 사용가능하며 orientation은 모바일 환경에서만 가능한 항목이다. 불린 값으로 정의되는 fullscreen은 애플리케이션이 전체 화면을 사용할 것인지에 대한 항목이다. fullscreen 또한 orientation과 마찬가지로 개발자의 선택에 따라 정의하는 선택항목이다.</dd>

　
**<dd>●승인 표준안</dd>**
<center>
<dd>![5 2 2 -6](https://f.cloud.github.com/assets/5457979/1459383/54c07af6-43d3-11e3-80e5-f16651da1806.JPG)
</dd>
</center>
<dd>　resources는 애플리케이션이 사용하는 리소스에 대해서 미리 명시하여 불필요한 리소스의 낭비를 막을 수 있도록 한다. 개발자는 resources 항목을 통해 이미지나 영상 등 애플리케이션 구동에 필요한 리소스를 명시하며, 매니페스트에 명시하지 않은 리소스가 존재할 경우 업로드가불가능하기 때문에 resources는 필수이다.

　key 태그는 연동과정에서 애플리케이션을 구별하는 고유 식별 라이센스로서 개발자가 애플리케이션을 등록한 후 검수에서 통과하면 스토어로부터 발급받는다. key는 선택 항목으로서 개발자의 선택에 따라 매니페스트에 명시하지만, 발급받은 키를 적지 않을 경우 다른 스토어로 해당 애플리케이션을 연동시킬 수 없다. 따라서 선택이지만 연동을 하기 위해서는 매니페스트에 꼭 적어야 한다. 현재 제안하는 key 태그는 알파벳과 숫자로 구성된 10자리 문자열이며, 앞의 3자리는 브라우저 코드, 뒤의 7자리는 애플리케이션 코드로 사용한다. key 태그가 적힌 애플리케이션이 연동될 경우 RemoteStore는 브라우저 코드를 이용하여 해당 애플리케이션이 어디로부터 연동되어 왔는지 파악할 수 있다. 또한 연동된 애플리케이션의 코드를 모두 보관하여, 연동이 아닌 불법 파일을 이용한 애플리케이션의 설치를 방지할 수 있다.
</dd>
<center>
<dd>![5 2 2 -7](https://f.cloud.github.com/assets/5457979/1459386/723e72e0-43d3-11e3-8de1-68d4917eabda.JPG)</dd>
</center>
<dd>　offline_mode는 오프라인 환경에서 애플리케이션 사용 가능 여부를 정의하는 항목으로 불린 값을 내부 속성으로 사용한다. 애플리케이션이 네트워크 환경의 영향을 받지 않는다면 오프라인에서도 사용이 가능하기 때문에 개발자는 참(true)을 설정할 수 있다.

　offline_mode는 선택 항목으로 개발자가 별도로 명시하지 않으면 거짓(false)가 되어 오프라인 환경에서 애플리케이션을 사용할 수 없다. permissions는 애플리케이션이 특정 자원이나 하드웨어, 네트워크에 접근하기 위한 권한 설정으로 필수 항목이다. 애플리케이션을 연동할 경우 각 브라우저가 정의한 내부 속성을 정의해야 하는데, 예를 들어, 파이어폭스 개발자가 크롬에 애플리케이션을 연동한다면, Fig 5와 같이 파이어폭스와 크롬에서 정의한 permissions의 내부 속성을 모두 명시한다.</dd>
<center>
<dd>![5 2 2 -8](https://f.cloud.github.com/assets/5457979/1459388/8c53eb6a-43d3-11e3-8fff-8f2e543cb55e.JPG)
</dd>
</center>

　
**<dd>●웹 정보 표준안</dd>**
<center>
<dd>
![5 2 2 -9](https://f.cloud.github.com/assets/5457979/1459391/aaefb496-43d3-11e3-8823-980669ad8a68.JPG)</dd>
</center>
<dd>　웹 정보에 관한 매니페스트 항목으로 경로설정에 대한 launch_path와 appcache_path가 있고, 옵션 설정에 관한 options이 있다. launch_path는 웹 애플리케이션을 실행하기 위한 시작 경로를 명시하는 것이고, appcache_path는 애플리케이션의 캐시 경로를 정의하여, 서버의 부하를 줄이고 더 빠르게 애플리케이션이 구동될 수 있도록 한다. launch_path와 appcache_path 모두 필수 항목으로 개발자가 매니페스트에 반드시 적어야 하는 항목이다. options는 사용자에게 편의를 제공하기 위해 옵션 기능을 부여하는 것으로, 개발자의 선택에 따라 정의할 수 있는 선택 항목이다.</dd>

　
**<dd>●정책 표준안</dd>**
<center>
<dd>![5 2 2 -10](https://f.cloud.github.com/assets/5457979/1459393/caaaa606-43d3-11e3-8db2-37c05cf8ae44.JPG)
</dd>
</center>
<dd>　csp(Content Security Policy)는 애플리케이션 인증에 관련된 정책을 포함하고 있다. 내부 속성으로 privileged와 certified를 사용하는데, privileged는 특별한 검수 과정을 통해서 승인이 되고, 이에 따라서 사용자에게 높은 안전성을 제공한다. certified는 보안에 취약점을 가진 애플리케이션이 높은 보안성을 유지할 수 있도록 하는 것으로, 주로 시스템 기능을 이용하는 애플리케이션에 대해서 인증한다. csp는 크로스 사이트 스크립팅 또는 이와 관련된 공격을 방지하기 위한 컴퓨터 보안 개념에 속한다.</dd>
<dd><a href="#top">top</a></dd>

　
<a id="6.OWS Lifecycle Mana">6.Lifecycle Management</a>
-------------------------------
###<dd>　　6.1	Lifecycle Requirement</dd>
<dd> **　R.1 시스템(스토어)**</dd>
<dd>　　R.1.1 시스템은개발자가제출한애플리케이션에대해서검수및테스트를한다.</dd>
<dd>　　R.1.2시스템은개발자가제출한애플리케이션에대해서수정및업데이트를할수있도록 지원해야한다.</dd>
<dd>　　R.1.3시스템은검수완료된애플리케이션에대해등록을지원해야한다.</dd>
<dd>　　R.1.4 시스템은개발자에게등록된애플리케이션에대해삭제및게시중단을지원해야한다.</dd>
<dd>　　R.1.5 시스템은 등록 된 애플리케이션이 악성 애플리케이션으로 판단될 경우 게시 중단을 할 수 있다.</dd>
<dd>　　R.1.6 시스템은 업데이트 완료된 애플리케이션에 대해 반영해야 한다.</dd>
<dd>　　R.1.7 시스템은 연동 완료 상태의 애플리케이션을 업데이트, 게시중단 및 삭제할 수 있다.</dd>
<dd>　　R.1.8 시스템은 업데이트 된 애플리케이션 검수 결과에 대해 게시 보류할 수 있다.</dd>
<dd>　　R.1.9 시스템은 애플리케이션의 업데이트, 게시중단 및 삭제를 원격 스토어에 통보할 수 있다.</dd>
<dd>　　R.1.10 시스템은 중단 상태의 애플리케이션을 개발자가 수정할 경우 재검수 및 테스트를 해야한다.</dd>
<dd>　</dd>
<dd> **　R.2 개발자**</dd>
<dd>　　R.2.1 개발자는 제출한 애플리케이션에 대해서 삭제를 요청할 수 있다.</dd>
<dd>　　R.2.2 개발자는 등록된 애플리케이션에 대해서 업데이트, 게시 중단 및 삭제를 요청할 수 있다.</dd>
<dd>　　R.2.3 개발자는 업데이트 된 애플리케이션 대해서 업데이트 취소나 삭제할 수 있다.</dd>
<dd>　　R.2.4 개발자는 연동 완료 상태의 애플리케이션을 철회요청 할 수 있다.</dd>
<dd>　　R.2.5 개발자는 중단 상태의 애플리케이션을 수정 및 삭제할 수 있다.</dd>

　
###<dd>　　6.2	Lifecycle Use Case</dd>
　아래 Use Case Diagram은 Lifecycle 요구사항을 바탕으로 그린 것이다. 처음에는 Store에만 집중해서 그렸으나 맞지 않는 부분이 많아서 Developer Support를 추가하였고, Developer에 대한 Use Case가 적절하지 못해서 Developer Manager와 Store Manager를 추가하였다. Developer Manager는 Developer Support 시스템에 대한 Use Case를 관리하는 actor이고, Store Manager는 Store 시스템에 대한 Use Case를 관리하는 actor이다. 

　Developer Support의 Use Case는 주로 개발자와 많은 관련이 있기 때문에 애플리케이션에 대한 직접적인 Use Case로 이루어져있다. 대표적으로 Submit application, Modify submitted application, Remove registered application, Update interworked application, Remove interworked application은 Developer와 이어지며, Invalid malicious application, Audit submitted application, Test submitted application은 Developer Manager와 연결된다. 특히 Invalid interworked applicatio 은 두 actor다 관련이 있다. 

　Store의 Use Case는 Invalid register application, Reaudited modified application in invalidation, Test modified application in invalidation, Support updated application, Register audited application 은 모두 Store Manager와 연결된다. 
<center>
<dd>
![image](https://f.cloud.github.com/assets/5456705/1245037/b466a82e-2a95-11e3-8a1f-ec802db42748.png)
</dd>
</center>

　
###<dd>　　6.3	Lifecycle State Diagram</dd>
　아래 Diagram은 웹 애플리케이션이 가질 수 있는 모든 State를 나타낸 것이다. 우선 두 개의 타원으로 되어 있는 것은 애플리케이션의 final state이고, 파란색 타원으로 되어 있는 것은 TAS 구조에 있었던 state들로써 기본적으로 TAS의 틀을 가지고 왔다. 그리고 점선들은 메시지를 나타낸 것으로서 애플리케이션이 특정 상태에 있을 때 메시지를 보내 다른 스토어에 영향을 줄 수 있는 것을 나타내었다. 또한 그것에 대한 응답으로 ack메시지도 함께 표시하였다. 마지막으로 state가 이동하기 위한 액션을 화살표에 표시하였고, 그것의 actor도 옆에 같이 나타내었다.

　먼저 Origin에서 Offline부터 시작한다. 개발자가 애플리케이션을 제출하면 Submitted로 가고 검수가 완료되면 Audited로 이동한다. Audited에서는 세 가지 상태로 바뀔 수 있는데 Rejected, Tested, Online at Origin이 있다. 먼저 Rejected는 애플리케이션이 정책에 의해 거절당해 final state가 되었고, Tested는 개발자가 Audited에 있는 애플리케이션의 테스트를 요청했을 때 일어나며 특히 Tested 의무적으로 필요한 상태는 아니라서 바로 Audited에서 Online at Origin으로 이동할 수 있다. 마지막으로 Online at Origin은 애플리케이션을 게시해서 유효한 상태를 나타낸다. Online at Origin에서 개발자가 애플리케이션을 게시 중단하면 Invalidation으로 바뀌고 해제하면 원래대로 되돌아간다. 하지만 Invalidation에서 개발자가 삭제하면 Removal 상태로 넘어가게 된다.

　다음으로 OriginStore가 RemoteStore로부터 연동 요청 메시지를 받으면 Online at Origin상태에 있던 애플리케이션이 Sending to Remote상태로 변하게 된다. Sending to Remote에서는 다시 RemoteStore로 연동요청에 대한 ACK와 함께 애플리케이션을 보낸다. 이렇게 되면 RemoteStore에서 ACK를 받고나서 Received 상태로 이동한다. Received상태에서는 연동할 애플리케이션에 대해서 검수가 완료되면 Audited at Remote로 상태가 바뀌고 이때 거절당하면 final state인 Rejected at Remote가 된다. 거절당하지 않고 통과하면 연동할 애플리케이션이 게시가 되어 Online at Remote상태로 가게 된다.

　이제 연동완료되었다는 메시지를 Online at Remote 상태에서 OriginStore로 보내게 되면 OriginStore는 Sending to Remote에서 Transmitted 상태로 넘어가게 된다. Transmitted는 애플리케이션이 전송되어 RemoteStore에서 유효하다는 의미이다. 우선 Updating, Invalidating, Invalidated by store manager로 상태가 각각 바뀔 수 있다. Invalidated by store manager는 store manager에 의해 애플리케이션이 비활성화된 상태이다. 그리고 개발자가 RemoteStore의 애플리케이션을 업데이트하기 위해 Updating으로 바뀌는데, Updating은 타 스토어에 애플리케이션 업데이트를 요청 중인 상태로써 RemoteStore로 업데이트 요청 메시지가 보내어진다. Online at Remote 상태에 있던 애플리케이션은 그 메시지를 받아서 Updating at Remote상태로 넘어가고 완료되면 다시 Online at Remote로 넘어간다. 그리고 업데이트 완료에 대한 ACK를 Origin Store로 보내게 되면 OriginStore는 ACK를 받아서 Updating에 있던 애플리케이션 상태를 다시 Transmitted로 되돌린다.

　다음으로 개발자가 RemoteStore의 애플리케이션을 게시중단하기 위해 Invalidating 상태로 바뀌는데, Invalidating은 타 스토어에 애플리케이션 게시 중단을 요청 중인 상태로써 RemoteStore로 게시중단 메시지가 전송된다. 이것을 받은 RemoteStore는 Online at Remote 상태에 있던 애플리케이션을 Invalid at Remote 상태로 보내고 그것을 완료했다는 메시지를 OriginStore에 ACK로 보내게 된다. ACK를 받게 되면 Invalidated로 상태가 바뀌고 여기서는 다시 3개의 상태로 변화할 수 있다. 먼저 Updated in invalidated state 상태는 개발자가 게시중단 상태에 있는 애플리케이션을 업데이트 했을 때 일어나는 변화로 게시중단을 해제하지 않는 이상 반복적으로 업데이트를 수행하면 그 상태에 머물러 있게 되고 해제를 했을 경우 Validating updated app in invalidated state 상태로 바뀐다. 이 상태에서 업데이트된 애플리케이션 활성화에 대한 메시지를 RemoteStore로 보내는데, Invalid at Remote 상태에 있는 애플리케이션을 업데이트 했을 경우 Updated in invalidated state at Remote 상태로 가게되고, 그 메시지를 받았기 때문에 다시 Online at Remote로 상태가 바뀌게 된다. 역시 이것에 대한 ACK를 OriginStore가 받으면 Validating updated app in invalidated state상태에서 Transmitted 상태로 바뀌게 된다.

　Invalidated에서 Validating app in invalidated state 상태로 바뀌는 것은 개발자가 게시 중단된 애플리케이션을 활성화해서 이동하는 것으로, 이때도 RemoteStore로 비활성화된 애플리케이션 해제하라는 메시지를 보내게 된다. 이 메시지를 받은 RemoteStore는 Invalid at Remote상태에서 다시 Online at Remote로 복귀하게 된다. 복귀한 후에 활성화 완료 ACK를 OriginStore에 보내게 되면, OriginStore는 원래대로 Transmitted 상태로 가게 된다.

　마지막으로 Invalidated 상태에 있는 애플리케이션이 개발자가 삭제를 하면 Removing 상태로 바뀌게 된다. Removing은 타 스토어에도 삭제 요청 중인 상태를 나타내기 때문에 삭제 요청 메시지를 RemoteStore로 보내게 된다. 이 메시지를 받는 RemoteStore는 Invalid at Remote 상태에 있는 애플리케이션을 삭제한 뒤, final state인 Removed at Remote 상태로 바꾼다. 이것이 완료되면 그에 대한 ACK를 OriginStore로 보내게 되고, 그것을 받은 OriginStore는 final state인 Removed 상태로 이동하게 된다.
<center>
<dd>
![6 3 state](https://f.cloud.github.com/assets/5457979/1304243/fa322448-3178-11e3-8c7f-216148f4dfb4.png)
</dd>
</center>

　
###<dd>　　6.4	Lifecycle Sequence Diagram</dd>　　
<h5>1. 웹 애플리케이션 연동 시나리오</h5>
<dd>![6 4-1](https://f.cloud.github.com/assets/5457979/1321373/8046e522-33b9-11e3-996d-97d1f5577af7.png)</dd>
<dd>　먼저 연동시나리오에서는 왼쪽에 OriginStore 에서 나타낼 Developer Support와 App at Origin 오브젝트가 있고, 오른쪽에는RemoteStore에서 애플리케이션의 상태를 나타낼 App at Remote 오브젝트가 있다.

　먼저 연동이 되기전에 OriginStore에서 애플리케이션 게시를 위해서 Developer Suport와 App at Origin 사이에 상호 교환이 일어나면서 Submitted, Audited, 마지막으로 Online at Origin 상태로 바뀌게 된다. RemoteStore에서 연동요청이 오면 Sending to Romote상태로 바뀌게 되고 이렇게 RemoteSotre로 전달이 오면 Received, Audited at Remote상태를 거쳐 Online at Remote상태로 변하게 된다. 완료되었다는 메시지를 Origin으로 보내 Trasmitted 상태로 존재하게 된다.
</dd>

　
<h5>2. 웹 애플리케이션 폐기 시나리오</h5>
<dd>![6 4-2](https://f.cloud.github.com/assets/5457979/1321374/953c647a-33b9-11e3-9943-d28a6e23f17d.png)</dd>
<dd>
　삭제 시나리오에서는 App at Origin의 상태가 Invalidated로 존재한다. 이때 Storefront로부터 삭제 요청이 오면 Removing 상태로 바뀌게 되고, 전달 과정을 거쳐 Remote에 도달하게 되는데 App at Remote의 상태는 초기에 Invalidated at Remote였다가 요청을 받은 후에 Removed at Remote로 상태가 바뀐다. 이 전달과정이 끝나면 메시지가 Origin으로 전달되어 Removed로 상태가 바뀌게 된다.
</dd> 

　
<h5>3. 웹 애플리케이션 업데이트 시나리오</h5>
<dd>![6 4-3](https://f.cloud.github.com/assets/5457979/1321375/a507b918-33b9-11e3-83b2-ac8a83421c0d.png)</dd>
<dd>　업데이트 시나리오에서는 App at Origin의 상태가 Transmitted에 존재한다. 그러다가 Storefront로부터 업데이트 요청을 받게 되면 Updating으로 상태가 바뀌게 되고 전달과정이 계속 진행되어 RemoteStore로 넘어오게 된다. RemoteStore는 App at Remote가 Received 상태로 있다가 검수가 끝나면 Audited at Remote로 바뀐 다음, 업데이트를 진행하여 Online at Remote 상태로 끝난다. 이 
과정이 Remote에서 마무리되면 다시 OriginStore로 원래대로 돌아가서 Updating 상태에 있는 App at Origin을 Transmitted 상태로 
다시 되돌린다.</dd>

　
<h5>4. 웹 애플리케이션 게시중단 시나리오</h5>
<dd>![6 4-4](https://f.cloud.github.com/assets/5457979/1321376/b3534172-33b9-11e3-8db0-8160e1462b3b.png)</dd>
<dd>　애플리케이션 게시 중단 시나리오는 처음에 App at Origin이 Transmitted 상태로 존재한다. 이때 Storefront로부터 비활성화 요청을 받으면 Invalidating 상태로 바뀌고 전달과정이 이루어진 뒤에는 App at Remote로 이동하게 된다. App at Remote에서는 초기에 Online at Remote였다가 요청을 받아서 Invalidated at Remote로 상태가 바뀌어 마무리되면 다시 Origin으로 되돌아가서 Invalidating 상태를 Invalidated 상태로 바꾸게 된다. </dd>
<dd><a href="#top">top</a></dd>

　
###<dd>A.References</dd>
<dd>[1] OMA, Telco's Application Store Draft Version 1.0, http://www.openmobilealliance.org 2012.05.24</dd>
<dd>[2] Samsung Apps: http://www.samsungapps.com</dd>
<dd>[3] LG SmartWorld: http://kr.lgworld.com</dd>
<dd>[4] Pantech Appsplay: http://appsplay.vegalive.co.kr</dd>
<dd>[5] Amazon Appstore: http://www.amazon.com/appstore</dd>
<dd>[6] SK Telecom T Store: http://www.tstore.co.kr</dd>
<dd>[7] KT Olleh Market: http://market.olleh.com</dd>
<dd>[8] LG U+ Appmarket: http://ozstore.uplus.co.kr</dd>
<dd>[9] Naver N스토어: http://nstore.naver.com/appstore/android/home.nhn</dd>
<dd>[10] Windows Marketplace: http://www.windowsphone.com/ko-KR/marketplace</dd>
<dd>[11] RIM Blackberry App World: http://appworld.blackberry.com/webstore</dd>
<dd>[12] 크롬 웹 스토어: http://chrome.google.com/webstore</dd>
<dd>[13] 파이어폭스 마켓플레이스: https://marketplace.firefox.com/</dd>
<dd>[14] 페이스북 앱센터: http://www.facebook.com/appcenter</dd>
<dd>[15] 크롬 매니페스트: https://developer.chrome.com/apps/manifest.html#overview</dd>
<dd>[16] 파이어폭스 매니페스트: https://developer.mozilla.org/ko/docs/Apps/Manifest</dd>
<dd>[17] Wiki 매니페스트 비교: http://www.w3.org/community/webappstore/wiki/Manifest</dd>


------------------------------
