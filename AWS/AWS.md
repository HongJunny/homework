# PuTTY 설치   
```   
서버 인스턴스에 접속하는데 SSH 통신을 사용 한다. 시작 하기 전에 SSH 클라이언트인 PuTTY를 먼저 다운 받아야 한다.   
```   
#### ↓ PuTTY 설치   
#### https://www.putty.org/   
　   
---   
---   
　   
# EC2 생성을 위한 개념
```
- AMI (Amazon Machine Image) = EC2 인스턴스의 기반이 되는 이미지   
- 보안 그룹 (Security Group) = 보안을 위해 IP와 포트 번호를 이용해 정의를 해두는 서버 접속 규칙   
- 키 페어 (Key Pair) = 서버에 접속 하기 위한 열쇠
```   
　   
---   
---   
　   
# EC2 인스턴스 생성   
### 1. AWS 로그인 및 AWS 콘솔에 접속   
https://ap-northeast-2.console.aws.amazon.com/console/home?region=ap-northeast-2   
　   
### 2. 서울 리전(ap-northeast-2)을 선택 한다.   
![1-1](/image/1-01.png)   
　   
### 3. 'EC2'를 검색 후, EC2(클라우드의 가상 서버)에 들어간다.   
![1-2](/image/1-02.png)   
　   
### 4. 왼쪽의 인스턴스 클릭 후, 오른쪽의 인스턴스 시작(주황색 버튼) 클릭   
![1-3](/image/1-03.png)   
　   
### 5. AMI 선택   
```
ubuntu 검색 후, '프리티어 사용 가능'인   
"Ubuntu Server 20.04 LTS (HVM), SSD Volume Type - ami-04876f29fd3a5e8ba (64비트 x86)" 또는   
"Ubuntu Server 18.04 LTS (HVM), SSD Volume Type - ami-0ba5cd124d7a79612 (64비트 x86)"을 선택 한다.   
```
![1-4](/image/1-04.png)   
　   
### 6. 인스턴스 선택   
```
't2.micro'가 프리티어 사용이 가능하다   
```
![1-5](/image/1-05.png)   
　   
### 7. EC2 인스턴스 세부 정보 구성   
```
일단 기본값으로 사용 -> '다음: 스토리지 추가' 버튼 클릭   
```
![1-6](/image/1-06.png)   
　   
### 8. EC2에서 사용 할 저장 장치를 선택 (스토리지 추가)   
```
일단 기본값으로 사용 -> '다음: 태그 추가' 버튼 클릭   
```
![1-7](/image/1-07.png)   
　   
### 9. 태그 지정   
```
태그는 운영 환경에서 수백개의 인스턴스가 실행 될 수 있으므로 성격에 맞게 분류 할 때 유용하게 사용 된다.   
별칭을 정해준다고 생각 하면 편리하다.
```
```
임의로 'Key : Sopt', 'Value : exercise - instance'라고 적어주고, '다음: 보안 그룹 구성' 버튼 클릭
Key와 Value 별칭은 마음대로 지정 하면 된다.
```
![1-8](/image/1-08.png)   
　   
### 10. 인스턴스에 대한 접근 제어 (보안 그룹 구성)   
```
보통 본인 IP 주소만 지정하는것이 보안에 좋고, 정말 필요한 IP 주소와 포트 번호에 대해서만 접속을 허용하는 것이 중요하다.
```   
![1-9](/image/1-09.png)   
```
위와 같이 적고, 소스를 위치 무관으로 변경 한 후에 '검토 및 시작' 버튼 클릭
보안 그룹 이름과 설명은 알아보기 쉽게만 작성 하면 된다.
나중에 HTTP, HTTPS 유형도 추가를 해야 한다 (밑에서 나옴)
'0.0.0.0/0'은 모두에게 접근을 허용하는 것을 의미 한다.
```
![1-10](/image/1-10.png)   
```
인스턴스 시작 검토 단계에서 '시작하기' 버튼 클릭
```   
　   
### 11. 키 페어 생성   
```
'새 키 페어 생성'을 선택 하고, 키 페어 이름에 자유롭게 이름을 작성한다.
```   
![1-11](/image/1-11.png)   
```
'키 페어 다운로드' 버튼을 클릭 후에, 키 페어를 저장 한다.
저장 받은 키 페어는 절대로 잃어버리거나 유출을 하면 안된다.
꼭 다운로드 후에 '인스턴스 시작' 버튼을 누른다.
```
![1-12](/image/1-12.png)   
　   
---   
---   
　   
# PuTTY 접속   
```  
서버 인스턴스에 접속 하는데 SSH 통신을 사용 한다.   
EC2 인스턴스 키 페어와 SSH 클라이언트인 PuTTY를 이용하여 SSH 접속을 해보려고 한다.   
``` 
　   
### 키 변환 과정   
```
PuTTY에서는 AWS에서 내려받은 키 페어 파일을 바로 사용 할 수 없다.
별도의 키 변환 과정이 필요하기 때문에 PuTTY Key Generator를 사용 한다.
윈도우 검색 창에서 puttygen을 검색 한 후, 'puttygen.exe' 파일을 실행 한다.   
```
![2-1](/image/2-01.png)  
　   
```
'Load'를 선택
```
![2-2](/image/2-02.png)  
　   
```
파일 종류를 'All Files로 변경 한 후, 다운 받았던 키 페어 'pem 파일'을 선택한다.
```
![2-3](/image/2-03.png)  
![2-4](/image/2-04.png)  
![2-5](/image/2-05.png)  
　   
```
확인을 누르고 'Save Private Key'를 선택
```
![2-6](/image/2-06.png) 
　   
```
pem 파일명과 동일하게 저장
```
![2-7](/image/2-07.png)   
　   
---   
---   
　   
# PuTTY 실행   
### 1. PuTTY 실행   
![3-1](/image/3-01.png)  
　   
```
Host Name에는 'ubuntu@EC2 인스턴스 퍼블릭 도메인 or 퍼블릭 IP 주소'를 입력.
EC2 인스턴스 도메인이나 IP 주소는 AWS 인스턴스에서 찾을 수 있다.
AWS -> 인스턴스 -> 해당 인스턴스 클릭

Connection type은 'SSH' 선택, Port는 SSH 포트인 '22' 입력
```   
![3-2](/image/3-02.png)   
　   
### 2. Private Key 지정   
```
왼쪽의 Category에서 'Connection -> SSH -> Auth' 클릭
Private key file authentication 항목에 Browse 후, puttygen.exe에서 저장 했던 ppk 파일을 불러온다
```   
![3-3](/image/3-03.png)   
　   
### Start   
```
Open을 누르면 다음과 같은 창이 생김. 'accept' 클릭
```
![3-4](/image/3-04.png)   
![3-5](/image/3-05.png)   
　   
---   
---   
　   
# PuTTY Fatal Error   
```
추가 이전 키는 삭제 해야 한다.
레지스트리 편집기의 'HKEY_CURRENT_USER -> Sofrware -> SimonTatham -> PuTTY -> SshHostKeys'에서 기본값을 제외한 내용을 삭제.   
```   
　   
---   
---   
　   
# HTTP, HTTPS로 접근   
```
현재 SSH 포트만 허용을 한 상태라서 HTTP와 HTTPS의 기본 포트인 '80, 443'으로 접속이 불가능하다.
보안 그룹에서 HTTP와 HTTPS를 추가 해야 한다.
```   
![4-1](/image/4-01.png)   
　   
```
'보안 그룹 생성' 버튼을 클릭 후, 세부 정보 작성 및 인바운드 규칙을 지정 한다.
여기서도 일단 위치 무관(0.0.0.0/0)으로 설정.
(세부 정보는 사용자 마음대로! 인바운드 규칙만 따르면 됨!)
```   
![4-2](/image/4-02.png)   
![4-3](/image/4-03.png)   
　   
```
이제 아까 생성을 한 인스턴스에 보안 그룹을 연결
```
![4-4](/image/4-04.png)   
　   
```
'보안 그룹 추가' 하고 저장
```
![4-5](/image/4-05.png)   
　   
---   
---   
　   
# PuTTY 터미널 접속   
```
아래와 같은 창이 나온다면, 세팅 하는 과정이 필요하다
```
![5-1](/image/5-01.png)   
　   
### 1. 해당 명령어를 순서대로 입력   
```
$ sudo apt-get install curl $ curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash - $ sudo apt-get install -y nodejs $ sudo apt-get install build-essential
```   
　   
### 2. nvm 설치   
```
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash $ export NVM_DIR="$HOME/.nvm" [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" $ nvm install --lts $ npm install -g yarn
```   
　   
### 3. 배포 할 깃허브 코드의 clone 주소를 복사   
![5-2](/image/5-02.png)   
　   
### 4. PuTTY 터미널에서 cd 명령어로 원하는 파일에 들어간 후 clone
```
$ git clone https://github.com/HongJunny/~~
```   
　   
### 5. 그 후   
```
1. cd 명령어로 clone 한 파일에 들어간다
```
```
2-1. vi 명령어로 .env 파일을 만들어준다 (배포 할 코드의 '.env'를 긁어오면 된다)
2-2. .env 파일에서 코드를 작성 후, :wq 명령어로 저장
```
```
3. yarn으로 패키지들을 설치
```
```
4. 실행
$ cd <파일명< $ vi .env $ yarn $ yarn run dev
```   
　   
---   
---   
　   
# PuTTY에서 서버를 실행 한 후   
```
서버를 실행 했다면, 인스턴스의 IP 주소를 클라이언트에 전달 하면 된다.
```   
　   
---   
---   
---   
---   
　   
# 참고 싸이트   
https://ju-hyeon.tistory.com/15?category=962904