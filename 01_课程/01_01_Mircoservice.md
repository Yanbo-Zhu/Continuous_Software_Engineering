

# 1 Design Principles and Architectural Patterns

Design principles are high-level, abstract guidelines that can help give structure to software.

They provide general rules and best practices, e.g.:
▪ Separation of Concerns
▪ Encapsulation
▪ Explicit Dependencies
▪ Loose Coupling
▪ Persistence Ignorance
▪ Bounded contexts; Programmatic Interfaces


An architectural pattern is a set of architectural design decisions that are applicable to a recurring design problem, and parameterized to account for different software development contexts in which that problem appears.

Specific, reusable solutions or proven ”templates”
e.g.:
• Model-view-controller (MVC) Pattern
• Command Query Responsibility Segregation (CQRS) Pattern
• Circuit Breaker Pattern

# 2 Microservice Architecture

In short, the microservice architectural style is an approach to developing a single application as a suite of small [focused] services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API.

These services are built around business capabilities and are independently deployable by fully automated deployment machinery. 


There is a bare minimum of centralized management of these services, which may be written in different programming languages and use different data storage technologies.”

Characteristics of Microservices [Fowler]
1. Componentization via Services
2. Organized around Business Capabilities
3. Products not Projects
4. Smart endpoints and dumb pipes
5. Decentralized Governance
6. Decentralized Data Management
7. Infrastructure Automation
8. Design for failure
9. Evolutionary Design



# 3 Microservice Design Patterns: Data Management Patterns


Data Management Patterns
• Shared Database
• Database per Service
• API Composer
• CQRS


## 3.1 Pattern: Shared Database


to meet the characteristic : Decentralized Data Management 

![](image/Pasted%20image%2020241109144120.png)

![](image/Pasted%20image%2020241109144320.png)

## 3.2 Pattern: API Composer

How can we query and retrieve data from across multiple microservices?

![](image/Pasted%20image%2020241109144403.png)



## 3.3 Pattern: Command Query Responsibility Segregation (CQRS)


![](image/Pasted%20image%2020241109144422.png)


若干个 service 总调用同一个 service 

左边的每个小黄blocks 去满足  不同的 query needs , 上面的小球 代表 command interface

邮编的 block 上面的小球 是function in API

# 4 Inter-service Communication Patterns

Inter-service Communication Patterns
• Synchronous Communication
• Asynchronous Communication
• Messaging
• Client-side Service Discovery
• Server-side Service Discovery

![](image/Pasted%20image%2020241109144558.png)


---


![](image/Pasted%20image%2020241109144609.png)



Pattern: Client-side Service Discovery
![](image/Pasted%20image%2020241109144713.png)


Pattern: Server-side Service Discovery
![](image/Pasted%20image%2020241109144724.png)

![](image/Pasted%20image%2020241109144756.png)


