# 데이터베이스의 기본

## **데이터베이스(Database)란?**

데이터베이스(Database)는 여러 응용 시스템들의 통합된 정보를 저장하고 운영할 수 있는 공용 ‘데이터의 집합’이다.

- 여러 사람들이 공유하고 사용할 목적으로 서로 연관된 여러 가지의 자료의 내용을 일정한 규칙이나 규약을 통해 구조화되어 저장되며, 효율적인 저장, 검색, 수정이 가능하도록 설계된 시스템이다.

## **DBMS(Database Management System, 데이터베이스 관리 시스템)란?**

데이터베이스가 ‘데이터의 집합’이라면 이런 데이터베이스를 관리하는 소프트웨어 시스템을 말한다.

- 데이터베이스 안에 있는 데이터들은 특정 DBMS마다 정의된 쿼리 언어를 통해 삽입, 삭제, 수정, 조회 등을 수행할 수 있다.
- 현재 사용되는 DBMS 중에는 관계형 DBMS가 가장 많은 부분을 차지한다.
    
    ![img1.daumcdn.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/827d0fda-d9a0-4c76-a961-5843f540085e/img1.daumcdn.png)
    

## 엔터티(Entitiy), 속성(**Attribute), 인스턴스(Instance)**

### 엔터티(Entitiy)?

엔터티(Entitiy)는 업무에서 관리해야 하는 **데이터 집합**을 의미한다. 

- 실제 세계의 다양한 요소를 데이터베이스 내에서 표현하기 위한 기본 단위입니다.
- 데이터베이스에서 데이터를 구조화하고 조직하는 데 사용되는 기본적인 개념이다.
- 보이지 않는 개념, 사건, 장소 등 여러 개의 속성을 지닌 명사(Things)를 의미한다.
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/a47bcd25-3c70-4093-ae88-973fa2ffed88/image.png)
    
- 예를 들어 회원이란 엔티티를 보면 회원 (이름, 아이디, 주소, 전화번호) 등이 있으며 서비스에 맞게 속성을 지정한다.

예를 들어, 회원과 같은 실제 세계의 중요한 객체들을 식별하고, 이들의 속성과 관계를 정의하면 엔터티가 될 수 있다.

- 데이터베이스 설계의 초기 단계에서 개념적 모델을 만들 때 사용된다.

![img1.daumcdn.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/b5c00412-dd37-4b7b-bdf6-0d833d846dc2/img1.daumcdn.png)

속성(**Attribute)** : 속성은 업무에서 필요로 하는 고유한 성질, 특징을 의미한다. 속성은 인스턴스의 구성요소로 더 이상 분리되지 않는 최소의 데이터 단위이다.

- 요구 사항을 기반으로 관리해야 할 필요가 있는 속성들만 엔터티의 속성이 된다.

인스턴스(**Instance)** : 인스턴스는 데이터베이스에 저장된 데이터 내용의 전체 집합을 의미한다.

---

## 릴레이션(**Relation)**

릴레이션은 관계형 데이터베이스**에서 정보를 구분하여 저장하는 기본 단위**이다. 

- 엔터티는 릴레이션으로 변환되며, 릴레이션은 행(레코드)과 열(필드)로 구성됩니다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/cc166779-8d96-4e31-8951-7780f42176ed/image.png)

- 예를 들어 회원 엔터티가 **있으면 DB 안에서 관리될 때 릴레이션으로 변경해서 관리**한다.
- 데이터베이스의 종류는 관계형 데이터베이스와 NoSQL 데이터베이스로 나눌 수 있는데 릴레이션은 관계형 DB에서 **테이블**이라고 하고 NoSQL DB에서는 **컬렉션**이라고 한다.

### **테이블과 컬렉션**

관계형 데이터베이스인 **MySQL**의 구조는 레코드-테이블-데이터베이스로 이루어져 있다.

- 레코드가 모여서 테이블을 만들고 테이블이 모여서 DB를 구성한다.

NoSQL 데이터베이스인 MongoDB의 구조는 도큐먼트-컬렉션-데이터베이스로 이루어져 있다.

- 도큐먼트가 모여 컬렉션을 만들고, 컬렉션이 모여서 DB를 구성한다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/5ec84c18-d672-4329-b9c8-d291a4ce54e2/image.png)

---

## 

---

## 도메인

도메인은 릴레이션의 각 속성이 가질 수 있는 값들의 집합을 의미한다.

![image (2).png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/3f4e1981-7810-497c-8c24-83c438d9b6ae/image_(2).png)

속성이 이름, 아이디, 주소 , 전화번호, 성별라면 도 메인은 특정 속성의 값이 가질 수 있는 범위나 타입을 정의한다.

- 예를 들어 성별이라는 속성이 가질 수 있는 값은 {남, 여} 라는 집합이 된다.
- 이름: 문자열, 최대 50자

---

## 필드와 레코드

