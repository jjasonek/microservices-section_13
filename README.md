# Udemy Course Microservices with Spring Boot, Docker, Kubernetes Section_11
https://www.udemy.com/course/master-microservices-with-spring-docker-kubernetes/
## spring version: 3.4.5
## gatewayservice version: 3.5.0
## Java 21


## Documentation
After adding the library, the swagger page is accessible through address 
http://localhost:8080/swagger-ui/index.html,
http://localhost:8090/swagger-ui/index.html,
http://localhost:9000/swagger-ui/index.html.

## links

### Eureka Server dashboard
http://localhost:8070/

### Link from Eureka Server to Gateway Server
http://172.24.64.1:8072/actuator/info
{
    "app": {
        "name": "gatewayserver",
        "description": "Eazy Bank Gateway Server Application",
        "version": "1.0.0"
    }
}

### Further links
http://localhost:8072/actuator
http://localhost:8072/actuator/gateway
http://localhost:8072/actuator/gateway/routes

### Example invoking an service:
POST http://localhost:8072/eazybank/accounts/api/create


### actuator links:
http://localhost:8072/actuator
http://localhost:8071/actuator
http://localhost:8070/actuator
http://localhost:8080/actuator
http://localhost:8090/actuator
http://localhost:9000/actuator


## Add MessageFunctions

