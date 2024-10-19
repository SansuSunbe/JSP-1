# 04강 서블릿 & JSP 페이지 이동

# JSP 파일 생성 시 오류 해결

- 프로젝트의 build path에 들어간다.

![image](https://github.com/user-attachments/assets/92c8e1d9-a7c1-472e-bda2-fd4fbca685ae)

- Class Path 클릭 후 라이브러리 추가를 누른다.

![image 1](https://github.com/user-attachments/assets/eec790f6-87fa-4e29-b00d-84ac400cfc53)

- 설치한 톰캣을 추가해준다.

![image 2](https://github.com/user-attachments/assets/f6dc9379-7dff-4181-8bba-f14a070444f2)

- Order and Export 에서 모든 항목 체크 후 적용 후 닫는다.

![image 3](https://github.com/user-attachments/assets/c3a845a8-ff7f-4e07-8d40-70b0e4fd73e5)

- 그래도 오류가 생긴다면 지시어에 “<%@“를 → “<% @” 띄웠다 붙여주고 저장한다.
    
![image 4](https://github.com/user-attachments/assets/6556241d-b3ac-41eb-a711-874a5dd495b7)

- 띄어쓰기 후 되돌리기 하니 에러가 사라짐

![image 5](https://github.com/user-attachments/assets/37927122-bf7c-4586-9634-93bf40574110)

# SERVLET 파일 생성

- src 경로에 servlet 파일을 생성해준다.

![image 6](https://github.com/user-attachments/assets/d5f3123d-91bc-4a53-9010-10bf99ad450e)

# jsp & servlet 간의 이동

- JSP에서 작성한 코드를 실행시키면 <form> 태그에 지정해 놓은 servlet에 method방식을 정하면 전달된다.

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JSP 페이지</title>
</head>
<body>
	<h1>JSP로 만든 페이지</h1>
	<form action="Hello" method="post">
		<p>서블릿으로 이동</p>
		<button>이동</button>
	</form>
</body>
</html>
```

```java
package com.online.servlet;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class MyServlet
 */
@WebServlet("/Hello")
public class MyServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public MyServlet() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html; charset=UTF-8"); // <- 인코딩 타입 설정
		PrintWriter out = response.getWriter();
		out.println("<html><body><h1>서블릿으로 만든 페이지</h1>");
		out.println("<a href='index.jsp'>JSP로 이동</a>");
		out.close();
		// TODO Auto-generated method stub
		response.getWriter().append("Served at: ").append(request.getContextPath());
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html; charset=UTF-8"); // <- 인코딩 타입 설정
		PrintWriter out = response.getWriter();
		out.println("<html><body><h1>서블릿으로 만든 페이지</h1>");
		out.println("<a href='Baby'>JSP로 이동</a>");
		out.close();
		// TODO Auto-generated method stub
		doGet(request, response);
	}

}
```

- method 방식을 post 방식으로 보낼 때 web.xml을 <url-mapping> 태그로 이용자에게 나타날 페이지 주소를 감출 수 있다.

![image 7](https://github.com/user-attachments/assets/faf650ff-bbd2-436c-a9cd-c90188fca4c6)

```java
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>day04</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.jsp</welcome-file>
    <welcome-file>default.htm</welcome-file>
  </welcome-file-list>
  
  <servlet>
  	<servlet-name>baby</servlet-name>
  	<jsp-file>/index.jsp</jsp-file>
  </servlet>
  <servlet-mapping>
  	<servlet-name>baby</servlet-name>
  	<url-pattern>/Baby</url-pattern>
  </servlet-mapping>
</web-app>
```

# post, get 메서드 차이

- get 방식으로 전달할 때의 주소

![image 8](https://github.com/user-attachments/assets/bc18cdf8-1554-4f61-bc85-55b84fe17895)

- post 방식으로 전달할 때의 주소
  
![image 9](https://github.com/user-attachments/assets/48345b06-3f6c-44b0-b3b0-ce7c42fbb8a1)

- post 방식으로 전달하게 되면 web.xml을 한번 더 거치게 된다.
- 즉 보안 면에서는 post 방식이 더 우위지만 속도 면에서는 get 방식에 비해 떨어지게 된다.