- 지금까지 설명한 것을 기반으로 데이터베이스에서 필드와 레코드로 구성된 테이블을 만들 수 있다.
- 필드는 데이터베이스의 테이블에서 속성의 구체적인 데이터를 열 형태로 저장하는데 사용된다.
- 테이블은 관계형 데이터베이스에서 엔터티의 구체적인 데이터를 행과 열의 형태로 저장하는데 사용된다.
- 테이블에 쌓이는 행 단위의 데이터를 레코드라고 하는데, 튜플이라고도 부른다.

![ddd.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/553b234f-6b2a-47bc-b3b0-1ed8e53bddd7/ddd.png)

1. 회원 엔터티는 이름, 아이디, 주소, 번호 등의 속성을 가진다.
2. member 테이블은 name, ID, address, phonenumber 등의 필드를 가진다.
3. member 테이블의 각 행은 개별 회원의 정보를 저장하는 데 사용된다. 즉, 각 레코드는 name, ID, address, phonenumber 등의 필드에 대응하는 값들을 포함하며, 하나의 회원을 나타낸다.

### 필드 타입

- 필드는 타입을 갖는다. 예를 들어 이름은 문자열이고 전화번호는 숫자이다.
- 이러한 타입들은 DBMS마다 다르며 MySQL을 기준으로 알아보고자 한다.

### 숫자 타입

- 숫자 타입으로는 TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT 등이 있다.

### 날짜 타입

- 날짜 타입으로는 DATE, DATETIME, TIMESTAMP 등이 있다.

### 문자 타입

- CHAR, VARCHAR, TEXT, BLOB, ENUM, SET이 있다.

---

## 관계

데이터베이스에는 여러 개의 테이블이 있고 이러한 테이블은 서로의 관계가 정의되어 있는데, 이러한 관계를 관계화살표로 나타낼 수 있다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/ebb61fea-7111-49d6-b8d2-94660cf6429e/image.png)

### 1:1 관계

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/af3195cb-6b35-44eb-bee1-c35c7dcffb21/image.png)

1. 한 유저당 유저 이메일은 하나씩 있으므로 이 경우 1:1 관계가 된다.

2. 1:1 관계는 테이블을 두 개의 테이블로 나눠 테이블의 구조를 더 이해하기 쉽게 만들어 준다.

**N:M 관계**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/44f10a90-cdbf-4a5b-8571-4f660e51d447/image.png)

1. 학생도 강의를 많이 들을 수 있고 강의도 여러 명의 학생을 포함할 수 있으므로 이 경우 N:M 관계가 된다.

2. N:M 관계는 테이블 두 개를 직접적으로 연결해서 구축하지는 않고, 1:N, 1:M 관계를 갖는 테이블 두 개로 나눠서 설정한다.

---

## 키

- 테이블 간의 관계를 조금 더 명확하게 하고 테이블 자체의 인덱스를 위해 설정된 장치다.
- 기본키, 외래키, 후보키, 슈퍼키, 대체키가 있다.

![dawdfq.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/7d103149-88cd-4c61-b93d-e111778336cd/dawdfq.png)

1. 슈퍼키는 유일성이 있고 그 안에 포함된 후보키는 최소성까지 갖춘 키이다.
2. 후보키 중에서 기본키로 선택되지 못한 키는 대체키가 된다.
3. 유일성은 중복되는 값이 없다는 것이고 최소성은 최소 필드만 써서 키를 형성할 수 있는 것을 말한다.

### 기본키

기본키는 유일성과 최소성을 만족하는 키이다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/2d9a8f69-91a2-4e74-b0b2-d0e75d5e8745/image.png)

1. 테이블의 데이터 중 고유하게 존재하는 속성이며 기본키에 해당하는 데이터는 중복되어서는 안 된다.

2. 해당 예제에서는 PDT-0002 값이 중복되기 때문에 ID 필드는 기본키가 될 수 없다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/d7895c05-637e-40b6-b3d8-7fe1e6de59ff/image.png)

1. 해당 예제에서는 중복되는 값이 없기 때문에 ID 필드는 기본키가 될 수 있다.

2. {ID, name} 복합키를 기본키로 설정할 수 있지만, 이럴 경우 최소성을 만족하지 않는다.

### 외래키

외래키는 다른 테이블의 기본키를 그대로 참조하는 값으로 개체와의 관계를 식별하는 데 사용한다. 중복을 허용한다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/3b793990-edce-47d3-8f7a-9b1cdf3c3038/52c1467d-60c2-436c-abe2-8376edeee6cc/image.png)

1. 해당 예제에서는 user_id 필드에 a_2 값이 중복되는 것을 볼 수 있다.

2. client 테이블의 ID 기본키가 product 테이블의 user_id 외래키로 설정될 수 있음을 보여준다.

### 후보키

후보키는 기본키가 될 수 있는 후보들이며 유일성과 최소성을 동시에 만족하는 키이다.

### 대체키

대체키는 후보키가 두 개 이상일 경우 어느 하나를 기본키로 지정하고 남은 후보키들을 말한다.

### 슈퍼키

슈퍼키는 각 레코드를 유일하게 식별할 수 있는 유일성을 갖춘 키이다.
