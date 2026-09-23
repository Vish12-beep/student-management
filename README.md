Student Management - Spring MVC Demo
A complete Spring MVC (annotation-based, no XML) project demonstrating almost every
core concept, built around a simple Student CRUD app.
Concepts covered
Java-based config (`WebAppInitializer`, `WebConfig`, `RootConfig`) — no `web.xml`
DispatcherServlet (front controller pattern)
Layered architecture: Controller -> Service -> DAO -> Hibernate/MySQL
`@Controller` (returns JSP views) vs `@RestController` (returns JSON)
`@GetMapping` / `@PostMapping`, `@PathVariable`, `@RequestParam`, `@ModelAttribute`
Bean Validation (`@Valid` + `BindingResult` + `<form:errors>`)
Post/Redirect/Get pattern with `RedirectAttributes` (flash messages)
File upload (`MultipartFile`)
`HandlerInterceptor` (request logging)
`@ControllerAdvice` / `@ExceptionHandler` (global exception handling)
Internationalization (`MessageSource`, `LocaleResolver`, `LocaleChangeInterceptor`)
Static resource handling (CSS)
`@Transactional` declarative transactions
Connection pooling with HikariCP
1. Prerequisites
STS (Spring Tool Suite) with a Maven + Tomcat (8.5+/9) server configured
MySQL running locally
2. Database
You do NOT need to create tables manually — Hibernate's `hibernate.hbm2ddl.auto=update`
will create the `students` table automatically on first run. You only need the database
itself to exist (the JDBC URL below is also set with `createDatabaseIfNotExist=true`,
so even that's optional).
If you'd like to create it manually anyway:
```sql
CREATE DATABASE IF NOT EXISTS student\\\\\\\\\\\\\\\_db;
```
3. Configure your DB credentials
Open `src/main/java/com/example/studentmvc/config/RootConfig.java` and update:
```java
private static final String DB\\\\\\\\\\\\\\\_URL = "jdbc:mysql://localhost:3306/student\\\\\\\\\\\\\\\_db?...";
private static final String DB\\\\\\\\\\\\\\\_USER = "root";
private static final String DB\\\\\\\\\\\\\\\_PASSWORD = "root";   // <-- change to your MySQL password
```
4. Import into STS
File -> Import -> Maven -> Existing Maven Projects
Browse to this `student-mvc` folder -> Finish
Right-click project -> Maven -> Update Project (forces dependency download)
Right-click project -> Run As -> Run on Server (choose your Tomcat server)
5. Try it out
`http://localhost:8080/student-mvc/` -> redirects to the student list
`http://localhost:8080/student-mvc/students/new` -> add form
`http://localhost:8080/student-mvc/students?lang=fr` -> French UI (i18n demo)
`http://localhost:8080/student-mvc/api/students` -> JSON REST endpoint
6. Notes
If Tomcat's context path differs from `student-mvc`, adjust URLs above accordingly.
Uploaded photos are stored under `src/main/webapp/resources/uploads` at runtime (visible
under the deployed webapp's `resources/uploads` folder).
Console logs (via the logging interceptor) show every request's method, URI and timing —
check the STS Console view while the server runs.