2025-07-09T22:59:30.288+02:00  INFO 19024 --- [message] [           main] c.eazybytes.message.MessageApplication   : Starting MessageApplication using Java 22.0.1 with PID 19024 (C:\Training\Microservices\section_13\message\target\classes started by jijas in C:\Training\Microservices\section_13)
2025-07-09T22:59:30.295+02:00  INFO 19024 --- [message] [           main] c.eazybytes.message.MessageApplication   : No active profile set, falling back to 1 default profile: "default"
2025-07-09T22:59:31.100+02:00  INFO 19024 --- [message] [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port 8080 (http)
2025-07-09T22:59:31.116+02:00  INFO 19024 --- [message] [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2025-07-09T22:59:31.116+02:00  INFO 19024 --- [message] [           main] o.apache.catalina.core.StandardEngine    : Starting Servlet engine: [Apache Tomcat/10.1.42]
2025-07-09T22:59:31.155+02:00  INFO 19024 --- [message] [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2025-07-09T22:59:31.157+02:00  INFO 19024 --- [message] [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 812 ms
2025-07-09T22:59:31.592+02:00  INFO 19024 --- [message] [           main] o.s.c.f.web.mvc.FunctionHandlerMapping   : FunctionCatalog: org.springframework.cloud.function.context.catalog.BeanFactoryAwareFunctionRegistry@5df6163a
2025-07-09T22:59:31.628+02:00  INFO 19024 --- [message] [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port 8080 (http) with context path '/'
2025-07-09T22:59:31.635+02:00  INFO 19024 --- [message] [           main] c.eazybytes.message.MessageApplication   : Started MessageApplication in 1.835 seconds (process running for 3.32)


### Application starts by default on port 8080 and name of the function is the API path. 

POST http://localhost:8080/email
...
2025-07-09T23:05:38.455+02:00  WARN 19024 --- [message] [nio-8080-exec-1] c.f.c.c.BeanFactoryAwareFunctionRegistry : Failed to locate function 'email' for function definition 'email'. Returning null.
2025-07-09T23:05:38.583+02:00  INFO 19024 --- [message] [nio-8080-exec-1] c.e.message.functions.MessageFunctions   : Sending email with the details: AccountsMsgDto[accountNumber=1234545454, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437687]

POST http://localhost:8080/sms
...
2025-07-09T23:13:31.060+02:00  WARN 19024 --- [message] [nio-8080-exec-4] c.f.c.c.BeanFactoryAwareFunctionRegistry : Failed to locate function 'sms' for function definition 'sms'. Returning null.
2025-07-09T23:13:31.062+02:00  INFO 19024 --- [message] [nio-8080-exec-4] c.e.message.functions.MessageFunctions   : Sending sms with the details: AccountsMsgDto[accountNumber=1234545454, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437687]


## Test composed functions

POST http://localhost:9010/email
...
2025-07-09T23:24:01.210+02:00  WARN 2280 --- [message] [nio-9010-exec-2] c.f.c.c.BeanFactoryAwareFunctionRegistry : Failed to locate function 'email' for function definition 'email'. Returning null.
2025-07-09T23:24:01.319+02:00  INFO 2280 --- [message] [nio-9010-exec-2] c.e.message.functions.MessageFunctions   : Sending email with the details: AccountsMsgDto[accountNumber=1234545454, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437687]

POST http://localhost:9010/sms
...
2025-07-09T23:24:06.695+02:00  WARN 2280 --- [message] [nio-9010-exec-3] c.f.c.c.BeanFactoryAwareFunctionRegistry : Failed to locate function 'sms' for function definition 'sms'. Returning null.
2025-07-09T23:24:06.697+02:00  INFO 2280 --- [message] [nio-9010-exec-3] c.e.message.functions.MessageFunctions   : Sending sms with the details: AccountsMsgDto[accountNumber=1234545454, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437687]

POST http://localhost:9010/emailsms
...
2025-07-09T23:29:40.778+02:00  WARN 2280 --- [message] [nio-9010-exec-6] c.f.c.c.BeanFactoryAwareFunctionRegistry : Failed to locate function 'emailsms' for function definition 'emailsms'. Returning null.
2025-07-09T23:29:40.783+02:00  WARN 2280 --- [message] [nio-9010-exec-6] c.f.c.c.BeanFactoryAwareFunctionRegistry : Failed to locate function 'emailsms' for function definition 'emailsms'. Returning null.
2025-07-09T23:29:40.786+02:00  INFO 2280 --- [message] [nio-9010-exec-6] c.e.message.functions.MessageFunctions   : Sending email with the details: AccountsMsgDto[accountNumber=1234545454, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437687]
2025-07-09T23:29:40.786+02:00  INFO 2280 --- [message] [nio-9010-exec-6] c.e.message.functions.MessageFunctions   : Sending sms with the details: AccountsMsgDto[accountNumber=1234545454, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437687]
2025-07-09T23:29:40.787+02:00  WARN 2280 --- [message] [nio-9010-exec-6] c.f.c.c.BeanFactoryAwareFunctionRegistry : Failed to locate function 'emailsms' for function definition 'emailsms'. Returning null.
2025-07-09T23:29:40.789+02:00  WARN 2280 --- [message] [nio-9010-exec-6] c.f.c.c.BeanFactoryAwareFunctionRegistry : Failed to locate function 'emailsms' for function definition 'emailsms'. Returning null.


## Test non blocking notification about created account

### run Redis server
docker run -p 6379:6379 --name eazyredis -d redis
### Start RabbitMQ
docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:4-management
### start KeyCloak Docker container
docker run -d -p 127.0.0.1:7080:8080 -e KC_BOOTSTRAP_ADMIN_USERNAME=admin -e KC_BOOTSTRAP_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:26.3.0 start-dev
### login to RabbitMQ
http://localhost:15672/
guest/guest

### Invoke the API
POST http://localhost:8072/eazybank/accounts/api/create

### accounts log
2025-07-10T20:35:13.321+02:00  INFO [accounts,,] 40456 --- [accounts] [nio-8080-exec-1] c.e.a.service.impl.AccountServiceImpl    : Sending communication for the details: AccountsMsgDto[accountNumber=1446456721, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437689]
2025-07-10T20:35:13.331+02:00  INFO [accounts,,] 40456 --- [accounts] [nio-8080-exec-1] o.s.c.s.binder.DefaultBinderFactory      : Creating binder: rabbit
2025-07-10T20:35:13.331+02:00  INFO [accounts,,] 40456 --- [accounts] [nio-8080-exec-1] o.s.c.s.binder.DefaultBinderFactory      : Constructing binder child context for rabbit
2025-07-10T20:35:13.554+02:00  INFO [accounts,,] 40456 --- [accounts] [nio-8080-exec-1] o.s.c.s.binder.DefaultBinderFactory      : Caching the binder: rabbit
2025-07-10T20:35:13.619+02:00  INFO [accounts,,] 40456 --- [accounts] [nio-8080-exec-1] o.s.a.r.c.CachingConnectionFactory       : Attempting to connect to: [localhost:5672]
2025-07-10T20:35:13.707+02:00  INFO [accounts,,] 40456 --- [accounts] [nio-8080-exec-1] o.s.a.r.c.CachingConnectionFactory       : Created new connection: rabbitConnectionFactory#400aa720:0/SimpleConnection@4437350c [delegate=amqp://guest@127.0.0.1:5672/, localPort=65323]
2025-07-10T20:35:13.751+02:00  INFO [accounts,,] 40456 --- [accounts] [nio-8080-exec-1] o.s.c.s.m.DirectWithAttributesChannel    : Channel 'accounts.sendCommunication-out-0' has 1 subscriber(s).
2025-07-10T20:35:13.788+02:00  INFO [accounts,,] 40456 --- [accounts] [nio-8080-exec-1] o.s.a.r.c.CachingConnectionFactory       : Attempting to connect to: [localhost:5672]
2025-07-10T20:35:13.794+02:00  INFO [accounts,,] 40456 --- [accounts] [nio-8080-exec-1] o.s.a.r.c.CachingConnectionFactory       : Created new connection: rabbitConnectionFactory.publisher#1f2e3612:0/SimpleConnection@7b17aae2 [delegate=amqp://guest@127.0.0.1:5672/, localPort=65324]
2025-07-10T20:35:13.808+02:00  INFO [accounts,,] 40456 --- [accounts] [nio-8080-exec-1] c.e.a.service.impl.AccountServiceImpl    : Is the communication request successfully triggered? : true
2025-07-10T20:35:36.617+02:00  INFO [accounts,,] 40456 --- [accounts] [rap-executor-%d] c.n.d.s.r.aws.ConfigClusterResolver      : Resolving eureka endpoints via configuration

### message log
2025-07-10T20:35:14.076+02:00  INFO 33308 --- [message] [ation.message-1] c.e.message.functions.MessageFunctions   : Sending email with the details: AccountsMsgDto[accountNumber=1446456721, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437689]
2025-07-10T20:35:14.081+02:00  INFO 33308 --- [message] [ation.message-1] c.e.message.functions.MessageFunctions   : Sending sms with the details: AccountsMsgDto[accountNumber=1446456721, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437689]


## Test non blocking notification about created account and notification about sent communication

### accounts log (I postponed sending communication by a breakpoint inside the email function)
Hibernate: insert into accounts (account_type,branch_address,communication_sw,created_at,created_by,customer_id,account_number) values (?,?,?,?,?,?,?)
2025-07-10T22:58:47.594+02:00  INFO [accounts,,] 37516 --- [accounts] [nio-8080-exec-8] c.e.a.service.impl.AccountServiceImpl    : Sending communication for the details: AccountsMsgDto[accountNumber=1124062841, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437688]
2025-07-10T22:58:47.597+02:00  INFO [accounts,,] 37516 --- [accounts] [nio-8080-exec-8] c.e.a.service.impl.AccountServiceImpl    : Is the communication request successfully triggered? : true
2025-07-10T23:01:16.827+02:00  INFO [accounts,,] 37516 --- [accounts] [sent.accounts-1] c.e.accounts.functions.AccountFunctions  : Updating communication status for the account number: 1124062841
Hibernate: select a1_0.account_number,a1_0.account_type,a1_0.branch_address,a1_0.communication_sw,a1_0.created_at,a1_0.created_by,a1_0.customer_id,a1_0.updated_at,a1_0.updated_by from accounts a1_0 where a1_0.account_number=?
Hibernate: select a1_0.account_number,a1_0.account_type,a1_0.branch_address,a1_0.communication_sw,a1_0.created_at,a1_0.created_by,a1_0.customer_id,a1_0.updated_at,a1_0.updated_by from accounts a1_0 where a1_0.account_number=?
Hibernate: update accounts set account_type=?,branch_address=?,communication_sw=?,customer_id=?,updated_at=?,updated_by=? where account_number=?

### message log
2025-07-10T23:01:16.786+02:00  INFO 40096 --- [message] [ation.message-1] c.e.message.functions.MessageFunctions   : Sending email with the details: AccountsMsgDto[accountNumber=1124062841, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437688]
2025-07-10T23:01:16.791+02:00  INFO 40096 --- [message] [ation.message-1] c.e.message.functions.MessageFunctions   : Sending sms with the details: AccountsMsgDto[accountNumber=1124062841, name=Madan Reddy, email=tutor@eazybytes, mobileNumber=4354437688]


## Docker compose

### for all microservices we call following to generate docker images s11:
mvn compile jib:dockerBuild

docker image ls --filter=reference="jjasonek/*:s13"

Alternatively you can use (on Linux):
docker images | grep s13

### push images to docker hub:
docker image push docker.io/jjasonek/accounts:s13
docker image push docker.io/jjasonek/loans:s13
docker image push docker.io/jjasonek/cards:s13
docker image push docker.io/jjasonek/message:s13
docker image push docker.io/jjasonek/configserver:s13
docker image push docker.io/jjasonek/eurekaserver:s13
docker image push docker.io/jjasonek/gatewayserver:s13

### Run docker compose:
docker-compose up -d

