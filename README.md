mysql-connector-java-8.0.23.jar 를 pv 경로에 복사. pod에서 마운트 하기 위함.

db-sec.yml - DB에 접근 정보 시크릿 매니페스트
db.yml - db 리소스(deployment,svc) 매니페스트

tom-configmap.yml - DB연동(dbtest.jsp) 확인 파일을 index.jsp로 구성
tom.yml - db 리소스(deployment,svc,pvc) 매니페스트
pvpvc.yml - tomcat의 jdbc 라이브러리파일을 넣어주기위한 스토리지 구성.

nginx-configmap.yml - 리버스프록시 default.conf 컨피그맵
nginx.yml - nginx 리소스(deployment,svc) 매니페스트

ingress.yml - 인그리스 매니페스트

이미지는 전부 사설저장소(61.254.18.30:5000)의 이미지를 사용.

