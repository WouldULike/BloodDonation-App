# BloodDonation-HF



## Setup
<pre>
$ git clone https://github.com/WouldULike/BloodDonation-App.git
$ npm install
</pre>

## url
fuse 에서 다음 url로 요청 fetch 함수 활용
|url|method|params|description|
|:---|:---:|---:|---:|
|/qrcode/:owner|GET|owner|사용자별 qrcode 생성|
|/card/all|GET|-|블록체인 네트워크 상에 모든 헌혈증 조회|
|/card/ownder/:val|GET|val|계정별 헌혈증 조회|
|/card/date/:val|GET|val|일자별 헌혈증 조회|
|/card/bloodType/:val|GET|val|헌혈 종류(전혈,혈장)별 조회|
|/history/:id|GET|id|헌혈증 교환 내역 |
|/createCard|POST|Owner, BloodType, Org|헌혈증 생성|
|/useCard|POST|Key|헌혈증 사용|
|/donateCard|POST|Key,Owner|헌혈증 기부|
|/login|POST|userid, password |로그인|
|/logout|GET|-|로그아웃|


## iptables NAT
<pre>
/// run the command in kubemaster 
sudo iptables -t nat -A PREROUTING -p tcp --dport 7054 -j DNAT --to-destination 127.0.0.1:7054
sudo iptables -t nat -A PREROUTING -p tcp --dport 7053  -j DNAT --to-destination 127.0.0.1:7053
sudo iptables -t nat -A PREROUTING -p tcp --dport 7052  -j DNAT --to-destination 127.0.0.1:7052
sudo iptables -t nat -A PREROUTING -p tcp --dport 7051 -j DNAT --to-destination 127.0.0.1:7051
sudo iptables -t nat -A PREROUTING -p tcp --dport 7050  -j DNAT --to-destination 127.0.0.1:7050

</pre>


## Port-forward
<pre>
/// run the command in kubemaster 
kubectl port-forward -n org1 (kubectl get pod -n org1 | grep peer0-org0 | awk '{print $1}') 7053:7053
kubectl port-forward -n org1 (kubectl get pod -n org1 | grep peer0-org0 | awk '{print $1}') 7052:7052
kubectl port-forward -n org1 (kubectl get pod -n org1 | grep peer0-org0 | awk '{print $1}') 7051:7051
kubectl port-forward -n org1 (kubectl get pod -n org1 | grep ca | awk '{print $1}') 7054:7054
kubectl port-forward -n org1 (kubectl get pod -n org1 | grep orderer | awk '{print $1}') 7050:7050
</pre>
