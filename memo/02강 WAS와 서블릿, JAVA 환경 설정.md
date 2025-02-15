# 02강 WAS와 서블릿, JAVA 환경 설정

# 웹 서버

## 아파치

- 사용자의 요청이 정적 데이터인지 동적 데이터인지 판단한다.
- 정적 데이터일 경우 이미 준비된 HTML 문서를 그대로 응답해주며, 동적 데이터라면 웹 컨테이너에 요청을 보낸다.

## 웹 컨테이너(서블릿 컨테이너)

- 동적 데이터일 경우 JSP, 서블릿으로 연산 및 제어, DB에 접근해서 정제된 데이터(정적 데이터)가 완성되면 이를 응답해준다.

## WAS(Web Application Server) - 톰캣

- 동적 데이터를 처리할 서블릿을 메모리에 할당하며, web.xml을 참조하여 해당 서블릿에 대한 Thread를 생성한다. 서블릿 요청과 서블릿 응답 객체 생성 후 서블릿에 전달하면 연산 종료 후 메모리에서 해체시킨다.

## 서블릿(Servlet)

- Java 코드 안에 HTML 코드를 작성할 수 있는 Java 프로그램이다.
- Thread에 의해 서블릿에 있는 service() 메서드가 호출된다.
- 전송방식 요청에 맞게 doGet() 또는 doPost() 메서드를 호출한다.

## WAS

- WAS는 Response(응답) 객체를 HttpResponse 형태(정적 데이터)로 바꾸어서 웹 서버에 전달하고, 생성된 Thread를 종료시킨다. 그리고 HttpServletRequest와 HttpServletResponse 객체를 제거한다.

# 개발 환경 설정

[Java 개발 환경 설정하러 가기](https://blog.naver.com/coding_music/223457414418)

# 프로젝트 생성

1. Dynamic Web Project 선택

![image](https://github.com/user-attachments/assets/fb20f233-1145-47ed-802a-2fe6e729a509)

2. 항목 표시 후 Finish 클릭

![image 1](https://github.com/user-attachments/assets/a9134078-5baa-4952-b082-18573d4ced9f)

# 라이브러리 버젼 변경하기

1. 프로젝트 우클릭 후 Build Path 클릭 후 하위 항목 들어가기

![image 2](https://github.com/user-attachments/assets/6ad1aa6c-ee8d-475c-9f61-6ac1ba439310)

2. 라이브러리에 들어가서 라이브러리 버전 선택 후 Remove 클릭

![image 3](https://github.com/user-attachments/assets/bcf784ef-23c6-4af8-b6e5-c31a0ee31557)

3. 에드 라이브러리 클릭 후 JRE 시스템 라이브러리 추가

![image 4](https://github.com/user-attachments/assets/5daa492b-b8be-4c63-bdd0-94c6b85d7143)

