---
title: "스프링 부트 : REST 서비스"
excerpt: 스프링 부트로 RESTful 서비스 구축하기
header:
  actions:
    - label: 스프링 부트 더 알아보기
      url: https://jinhyun.blog/frameworks/spring-boot/
---

이 포스프는 스프링 부트를 사용해 간단한 RESTful 프로그램을 만듭니다.

## 1. 목표

직원 급여 관리 프로그램을 만들어 볼겁니다.

프로그램 구조는 직원 정보를 데이터베이스(H2)에 저장하고, 쿼리문(JPA)으로 질의해서 접근합니다. 그 결과를 인터넷에서 접근할 수 있도록 래핑합니다. (이것을 보통 스프링 MVC 계층이라고 합니다.)

## 2. 시작하기

해당 가이드는 Visual Studio Code를 사용하며 Spring Initializr 익스텐션을 사용합니다.

과정:

1. 명령 파레트 실행(`Ctrl` + `Shift` + `P`)
2. `Spring initializr: Create a Gradle Project...` 선택
3. `2.6.4` 버전 선택
4. `Java` 선택
5. 그룹 ID `com.example` 입력
6. 아티팩트 ID `restful` 입력
7. `Jar` 선택
8. 설치된 JDK 환경에 맞게 선택 (이 포스트는 1.8 기준입니다.)
9. 다음 의존성 선택
   1. Web
   2. JPA
   3. H2
    ![의존성](/assets/images/payroll-의존성.png)
10. 프로젝트를 생성할 경로 지정 후 열기

### 2.1. build.gradle

`build.gradle` 파일을 열면 다음과 같습니다.

{% highlight gradle linenos %}

