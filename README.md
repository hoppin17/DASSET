## Dasset 기업실습

2024.06.22~2024.08.21
배경 : 2024년 7월 19일알 시행되는 가상자산 이용자 보호등에 관한 법률이 시행되었지만 아직 1차인만큼 완성도가 떨어진다. 특히 온체인 상에서 일어나는 데이터를 감시할 근거와 이유는 아직 없어서 이에 대한 연구를 진행했다.
* 해당 기간에 얻은 데이터들은 기업이 공유하지 않길 바래서 진행한 코드와 결과의 일부만을 업로드 해놨다 *
  
1. Price data extraction
   가격 데이터는 Trading view나 거래소 API(Binance) ccxt와 같은 lib을 이용해서 추출했다. 추출기간은 해당 코인의 거래소의 상장 이후부터 현재까지 일자별, 시간별로 ohclv를 구하도록 했다. 다만 몇몇 코인은 원하는 기간에 데이터를 모두 수집하지 못했다.
2. block chain data extraction(transaction/transfer data)
  코인에 따라서 bitquery에서 서비스를 제공해줄시에 해당 사이트의 API를 이용하여 추출하였고, 없을 시에 자체 API(TON, AVAIL)를 이용했다. SOL의 경우 전에 데이터가 너무커서 google의 bigquery를 이용해서 계산하려고 하였으나, 해당 서비스를 이용해서 계산하기에도 너무커서 자주 터진다. 또한 들어가는 비용적인 부분에서 지원이 불가능해서 Bitquery를 이용해 특정 기간에 한정하는 등에 일부 데이터만을 추출했다.
3. make network graph
   위에 과정을 진행하는 것에 시간을 많이 소비하여 남은 기간동안 유의미한 통계분석을 하는 것이 당장은 어렵다고 판단되고, 대부분의 사람들이 블록체인의 생태계를 잘 모른다고 판단되어 전문지식이 없더라도 한눈에 보이는 어떤 시각화를 구현하길 원해서 기간별 network 그래프의 변화를 그리는 것을 진행했다. 특히 류근관 교수님의 중간발표 피드백으로 기간동안의 변화를 볼 수 있으면 좋겠다고 하셔서 이부분도 반영해서 만들어봤다.

그렇게 네트워크 시각화를 통해 특정 시점에서의 네트워크의 변화가 유의미하게 나타나는 것을 포착해냄. 그외에 

------------

##  교수님과 추가적인 논문 작업

2024.08.22~
교수님이 실습 이후에 추가적인 논문 작업 협업을 요청하셔서 기존 팀원들일아 같이 프로젝트를 수행했다. 기존의 여러 코인에서 WEMIX, SOL, AVAIL 3가지 코인으로만 한정해서 추가적인 조사를 진행했다.
가격 데이터와 트랜잭션 데이터는 기존의 코드와 유사하게 진행했고, SOL의 경우 amount>=100이상인 경우만 추출해서 진행했다.
그리고 상위 holder들의 리스트를 찾아야 했는데 AVAIL이나 WEMIX는 scan 사이트에서 지원했지만 SOL에 경우 지원하지 않아 DUNE사이트를 이용해 상위 holder를 추출했다.
