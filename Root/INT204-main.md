#### Rest Api
- ทำหน้าที่ควบคุม resource
- แล้วรอให้ front-end มาเรียกใช้งาน
- แต่ละ method มีหน้าที่ที่แตกต่างกัน เช่น get ขอข้อมูล
- การสื่อสารกันระหว่าง Front-End และ Back-End นั้นต้องใช้ .json
- เราใช้ postman ในการทดสอบ api
- เวลาเราทำ Rest เราควรจะทำเป็น Layered System
	- Controller (Presentation Layer)
		- ทำหน้าที่คุยกับ Front-End
	- Service (Business Logic Layer)
		- ประมวลผล Logic ต่าง ๆ
	- Repository (Persistence Layer)
		- เข้าถึง Database
	- ต้องเรียกลงมาเรื่อย ๆ เท่านั้น ==**ห้ามข้าม!!!**==
#### Spring Boot
- เป็น Project ที่สร้างขึ้นมาครอบ Spring framework
	- หัวใจหลักของ Spring framework คือ Dependency injection
	- Spring framework + Embedded HTTP Server - XML Config = Spring Boot
- เขียน Config แค่นิดเดียว
- เอา Tomcat มาเป็นส่วนนึงไปเลย ไม่ต้องมานั่ง Deploy เอง
- สามารถสร้าง Stand-Alone application ได้
- จะไปตรวจสอบว่าเราใช้ library อะไรอยู่บ้างแล้วมันจะเข้าไป auto-config ให้เรา
- ทำไมต้องใช้ 
	- เป็น Dependency injection
	- ทำ Starter Project ให้เรา
- Spring Boot Architecture
	- Presentation Layer 
		- มีหน้าที่ติดต่อกับ Front-End
		- มีหน้าที่ในการ Authentication (คุณเป็นใคร)
	- Business
		- ทำ Authorisation (คุณมีสิทธิ์ทำอะไรบ้าง)
		- ทำ Validation
		- ทำ Business logic
	- Persistence 
		- ทำ Storage logic ก่อนส่งไป Database
	- Database 
		- ทำ CRUD
- Spring Web Annotation
	- มีการ mapping ว่าจะไปที่ class ไหน
		- ใช้ `@RequestMapping("<path>")`
		- แล้วค่อยไปแยก method ที่ส่งมาทีหลังเช่น `@GetMapping , @PostMappin\g`
	- มีการแปลง body เป็น object ของ java ให้ (`@RequestBody`)
		- เป็นการไปขอ Body มาให้ เราไม่ต้องเขียนการแปลงเอง
	- `@pathVariable` ขอดู pathVariable ได้
	- ![Pasted image 20240126114219.png](./Pasted%20image%2020240126114219.png)
#### การใช้ h2.database 
- เพิ่ม Dependency และไป comment code ใน application.properties
	```
	<dependency>  
	    <groupId>com.h2database</groupId>  
	    <artifactId>h2</artifactId>  
	    <version>2.2.224</version>  
	    <scope>runtime</scope>  
	</dependency>
	```
- ทำไปเพื่อการทดสอบ Database เป็น database ใน main memory ไม่ใช่ database จริง ๆ
- เปิดปิด database นี้แล้วข้อมูลหายทันที
- ข้อมูลข้างในก็จะต้องเป็นไปตาม Constraint ของ Entity ที่เราเขียน
- ตอนเริ่มมาจะเป็น ```[]``` เพราะไม่มีข้อมูล แต่เชื่อมต่อ Database ได้แล้ว
- ดูข้อมูลได้ผ่าน
	- Postman
	- http://localhost:8080/h2-console
		- แล้วเอา ![Pasted image 20240126102840.png](./Pasted%20image%2020240126102840.png) ใน terminal ไปใส่ใน JBDC:URL
		- สามารถตั้งเองได้เช่น `spring.datasource.url = jdbc:h2:mem:demo` ใน application.properties
#### Exception Handling
##### HTTP Status Codes
- มีไว้เพื่อให้ฝั่ง client รู้ว่าสถานะเป็นอย่างไรบ้าง
- ประกอบไปด้วยดังนี้ 
	- 100-level (Informational) - server acknowledges a request
	- 200-level (Success) - server completed the request as expected
	- 300-level (Redirection) - client needs to perform further actions to complete the request
	- 400-level (Client error) - client sent an invalid request
	- 500-level (Server error) - server failed to fulfill a valid request due to an error with server
##### Handling Errors
- การส่ง Status code อาจจะแนบไปกับ Response body
- วิธีที่ง่ายที่สุดคือการส่ง Error Code ซึ่งมีอยู่ทั่วไปดังนี้
	- 400 Bad Request - ฝั่ง client ส่ง Request ไปไม่ดี ส่งผิด
	- 401 Unauthorized - ฝั่ง client ไม่สามารถยืนยันตัวตนได้
	- 403 Forbidden - ฝั่ง client ไม่มีสิทธิเข้าถึง Service นี้
	- 404 Not Found - ฝั่ง Server ไม่เจอ Resouce ที่ขอมา
	- 412 Precondition Failed - one or more conditions in the request header fields evaluated to false
	- 500 Internal Server Error - ฝั่ง Server มีปัญหา แต่ไม่เกี่ยวกับ Client
	- 503 Service Unavailable - the requested service is not available