plugins {
    id 'org.springframework.boot' version '2.6.4'
    id 'io.spring.dependency-management' version '1.0.11.RELEASE'
    id 'java'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '8'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation 'org.springframework.boot:spring-boot-starter-web'
    runtimeOnly 'com.h2database:h2'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

tasks.named('test') {
    useJUnitPlatform()
}

{% endhighlight %}

## 3. 엔티티 생성

먼저 엔티티를 만듭니다. 스프링에서 엔티티는 도메인 계층에 속해 있습니다.

**정보**: 지금은 도메인이 무슨 말이 이해가 잘 안 되시겠지만 스프링을 더 깊이 다루게 된다면 이해하게 됩니다. (지금은 몰라도 아무 지장 없습니다.)
{: .notice--info}

데이터베이스에서의 엔티티란 데이터의 집합을 말합니다. 여기서는 테이블과 같다고 생각하면 됩니다.

**정보**: 엔티티와 테이블은 개념상 비슷하나 동일한 개념은 아닙니다. 테이블은 데이터베이스에 물리적으로 존재하지만 엔티티는 개념으로만 말합니다.

예를 들어, 직원이라는 엔티티가 있다면 직원 A의 속성에는 이름, 직책, 연봉, 나이, 주민번호 등 다양한 속성이 존재합니다. 우리는 이 엔티티를 어떻게 소스 코드로 표현하는지 아래에서 살펴봅니다.

{% highlight java linenos %}

package com.example.payroll;

import java.util.Objects;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;

@Entity
public class Employee {

    private @Id @GeneratedValue Long id;
    private String name;
    private String role;

    Employee() {
    }

    Employee(String name, String role) {
        this.name = name;
        this.role = role;
    }

    public Long getId() {
        return this.id;
    }

    public String getName() {
        return this.name;
    }

    public String getRole() {
        return this.role;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setRole(String role) {
        this.role = role;
    }

    @Override
    public boolean equals(Object o) {

        if (this == o)
            return true;
        if (!(o instanceof Employee))
            return false;
        Employee employee = (Employee) o;
        return Objects.equals(this.id, employee.id) && Objects.equals(this.name, employee.name)
                && Objects.equals(this.role, employee.role);
    }

    @Override
    public int hashCode() {
        return Objects.hash(this.id, this.name, this.role);
    }

    @Override
    public String toString() {
        return "Employee{" + "id=" + this.id + ", name='" + this.name + '\'' + ", role='" + this.role + '\'' + '}';
    }
}

{% endhighlight %}

### 3.1. @Entity

`@Entity` 어노테이션이 붙은 클래스를 엔티티로 만듭니다. 정확히는 이 객체를 JPA 기반 데이터 저장소에 저장할 수 있도록 하는 JPA 어노테이션 입니다.

**정보**: JPA는 복잡한 SQL 질의문을 객체 지향에 맞게 질의할 수 있는 형식으로 만든 일종의 인터페이스입니다. 데이터베이스에 조회할 때마다 `SELECT ~`를 적는 노가다를 하지 않게 만듭니다.
{: .notice--info}

### 3.2. @ID

이 어노테이션이 붙은 필드 `id`를 `Emplyee` 엔티티의 Identity 속성으로 지정합니다.

### 3.3. @GeneratedValue

`id` 필드를 데이터베이스가 자동으로 1씩 증가하여 레코드를 삽입합니다. 프로그래머가 직접 1씩 증가하는 메서드 구현하는 것과 같은 효과의 어노테이션입니다.

## 4. 리포지토리 인터페이스 생성

방금 엔티티를 만들었으니 그 엔티티를 접근할 때 쓸 쿼리를 미리 정의합니다. 직원 급여 시스템에 필요한 질의문에는 무엇이 있을지 생각해봅시다.

- 새 직원 만들기 (Create)
- 직원 찾기 (Read)
- 기존 직원 정보 업데이트 (Update)
- 직원 삭제 (Delete)

위와 같이 기본적인 `CRUD`를 작성해야 할 것입니다. 그렇다면 각 쿼리문마다 메서드를 만들면 되는구나 싶겠지만 JPA는 그런 귀찮음을 없애줍니다.

다음 코드를 확인하세요.

`src/main`java.com/example/payroll/EmployeeRepository.java`:

{% highlight java linenos %}

package com.example.payroll;

import org.springframework.data.jpa.repository.JpaRepository;

public interface EmployeeRepository extends JpaRepository<Employee, Long> {

}

{% endhighlight %}

메서드는 작성되어 있지 않고 `JpaRepository`가 상속되었습니다. 앞서 말한 CRUD 기능이 모두 포함되어 있는 게 `JpaRepository`입니다. 제네릭에는 도메인 유형 엔티티 클래스와 ID 타입을 써주면 됩니다.

## 5. 데이터베이스 사전 구성

데이터를 담을 엔티티 클래스와 데이터베이스에 접근할 때 쓸 리포지토리 인터페이스도 만들었습니다. 모든 것을 할 수 있는 상태이지만 지금은 실습을 하는 상태이기 때문에 미리 데이터를 삽입하도록 하겠습니다.

`src/main/java.com/example/payroll/LoadDatabase.java`:

{% highlight java linenos %}

package com.example.payroll;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.boot.CommandLineRunner;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class LoadDatabase {
    private static final Logger log = LoggerFactory.getLogger(LoadDatabase.class);

    @Bean
    CommandLineRunner initDatabase(EmployeeRepository repository) {
        return args -> {
            log.info("Preloading " + repository.save(new Employee("Bilbo Baggins", "burglar")));
            log.info("Preloading " + repository.save(new Employee("Frodo Baggins", "thief")));
        };
    }
}

{% endhighlight %}

스프링 부트는 `CommandLineRunner` 애플리케이션 컨텍스트가 로드되면 모든 Bean을 실행합니다.

이 러너는 방금 생성한 EmployeeRepository의 카피를 요청합니다.

그 카피를 사용해 두 개의 엔티티를 생성하고 저장합니다.

## 6. payroll 실행

엔티티와 리포지토리 인터페이스, 데이터도 준비되었습니다. 이제 앱을 시작해볼 차례입니다.

VS Code에서 스프링 앱을 시작하는 방법은 크게 두 가지인데 명령 파레트 기준으로 설명드리겠습니다.

1. 명령 파레트 실행 (`Ctrl` + `Shift` + `P`)
2. `Spring Boot Dashboard: Run ...` 선택

디버그 콘솔 창이 하단에 생기면서 아래와 같이 출력됩니다.

`Debug Console`:
{% highlight console linenos %}

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v2.6.4)

2022-03-21 20:50:16.479  INFO 11806 --- [           main] com.example.payroll.PayrollApplication   : Starting PayrollApplication using Java 1.8.0_312 on JJH-LEGION5PRO with PID 11806 (/home/jjh/projects/payroll/bin/main started by jjh in /home/jjh/projects/payroll)
2022-03-21 20:50:16.480  INFO 11806 --- [           main] com.example.payroll.PayrollApplication   : No active profile set, falling back to 1 default profile: "default"
2022-03-21 20:50:16.916  INFO 11806 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Bootstrapping Spring Data JPA repositories in DEFAULT mode.
2022-03-21 20:50:16.962  INFO 11806 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Finished Spring Data repository scanning in 39 ms. Found 1 JPA repository interfaces.
2022-03-21 20:50:17.320  INFO 11806 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2022-03-21 20:50:17.327  INFO 11806 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2022-03-21 20:50:17.328  INFO 11806 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.58]
2022-03-21 20:50:17.373  INFO 11806 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2022-03-21 20:50:17.373  INFO 11806 --- [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 863 ms
2022-03-21 20:50:17.539  INFO 11806 --- [           main] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Starting...
2022-03-21 20:50:17.759  INFO 11806 --- [           main] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Start completed.
2022-03-21 20:50:17.800  INFO 11806 --- [           main] o.hibernate.jpa.internal.util.LogHelper  : HHH000204: Processing PersistenceUnitInfo [name: default]
2022-03-21 20:50:17.839  INFO 11806 --- [           main] org.hibernate.Version                    : HHH000412: Hibernate ORM core version 5.6.5.Final
2022-03-21 20:50:17.955  INFO 11806 --- [           main] o.hibernate.annotations.common.Version   : HCANN000001: Hibernate Commons Annotations {5.1.2.Final}
2022-03-21 20:50:18.030  INFO 11806 --- [           main] org.hibernate.dialect.Dialect            : HHH000400: Using dialect: org.hibernate.dialect.H2Dialect
2022-03-21 20:50:18.355  INFO 11806 --- [           main] o.h.e.t.j.p.i.JtaPlatformInitiator       : HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
2022-03-21 20:50:18.361  INFO 11806 --- [           main] j.LocalContainerEntityManagerFactoryBean : Initialized JPA EntityManagerFactory for persistence unit 'default'
2022-03-21 20:50:18.602  WARN 11806 --- [           main] JpaBaseConfiguration$JpaWebConfiguration : spring.jpa.open-in-view is enabled by default. Therefore, database queries may be performed during view rendering. Explicitly configure spring.jpa.open-in-view to disable this warning
2022-03-21 20:50:18.952  INFO 11806 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2022-03-21 20:50:18.961  INFO 11806 --- [           main] com.example.payroll.PayrollApplication   : Started PayrollApplication in 2.723 seconds (JVM running for 3.016)
2022-03-21 20:50:19.016  INFO 11806 --- [           main] com.example.payroll.LoadDatabase         : Preloading Employee{id=1, name='Bilbo Baggins', role='burglar'}
2022-03-21 20:50:19.018  INFO 11806 --- [           main] com.example.payroll.LoadDatabase         : Preloading Employee{id=2, name='Frodo Baggins', role='thief'}
2022-03-21 20:51:43.317  INFO 11806 --- [nio-8080-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
2022-03-21 20:51:43.317  INFO 11806 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
2022-03-21 20:51:43.318  INFO 11806 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 1 ms

{% endhighlight %}

여기서 우리가 주목할 부분은 29 ~ 30 줄 입니다.

{% highlight console %}

2022-03-21 20:50:19.016  INFO 11806 --- [           main] com.example.payroll.LoadDatabase         : Preloading Employee{id=1, name='Bilbo Baggins', role='burglar'}
2022-03-21 20:50:19.018  INFO 11806 --- [           main] com.example.payroll.LoadDatabase         : Preloading Employee{id=2, name='Frodo Baggins', role='thief'}

{% endhighlight %}

우리가 사전에 만들어준 데이터가 구성되었습니다. 우리는 별다른 연결 작업을 해주지 않았는데 어떻게 이게 가능했을까요? 다음 섹션에서 자세히 알아보도록 하겠습니다.

## 7. PayrollApplication

프로젝트를 생성하면서 처음부터 존재했던 `PayrollApplication.java` 파일이 있는데 다음 내용을 살펴봅니다.

`src/main/java.com/example/payroll/PayrollApplication.java`:

{% highlight java linenos %}

package com.example.payroll;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class PayrollApplication {

    public static void main(String[] args) {
        SpringApplication.run(PayrollApplication.class, args);
    }

}

{% endhighlight %}

`public static void main()` 메서드가 있으므로 우리는 이 클래스가 프로그램의 시작점이라는 것을 알 수 있습니다.

### 7.1. @SpringBootApplication

`@SpringBootApplication` 어노테이션은 컴포넌트 스캔, 자동 구성, 프로퍼티 지원을 가져옵니다.

여기서 더 자세히 설명하지는 않습니다. 아직 개념이 부족한 상태이기 때문에 억지로 설명하지는 않고 그냥 이 어노테이션 덕분에 다른 클래스들을 가져올 수 있다라고 생각해도 충분합니다.

## 8. 웹으로 제공

콘솔로만 데이터의 존재를 확인할 수 있으면 무슨 의미가 있을까요? 사용자가 사용할 수 있으려면 웹으로 제공해야 합니다. 이를 리포지토리를 웹 계층으로 래핑한다고 말합니다. 래핑을 하려면 스프링 MVC로 전환해야 합니다.

**정보**: 앞의 말이 조금 어렵게 느껴질 수 있는 데 간단하게 말하면 여러분이 지금 보고 있는 이 포스트의 주소처럼 사용자가 웹 주소로 접근할 수 있게 표현한다는 의미입니다.
{: .notice--info}

### 8.1. EmployeeController

`src/main/java/payroll/EmployeeController.java`:

{% highlight java linenos %}

package com.example.payroll;

import java.util.List;

import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

@RestController
class EmployeeController {

  private final EmployeeRepository repository;

  EmployeeController(EmployeeRepository repository) {
    this.repository = repository;
  }

  @GetMapping("/employees")
  List<Employee> all() {
    return repository.findAll();
  }
  // end::get-aggregate-root[]

  @PostMapping("/employees")
  Employee newEmployee(@RequestBody Employee newEmployee) {
    return repository.save(newEmployee);
  }

  @GetMapping("/employees/{id}")
  Employee one(@PathVariable Long id) {

    return repository.findById(id)
      .orElseThrow(() -> new EmployeeNotFoundException(id));
  }

  @PutMapping("/employees/{id}")
  Employee replaceEmployee(@RequestBody Employee newEmployee, @PathVariable Long id) {

    return repository.findById(id)
      .map(employee -> {
        employee.setName(newEmployee.getName());
        employee.setRole(newEmployee.getRole());
        return repository.save(employee);
      })
      .orElseGet(() -> {
        newEmployee.setId(id);
        return repository.save(newEmployee);
      });
  }

  @DeleteMapping("/employees/{id}")
  void deleteEmployee(@PathVariable Long id) {
    repository.deleteById(id);
  }
}

{% endhighlight %}

- `@RestController` 어노테이션은 각 메서드에서 리턴된 데이터가 템플릿을 렌더링하는 대신 응답 body에 직접 기록되는 것을 나타냅니다.
- `EmployeeRepository`는 생성자에 의해 컨트롤러에 주입됩니다.
- 각 작업(`@GetMapping`, `@PostMapping`, `@PutMapping` 및 `@DeleteMapping`, HTTP GET, POST, PUT 및 DELETE 호출에 해당)에 대한 경로가 있습니다.
- `EmployeeNotFoundException`은 직원을 조회했지만 찾을 수 없는 경우를 나타내는 데 사용되는 예외입니다.

### 8.2. 조회 에러 처리

직원을 조회했지만 찾을 수 없는 경우는 무엇이 있을까요?

간단한 예시를 들어보면 직원 레코드가 30개가 있다고 가정합니다. ID는 1 부터 30까지 있을 겁니다. 그렇다면 ID가 31인 직원을 조회하면 어떻게 될까요? 당연히 ID가 31인 직원 레코드가 없으니 조회 결과는 없습니다. 이 에러를 처리하기 위한 클래스를 생성합니다.

`src/main/java/payroll/EmployeeNotFoundException.java`:

{% highlight java linenos %}

package com.example.payroll;

class EmployeeNotFoundException extends RuntimeException {

  EmployeeNotFoundException(Long id) {
    super("Could not find employee " + id);
  }
}

{% endhighlight %}

EmployeeNotFoundException이 발생하면 스프링 MVC 구성의 이 추가 정보가 HTTP 404를 렌더링하는 데 사용됩니다.

{% highlight java linenos %}

package com.example.payroll;

import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.ResponseStatus;

@ControllerAdvice
class EmployeeNotFoundAdvice {

  @ResponseBody
  @ExceptionHandler(EmployeeNotFoundException.class)
  @ResponseStatus(HttpStatus.NOT_FOUND)
  String employeeNotFoundHandler(EmployeeNotFoundException ex) {
    return ex.getMessage();
  }
}

{% endhighlight %}

- `@ResponseBody`는 이 어드바이스가 응답 본문에 직접 렌더링된다는 신호를 보냅니다.
- `@ExceptionHandler`는 EmployeeNotFoundException이 발생한 경우에만 응답하도록 어드바이스를 구성합니다.
- `@ResponseStatus`는 HttpStatus.NOT_FOUND, 즉 HTTP 404를 발행한다고 말합니다.
- 어드바이스의 본문은 콘텐츠를 생성합니다. 이 경우 예외 메시지를 제공합니다.

## 9. 중간점검

Payroll 애플리케이션을 실행합니다.

실행 방법은 [섹션 6 payroll 실행](#6-payroll-실행)과 동일합니다.

이제 실제로 어떻게 보여지는지 확인해볼 차례입니다. 아래 주소를 클릭하면 employee 데이터베이스의 내용을 확인할 수 있습니다.

<http://localhost:8080/employees>{:target="_blank"}

![Payrolll 로컬호스트 테스트](../../../assets/images/payroll-localhost-test.gif)
