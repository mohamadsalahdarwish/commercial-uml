# Commercial License Issue Design Document
This Document lays out the design and necessary touch points that represent the current architecture for commercial license issuing.

## C4model
The Commercial License Issuing is an electronic service that is provided by Balady portal to ease the procedure of issue/renewal of a commercial license for the beneficiary for all economic Activities according to the national classification for the economic activities.

Apigee is used to integrate the Service with several external services, such as the Ministry of Commerce and the Ministry of Justice, and many internal services. This provides a centralized solution for accessing these services and provides a fully integrated solution for the beneficiary. Additionally, the reusable components provided by the Service can be used with other modules.

## Level 1: System Context
The diagram shows the commercial license API as a box in the center, surrounded by its user (Beneficiary) and the other systems (internal, external components) that interact with it.
This system helps beneficiaries issue or renew commercial licenses. It also provides a set of user interfaces for internal Baladi employees to complete the necessary approvals for granting commercial licenses.                                                                 
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/context/commercial-contex-diagram.puml)

### The diagram shows that: 
-	The Beneficiary is the main actor who uses the commercial license API via the web browser.
-	The web portal that calls the commercial license Api via http requests for serving the functionality for acquiring a license for business.
-	The commercial license Api uses the common module as auxiliary service for integrating with several internal (Balady services) and external functionality to get several functionalities.
-	The commercial license Api uses internal services (reusable components) to provide auxiliary functionality.


## Level 2: Containers
The container diagram shows the containers that integrate with commercial license Api for generating a commercial license for several economical
activities and the below diagram shows the full picture of the containers and how they interact with each other.
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_ALL.puml)

### Commercial License Internal Services

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_1.puml)

#### This diagram shows that:
- The user accesses MVC application that provides a single page application user interface for generating commercial license.
- The MVC page uses http to call commercial license Api (CLA) service for providing the functionality of generating the commercial license.
- The CLA calls via http Balady App Calculator service to calculate the cost for generating the fees cost based on the provided action like
  generating commercial licenses, commercial license correction fees, vehicle route calculator.
- The CLA calls board contract service via http to retrieve board contract owned by beneficiary and it integrates with board contract
  configuration for any configuration related to the board like zone settings for board.
- The CLA calls commercial QR service via http to grant or validate or cancel QR code which is used to get all the business details like shop size,
  number of windows, etc.
- The CLA calls Commercial Issuing Consultation service via http to simulate the same procedure to produce a license without any fees to have
  an understanding about limitation.
- The CLA calls Craft service via http for granting craft license and validate crafts for commercial license.
- The CLA calls Engineering Office Api via http to get the business partner engineering office for Beneficiary granting commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_2.puml)

#### This diagram shows that: -
- The user accesses MVC page that provides a single page application user interface for generating commercial license.
- The MVC page uses http to call commercial license Api (CLA) service for providing the functionality of generating the commercial license.
- The CLA calls GIS service via http to get GIS location details by coordinates and information about zones.
- The CLA calls Commercial parking zone service via http to handles all tasks related to parking zones for vehicles like retrieval, validation, etc.
- The CLA calls SSO service via http to get Single sign-on functionality that handles authentication and authorization.
- The CLA calls Etmam Intg service via http to validate and acquire orders for balady service and get Order Details.
- The CLA calls Self Survey Api service via http to get more information about the license rating.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_3.puml)

#### The diagram shows that: -
- The user accesses MVC page that provides a single page application user interface for generating commercial license.
- The MVC page uses http to call commercial license Api (CLA) service for providing the functionality of generating the commercial license.
- The CLA calls Health Certificate Service via http to check if the beneficiary has a health certificate.
-
- The CLA calls Blocked Clients Api service via http to validate If the client is blocked in the municipality for the provided service.
- The CLA calls Balady Services API service via http to validate and retrieve commercial records for commissioner.
- The CLA calls Activity Management Api via http to manage the activities related to granting commercial license (validate activities related to
  Salama report and meeting civil defense rules).
- The CLA calls Governmental Service Bus (GSB) service that is accessed via http centralized access called Apigee which is a service that Managing
  high value/volume of APIs with enterprise-grade security and dev engagement and it’s mainly about integrating with governmental parties.
- The CLA calls General Security service via http to get approvals related to general security.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_common.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_integration.puml)

**This diagrams shows that:**
 - The CLA uses the common Api container for generating common functionality as an auxiliary function. 
 - The CLA integrate with several governmental institution via http even by using common service or directly by itself. 
 - Ministry of Municipal and Rural Affairs and Housing
    - A Service that gets information about Ejar Contracts and their Status. 
 - Ministry Of Commerce
   - Get Information about commercial records 
   - Get Information about applicant relation to commercial record.
   - Information about blocked families. 
 - Balady Investment Contract 
   - Get information about investment electronic contracts.
- Classification Pega 
  - Get Information About activities and Its classifications and special Activities that Require Special handling Like Furniture. 
- Ministry Of Labor 
  - Get Labor Info Related to Employee.
- Salama 
  - Integrate with civil Defense to buy and construct Salama tools and get Salama report number. 
- Balady Bills Service 
  - Grant/Cancel special permission for business opening in crisis (Corona). 
- Ministry of Justice 
  - Get information about deeds. 
- National Information Center (Tawakkalna)
  - Get information about citizens. 
-Moj API 
  - Provide Apis for integration with Ministry of Justice.

## Level 3: Component
The container diagram shows the components that make the commercial API container, which is the core service for generating commercial licenses.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-activity.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-approval.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-automate-expire-cancel.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-back-office.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-board.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-business-rules.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-calculator.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-common.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-correct.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-craft.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-credence-request.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-efada.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-grouped-request-renewal.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-integration.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-license.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-license-rating.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-lookup.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-migration.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-mobile-cancel.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-modify-request.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-momathel.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-new-request.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-nic.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-old-license-controller.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-precautionary-compliance.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-provider-observation.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-qr-code.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-renew.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-repeated.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-request.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-saudi-business-center.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-self-service.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-vehicle.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-expired.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-on-bill-fee.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-on-hold.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-on-not-belong.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-on-not-license-transfered.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-revoked.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-24-permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-hosue-hold-permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-non-food-permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-royal-gaurd_permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-seasonal_permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-self-service-permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-side-walk-permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-slaughter-permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-tobaco-permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-transfer_permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-transport_permit.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-vheicle-parking_permit.puml)
