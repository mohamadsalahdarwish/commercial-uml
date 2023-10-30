# Commercial License Issue Design Document
This Document lays out the design and necessary touch points that represent the current architecture for commercial license issuing.

## C4model
The Commercial License Issuing is an electronic service that is provided by Balady portal to ease the procedure of issue/renewal of a commercial license for the beneficiary for all economic Activities according to the national classification for the economic activities.

Apigee is used to integrate the Service with several external services, such as the Ministry of Commerce and the Ministry of Justice, and many internal services. This provides a centralized solution for accessing these services and provides a fully integrated solution for the beneficiary. Additionally, the reusable components provided by the Service can be used with other modules.

## Level 1: System Context
The diagram shows the commercial license API as a box in the center, surrounded by its user (Beneficiary) and the other systems (internal, external components) that interact with it.
This system helps beneficiaries issue or renew commercial licenses. It also provides a set of user interfaces for internal Baladi employees to complete the necessary approvals for granting commercial licenses.                                                                                
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/context/commercial-contex-diagram.puml)

The diagram shows that: 
-	The Beneficiary is the main actor who uses the commercial license API via the web browser.
-	The web portal that calls the commercial license Api via http requests for serving the functionality for acquiring a license for business.
-	The commercial license Api uses the common module as auxiliary service for integrating with several internal (Balady services) and external functionality to get several functionalities.
-	The commercial license Api uses internal services (reusable components) to provide auxiliary functionality.



