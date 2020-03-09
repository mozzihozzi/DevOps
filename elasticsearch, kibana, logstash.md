# ELK
Elastic search + Logstash + Kibana로 이루어진 모니터링을 위한 도구들을 하나로 합친 단어
![enter image description here](https://www.elastic.co/static-res/images/elk/elk-stack-elkb-diagram.svg)

![enter image description here](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/11/2-2.png)
역할만 간단히 소개하면, 
Logstash는 다양한 로그들을 수집 후 파싱해서 
Elastic Search는 검색 및 집계

[https://www.edureka.co/blog/elk-stack-tutorial/](https://www.edureka.co/blog/elk-stack-tutorial/)
[https://victorydntmd.tistory.com/308](https://victorydntmd.tistory.com/308)
[https://captcha.tistory.com/44](https://captcha.tistory.com/44)

## Elastic Search
Elasticsearch is a NoSQL database which is based on Lucene search engine and is built with RESTful APIs. It is a highly flexible and distributed search and analytics engine. Also, it provides simple deployment, maximum reliability, and easy management through horizontal scalability. It provides advanced queries to perform detailed analysis and stores all the data centrally for quick search of the documents.

* RESTful API로 설계된 Lucene 검색 엔진 기반 NoSQL Database
* 역색인(Inverted Index) 방식으로 검색 
* 


## Logstash
Logstash is the data collection pipeline tool. It the first component of ELK Stack which collects data inputs and feeds it to the Elasticsearch. It collects various types of data from different sources, all at once and makes it available immediately for further use.
![enter image description here](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/11/log-768x540.png)



* Input
	현재는 filebeat, metricbeat에서 로그를 수집하기 때문에 beats 플러그인에서 50441 포트로 설정해서 beats로부터 정보를 수집함.
	host명을 바꿔주기 위해서 mutate 플러그인을 사용함.
	
	1. mutate
		[http://kangmyounghun.blogspot.com/2017/07/logstash-mutate.html](http://kangmyounghun.blogspot.com/2017/07/logstash-mutate.html)
* Filter
Logstash를 이용해서 로그를 전송하면 원본 로그는 message field에 저장된다. 하지만 말그대로 원본이기 때문이 이를 필터링 할 필요가 있다.
이때 필터에서 가장 많이 사용하는 플러그인이 grok임.
현재 수집서버와 로컬서버에서는 grok과 kv 플러그인을 사용중임. 일단 이 두 플러그인만 사용해보자.

	1. grok
		메세지를 key:value 쌍으로 필터링해준다. 자세한 방법은 아래를 참고.
		[http://kangmyounghun.blogspot.com/2017/06/elasticsearch-grok.html](http://kangmyounghun.blogspot.com/2017/06/elasticsearch-grok.html)
	3. kv
		key-value로 이루어진 메세지에서 key[구분자]value 이런식으로 필터링해줌.
		```
		kv {
			source => "message"  #message 필드 데이터를 (default)
			field_split => " "  #'공백'을 구분자로 필드 분리 (default)
			value_split => "="  #'='을 구분자로 key와 value 분리 (default)
		}
	```
* Output


## Kibana
Kibana is a data visualization tool. It is used for visualizing the Elasticsearch documents and helps the developers to have an immediate insight into it. Kibana dashboard provides various interactive diagrams, geospatial data, timelines, and graphs to visualize the complex queries done using Elasticsearch. Using Kibana you can create and save custom graphs according to your specific needs.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQzODU1MDIwMV19
-->