Servlet
===
- HttpServlet을 상속받고 @WebServlet으로 url형식을 지정할 수 있음
  ```java
  @WebServlet("/test")
  public function TestServlet extends HttpServlet{
    //.....
  }
  ```
- Annotation을 쓰지 않고 web.xml을 이용해서 servlet클래스마다 url을 설정할 수 있다.
  ```java
  <servlet> //서블릿 정의
    <servlet-name>FirstServlet</servlet-name>      //servlet파일에 대해 이름 지정
    <servlet-class>FirstServlet</servlet-class>
  </servlet>

  <servlet-mapping> //url 매핑
    <servlet-name>FirstServlet</servlet-name> //위에서 미리 정의한 servlet의 name
    <url-pattern>/FirstServlet</url-pattern>   
  </servlet-mapping>
  ```
