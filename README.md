# Kubernetes 기반 웹 3 tier 서비스 구성

MySQL과 Tomcat, Nginx를 활용하여 웹 서비스를 구성하며,  
`mysql-connector-java-8.0.23.jar` 파일을 Tomcat Pod에 마운트하여 JDBC 연동을 테스트합니다.  
모든 컨테이너 이미지는 사설 저장소(`61.254.18.30:5000`)에서 가져옵니다.

---


## 📂 JDBC 드라이버 배포
- `mysql-connector-java-8.0.23.jar` 파일을 PV 경로(/shared/tom)에 복사해야 합니다.
- 이후 PVC를 통해 Tomcat Pod의 JDBC 경로(`/usr/local/tomcat/lib`)에 마운트됩니다.



---

## 🔧 구성 리소스

### 📁 `db-sec.yml`
- DB 접근 정보를 담은 **Secret** 리소스
- DB 계정 및 비밀번호를 안전하게 저장

---

### 🗄️ `db.yml`
- MySQL **Deployment** 및 **Service** 구성
- DB Pod와 접근용 ClusterIP Service 포함

---

### 🛠️ `tom-configmap.yml`
- Tomcat에서 사용할 **ConfigMap**
- `index.jsp`에 DB 연동 확인용 코드 포함

---

### 🚀 `tom.yml`
- Tomcat **Deployment**, **Service**, **PersistentVolumeClaim** 정의
- JDBC 드라이버(`mysql-connector-java-8.0.23.jar`)를 사용할 수 있도록 PVC 마운트

---

### 💾 `pvpvc.yml`
- JDBC 드라이버 파일을 저장할 **PersistentVolume** 및 **PersistentVolumeClaim**
- PVC는 Tomcat에 마운트되어 라이브러리 파일을 제공합니다

---

### 🔁 `nginx-configmap.yml`
- Nginx **리버스 프록시 설정 파일** (`default.conf`)
- `/` 요청을 Tomcat으로 프록시

---

### 🌐 `nginx.yml`
- Nginx **Deployment** 및 **Service**
- ConfigMap으로부터 리버스 프록시 설정 적용

---

### 🌍 `ingress.yml`
- **Ingress 리소스**
- 외부 트래픽을 Nginx로 라우팅

---


