---
title:  "서블릿 필터"
search: true
categories: 
  - Servlet
tags:
  - servlet
  - web
  - server
  - java
  - filter
last_modified_at: 2020-02-19T18:54:00-05:00
toc: true
---

# Filter
서블릿 실행 전후에 작업을 할 때 사용하는 기술  

## 필터 만들기
javax.servlet.Filter 인터페이스로 구현  

- **init()**  
`init()` 메서드는 필터 객체가 생성되고 준비 작업을 위해 한 번 호출  
매개변수는 FilterConfig 객체, 이 객체를 통해 필터 초기화 매개변수의 값을 사용  

- **doFilter()**  
필터와 연결된 URL에 대해 요청이 들어오면 `doFilter()`가 항상 호출  
필터가 할 일 작성  

- **destroy()**  
서블릿 컨테이너는 웹 애플리케이션을 종료하기 전에  
필터들에 대해 `destroy()`를 호출하여 마무리 작업을 할 수 있는 기회를 줌  

```java
public class ExampleFilter implements Filter {
	FilterConfig config;
	
	@Override
	public void init(FilterConfig config) throws ServletException {
		this.config = config;
	}

	@Override
	public void doFilter(ServletRequest request, ServletResponse response, 
			FilterChain chain) throws IOException, ServletException {
		/* 서블릿이 실행되기 전에 해야 할 작업 */

		chain.doFilter(request, response);	// 다음 필터 호출, 더이상 필터가 없다면 서블릿의 service()가 호출

		/* 서블릿을 실행한 후, 클라이언트에게 응답하기 전에 해야할 작업 */
	}

	@Override
	public void destroy() {}
}
```

## 필터의 배치
필터의 배치 방법도 서블릿과 마찬가지로  
DD파일에 기술하는 방법과 애노테이션으로 기술하는 방법  

### DD파일에 필터 배치 정보 설정
`web.xml` 파일에 문자 집합을 설정하는 필터를 등록  
```html
  <!-- 필터 선언 -->
  <filter>
  	<filter-name>필터 별명</filter-name>
  	<filter-class>필터 클래스 이름</filter-class>
  	
  	<init-param>
  		<param-name>매개변수 이름</param-name>
  		<param-value>매개변수 값</param-value>
  	</init-param>
  </filter>
  
  <!-- 필터 URL 매핑 -->
  <filter-mapping>
  	<filter-name>`<filter>`에서 정의한 이름</filter-name>
  	<url-pattern>필터가 적용될 URL</url-pattern>
  </filter-mapping>
```
**Note** : `<init-param>` - 필터가 사용할 정적인 데이터를 정의
{: .notice--info}  

## 애노테이션을 이용한 필터 배치
`@WebFilter` 애노테이션을 사용하여 필터의 소스 파일에 직접 배치 정보 설정  

```java
@WebFilter(
		urlPatterns="URL",
		initParams= {
				@WebInitParam(name="매개변수 이름", value=매개변수 값)
		})
public class ExampleFilter implements Filter {
	...
}
```
