# WCF-Learnings

## What is WCF? Why is it?
WCF stands for Windows Communication Foundation.

#### Before WCF:
webservices and dot net remoting are different technologies and having complete different programming models. we have so many technologies like this for communication.

So to implement this we have to learn each language to communicate with different application and to get different protocols and behaviors.

#### With WCF
WCF will unify and bring all these communication technologies under one roof. 
Microsoft has come up with a single programming model that is called as WCF- Windows Communication Foundation.
In WCF service we implement one service and we can configure as many end points as want to support all the client needs. 

let's say we have 2 clients then we have to configure 2 end points, if 4 clients then end points are 4, if 5 clients, endponts 5 like that WCF service is solved the problem of previous communication technologies by making them in one roof.

## What is the core to WCF service? 
System.Servicemodel assembly is core of the WCF service. WSDL (Web service description language) document will provide the Meta data information of the service.

## What is abc in WCF?
abc is stand for adress, binding and contract which represents (where how what)
* adress is to set the url where the service is located.
* binding is to set what the protocol is to be used to communicate with the service
* Contract is to set what service need to communicate with this address and binding
What ever the configuration we want to set that needs to be written within the <ServiceModel> </ServiceModel>

## What is distributed application?
Distributed application is an application where the parts of it run on 2 or more computer nodes. distributed applications are also called as connected systems.

## What is InterOperable appplication?
An application that can communicate with any other application that is built on any platform is called as interoperable application.

Webservices can communicate with any application built on any platform, where as  a .net remote service can be consumed only by another .net application. So webservices are interoperable, where as .net remoting services are not..

## What is Scalability?
Scalability means as the number of users increase we dont want the performance to degrade so making the application by dividing into different tiers and deploying them in different machines we can acheive the scalability

## Why web services are interoperable?
Web services uses open protocols and Message formats, it uses Html Protocols and xml Message formats
Any application built on any platform can understand these protocols and open standerds so web services are interoperable

* XML over Http Offers interoperability
* Binary over TCP offers better performance

## Is Webservice and WCF service is different?
Basic and primary difference is, ASP.NET web service is designed to exchange SOAP messages over HTTP only while WCF Service can exchange message using any format (SOAP is default) over any transport protocol i.e. HTTP, TCP, MSMQ or NamedPipes etc. Web Service is based on SOAP and return data in XML form

## Why would someone breakdown the application into different tiers and why would they deploy into different machines?
that is just to improve the scalability of the application

## How do you make changes in WCF Service whithout breaking clients??

Just use Name attribute with the service contract
```javascript
// Original one
[ServiceContract]
public interface IHelloService
{
}

/* And you all set the configuaration in App.config file like contract="HelloService.IHelloService"
and debug look at WSDL document. In WSDl search for the portType
<wsdl: portType name="IHelloService">

Once we change the interface name as below */

[ServiceContract]
public interface IHelloServiceChanged
{
}

/* In The WSDL Document protoType will be <wsdl: portType name="IHelloServiceChanged">
To prevent this breaking change we have to set the name property to previously used interface name like below */

[ServiceContract(Name="IHelloService")]
public interface IHelloServiceChanged
{
}

/* Now In The WSDL doc protoType will be 
<wsdl: portType name="IHelloService">
Solved.

Similarly we can also use with operation contract. */
```
