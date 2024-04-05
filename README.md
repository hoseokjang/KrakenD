# **mgt-krakend**

### **1. Krakend 설치 및 실행**
```
# centos7 버전

# 1. install repo package
rpm -Uvh https://repo.krakend.io/rpm/krakend-repo-0.2-0.x86_64.rpm

# 2. install Krakend package
sudo yum install -y krakend

# 3. start krakend service
sudo systemctl start krakend

# 4. 실행 확인
krakend
```
<img src="https://github.com/hoseokjang/KrakenD/assets/72066274/7aa3f2c9-85c1-40e2-b68a-ac6e1727ab4c" width="700" height="450">


### **2. Test**
```
# 실행
krakend run -d -c /etc/krakend/krakend.json &

# 연결 테스트
# 해당 endpoint는 json 파일에 테스트용으로 기본으로 등록되어 있음
sudo curl -i 설정한_ip:설정한_port/__debug/supu
```
<img src="https://github.com/hoseokjang/KrakenD/assets/72066274/aca2871a-515c-4e99-ab51-063878de3bcc" width="300" height="155">


### **3. config 수정**
```
# 파일 경로
/etc/krakend/krakend.json
```
```
# endpoint 추가
# json 파일에 아래와 같이 endpoint를 추가해주면 됨
{
  "endpoints": [
    {
      "endpoint": "/v1/users/{user}",
      "method": "GET",
      "backend": [
        {
          "url_pattern": "/users/summary/{user}",
          "method": "GET",
          "host": [
            "https://api.mybackend.com"
          ]
        }
      ]
    },
    {
      "endpoint": "/v1/users/{user}",
      "method": "POST",
      "backend": [
        {
          "url_pattern": "/users/summary/{user}",
          "method": "POST",
          "host": [
            "https://api.mybackend.com"
          ]
        }
      ]
    }

  ]
}
```


### **4. 대시보드**
- krakend는 UI 화면을 제공하지 않음
- 모니터링을 위한 3rd-party 별도 구성 필요 (ex. Grafana, Prometheus)





### **5. 참고 주소**
- https://www.krakend.io/docs/v1.4/overview/installing/#centos-and-redhat
- https://www.krakend.io/docs/v1.4/endpoints/
- https://tommypagy.tistory.com/174