##### Standardized Response Bodies
โดยปกติแล้วจะมีโครงสร้างดังนี้
```json
{
     "type": "/errors/incorrect-user-pass",
     "title": "Incorrect username or password.",
     "status": 401,
     "detail": "Authentication failed due to incorrect username or password.",
     "instance": "/login/log/abc123"
}
```
มีอยู่ 5 ส่วนด้วยกัน คือ
- type - a URI identifier that categorizes the error
- title - a brief, human-readable message about the error
- status - the HTTP response code (optional)
- detail - a human-readable explanation of the error
- instance - a URI that identifies the specific occurrence of the error
สามารถตั้งค่าให้ส่ง Error ไปแบบนี้ได้ด้วยการตั้งใน application.properties
```properties
server.error.include-stacktrace=on_param
server.error.include-exception=true //บอกให้แสดง EXCEPTION เพิ่ม
```
##### Flow การทำงาน
![Pasted image 20240308094442](./Pasted%20image%2020240308094442.png)
ซึี่งในตัว Spring Boot จะมี Tool ไว้ในแล้ว เช่น
###### @ResponseStatus
- อนุญาตให้มีการแก้ไข HTTP status ในการตอบกลับ
```java
package sit.int204.classicmodelsservice.exceptions;
import org.springframework.http.HttpStatus;  
import org.springframework.web.bind.annotation.ResponseStatus;  
  
@ResponseStatus(HttpStatus.NOT_FOUND) //บอกว่าให้ส่ง Status ไปแบบใดห์ (404)  
public class ItemNotFoundException extends RuntimeException{  
    public ItemNotFoundException(String message) {  
        super(message);  
    }  
}

// extends RuntimeException ประกาศว่าเป็น RuntimeException
```

```java
public Product getProductById(String productCode) { return  
        repository.findById(productCode).orElseThrow(()->  
                new ItemNotFoundException("Product code: "+ productCode + " does not exists !!!"));  
}
```
จากโค้ดข้างต้น ถ้าหา Product ไม่เจอ ก็ให้ทำการ โยน ( `.orElseThrow` ) ให้ `ItemNotFoundException`
ผลลัพธ์ที่ได้ตอนเกิด Exception
```json
{
    "timestamp": "2024-03-08T03:27:18.713+00:00",
    "status": 404,
    "error": "Not Found",
    "exception": "sit.int204.classicmodelsservice.exceptions.ItemNotFoundException",
    "message": "Product code: 1 does not exists !!!",
    "path": "/classic-models/products/1"
}
```
###### @ExceptionHandler
```java
//At ProductController

@ExceptionHandler(ItemNotFoundException.class)  
@ResponseStatus(HttpStatus.NOT_FOUND)  
public ItemNotFoundException handleItemNotFound(ItemNotFoundException exception){  
    return exception;  
}
```
จากโค้ดข้างต้น `handleItemNotFound` จะถูกเรียกตอนที่เกิด `ItemNotFoundException`
ซึ่งผลลัพธ์จากการ `return exception;`
```json
{
    "cause": null,
    "stackTrace": [
        {
            "classLoaderName": null,
            "moduleName": null,
            "moduleVersion": null,
            "methodName": "lambda$getProductById$0",
            "fileName": "ProductService.java",
            "lineNumber": 95,
            "nativeMethod": false,
            "className": "sit.int204.classicmodelsservice.services.ProductService"
        },
        {
            "classLoaderName": null,
            "moduleName": "java.base",
            "moduleVersion": "18.0.2.1",
            ...
```
###### @ControllerAdvice
```java
@RestControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {  
    @ExceptionHandler(ItemNotFoundException.class)  
    @ResponseStatus(HttpStatus.NOT_FOUND)  
    public ResponseEntity<ErrorResponse> handleItemNotFoundException(  
            ItemNotFoundException exception, WebRequest request) {  
        return buildErrorResponse(exception, HttpStatus.NOT_FOUND, request);  
    }  
  
    @ExceptionHandler(MethodArgumentNotValidException.class)  
    @ResponseStatus(HttpStatus.UNPROCESSABLE_ENTITY)  
    public ResponseEntity<ErrorResponse> handleMethodArgumentNotValid(  
            MethodArgumentNotValidException ex,  
            WebRequest request  
    ) {  
        ErrorResp...
```
สามารถกำหนดได้ว่า หากไม่ได้สั่งเรียก Exception เอง ให้มาเรียกที่นี่ เราจะได้ไม่จำเป้นต้องไปกำหนดในทุก ๆ Controller
##### Exception
###### Force Exception
เป็น Exception ที่ java จะบอกให้เราจัดการเอง ซึ่งเราสามารถ throw ไปที่อื่นได้
![Pasted image 20240308101237](./Pasted%20image%2020240308101237.png)จากรูปจะเห็นว่ามีการฟ้องว่ายังไม่ได้ Handle exception ตัวไหน

##### How Does Spring Process The Exception
![Pasted image 20240308112239](./Pasted%20image%2020240308112239.png)