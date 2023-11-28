# Commercial License Issue Design Document
This Document lays out the design and necessary touch points that represent the current architecture for commercial license issuing.

## Swimlane Diagram
![commercial_license_issuing.png](src%2Fc4%2Fswimlane%2Fcommercial_license_issuing.png)

## C4model
The Commercial License Issuing is an electronic service that is provided by Balady portal to ease the procedure of issue/renewal of a commercial license for the beneficiary for all economic Activities according to the national classification for the economic activities.

Apigee is used to integrate the Service with several external services, such as the Ministry of Commerce and the Ministry of Justice, and many internal services. This provides a centralized solution for accessing these services and provides a fully integrated solution for the beneficiary. Additionally, the reusable components provided by the Service can be used with other modules.

## Level 1: System Context
The diagram shows the commercial license API as a box in the center, surrounded by its user (Beneficiary) and the other systems (internal, external components) that interact with it.
This system helps beneficiaries issue or renew commercial licenses. It also provides a set of user interfaces for internal Baladi employees to complete the necessary approvals for granting commercial licenses.                                                                 
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/context/commercial-contex-diagram.puml)

### The diagram shows that: 
-	The Beneficiary is the main actor who uses the commercial license API via the web browser.
-	The web portal that calls the commercial license Api requests for serving the functionality for acquiring a license for business.
-	The commercial license Api uses the common module as auxiliary service for integrating with several internal (Balady services) and external functionality to get several functionalities.
-	The commercial license Api uses internal services (reusable components) to provide auxiliary functionality.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/context/commercial-contex-diagram-employee-internal.puml)

### The diagram shows that:
-	Balady employee is the main actor who uses the oracle ADF via the web browser(internal portal) to manage the employee approvals.
-   The oracle ADF calls the policy server to evaluate the policy for employee to map it to the right action. 
-	The oracle ADF updates the DB status based on employee action to track the employee approval process and track the next required actions then show it to the employee based on his/her role.
-	The commercial license Api tracks the database status related to the employee approval process to get the next required action after completing the employee approval process.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/context/commercial-contex-diagram-governmental-internal.puml)

### The diagram shows that:
-	Governmental employee is the main actor who uses the oracle ADF via the web browser(internal portal) to manage the governmental approvals.
-   The oracle ADF calls the policy server to evaluate the policy for governmental employee based to the governmental agency and municipality(tenant)to map it to the right action.
-	The oracle ADF updates the DB status based on governmental employee action to track the approvals process and track the next required actions.
-	The commercial license Api tracks the database status related to the governmental approval process to get the next required action after completing the governmental approval process.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/context/commercial-contex-diagram-civil-defense.puml)

### The diagram shows that:
-  The commercial license Api will need civil defense approval to grant a commercial license related to some activities.
-  In case of non-fawry commerical license civil defense will give feedback to the commercial license about the status of the current activity approval process status.

## Level 2: Containers
The container diagram shows the containers that integrate with commercial license Api for generating a commercial license for several economic
activities and the below diagram shows the full picture of the containers and how they interact with each other.
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_ALL.puml)

### Commercial License Internal Services

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_1.puml)

#### This diagram shows that:
- The user accesses MVC application that provides a single page application user interface for generating commercial license.
- The MVC page calls commercial license Api service for providing the functionality of generating the commercial license.
- The commercial license Api calls Balady App Calculator service to calculate the cost for generating the fees cost based on the provided action like
  generating commercial licenses, commercial license correction fees, vehicle route calculator.
- The commercial license Api calls board contract service to retrieve board contract owned by beneficiary and it integrates with board contract
  configuration for any configuration related to the board like zone settings for board.
- The commercial license Api calls commercial Quick Response  service to grant or validate or cancel Quick Response code which is used to get all the business details like shop size,
  number of windows, etc.
- The commercial license Api calls Commercial Issuing Consultation service to simulate the same procedure to produce a license without any fees to have
  an understanding about limitation.
- The commercial license Api calls Craft service for granting craft license and validate crafts permits for commercial license.
- The commercial license Api calls Engineering Office Api to get the business partner engineering office for Beneficiary granting commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_2.puml)

#### This diagram shows that: -
- The user accesses MVC page that provides a single page application user interface for generating commercial license.
- The MVC page uses http to call commercial license Api  service for providing the functionality of generating the commercial license.
- The commercial license Api calls GIS service to get GIS location details by coordinates and information about zones and this is done through a geo-reference, as the service depends on a locator to determine the coordinate for the issuing part.
- The commercial license Api calls Commercial parking zone service  to handle all tasks related to parking zones permits for commercial license of vehicles.
- The commercial license Api calls Etmam Intg service to validate and acquire orders for balady service and get Order Details.
- The commercial license Api calls Self Survey Api service  to get more information about the license rating.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_3.puml)

#### The diagram shows that: -
- The commercial license Api calls Activity Management Api to manage the activities related to granting commercial license (validate activities related to
  Salama report and meeting civil defense rules) , get all details related to activity like filtering by isic number, vehicle detailed activities, etc.
- The commercial license Api calls Blocked Clients Api service to validate If the client is blocked in the municipality for the provided service.
- The user accesses MVC page that provides a single page application user interface for generating commercial license.
- The MVC page uses http to call commercial license Api  service for providing the functionality of generating the commercial license.
- The commercial license Api calls Health Certificate Service to check if the beneficiary has a health certificate.
- The commercial license Api calls Governmental Service Bus (GSB) service that is accessed  centralized access called Apigee which is a service that Managing
  high value/volume of APIs with enterprise-grade security and dev engagement and it’s mainly about integrating with governmental parties.
- The commercial license Api calls General Security service(salama) to get approvals related to general security.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_common.puml)
![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/container/commercial-container-diagram_integration.puml)

**This diagrams shows that:**
 - The commercial license Api uses the common Api container for utilizing common functionality as an auxiliary function. 
 - The commercial license Api integrate with several governmental institution even by using common service or directly by itself. 
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

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-activity.puml)
#####  This diagram shows Component diagram for Managing Activities Related To Commercial License.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-approval.puml)
##### This diagram shows Component diagram for Managing General Security Approvals Related To Commercial License Request.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-automate-expire-cancel.puml)
##### This diagram shows Component diagram for managing commercial license request for automated expired license cancellation.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-back-office.puml)
##### This diagram shows Component diagram for Managing backoffice operation. 

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-board.puml)
##### This diagram shows Component diagram for managing owner contract for board purchased by etmam.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-business-rules.puml)
##### This diagram shows Component diagram for managing the business rules for extracting a commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-calculator.puml)
##### This diagram shows Component diagram for managing fees calculation for the Commercial License.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-common.puml)
##### This diagram shows Component diagram for applying common functionality like commercial license for housing , retrieving investment in municipalities.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-correct.puml)
##### This diagram shows Component diagram for correcting commercial request data.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-craft.puml)
##### This diagram shows Component diagram for Managing craft integration Related To Commercial License.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-credence-request.puml)
##### This diagram shows Component diagram for loading attachment for credence request approval.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-efada.puml)
##### This diagram shows Component diagram for managing request of type efada( medical certificate for Riyad).

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-grouped-request-renewal.puml)
##### This diagram shows Component diagram for managing license renewal for a group of owners.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-integration.puml)
##### This diagram shows Component diagram for integration with governmental sectors to get data for commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-license.puml)
##### This diagram shows Component diagram for managing license , group of owners license, engineering office observation.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-license-rating.puml)
##### This diagram shows Component diagram for  Managing License Rating.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-lookup.puml)
##### This diagram shows Component diagram for retrieving lookups for board types, worker types, accommodations types , salalma approved center list , cities, malls , districts,credences , vehicle types , self machine types.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-migration.puml)
##### This diagram shows Component diagram for migrating commercial license to another municipality.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-mobile-cancel.puml)
##### This diagram shows Component diagram for managing cancellation of commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-modify-request.puml)
##### This diagram shows Component diagram for managing modifying commercial license request

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-momathel.puml)
##### This diagram shows Component diagram for managing commercial license related to momathil.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-new-request.puml)
##### This diagram shows Component diagram for managing new commercial license request.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-nic.puml)
##### This diagram shows Component diagram for sending notification after bill cancellation.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-old-license-controller.puml)
##### This diagram shows Component diagram for managing Activities Related To old Commercial License.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-precautionary-compliance.puml)
##### This diagram shows Component diagram for managing all the violation that violate the precausionary compliance  done by individulas.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-provider-observation.puml)
##### This diagram shows Component diagram for managing all the observation of the engineering offices and all of its lifecycle for approval of commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-qr-code.puml)
##### This diagram shows Component diagram for managing Quick Response codes for scanning to get more information about the shop.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-renew.puml)
##### This diagram shows Component diagram for renewing commercial license including vehicle license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-repeated.puml)
##### This diagram shows Component diagram for retrieving licenses and delete repeated ones.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-request.puml)
##### This diagram shows Component diagram for managing all the commercial requests.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-saudi-business-center.puml)
##### This diagram shows Component diagram for exposing all the saudi business center data  like license activities , immediate activities, fees,license issuing, commercial license status,data, mall lists , clean electronic contracts,pest and furniture, homogenous activities.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-self-service.puml)
##### This diagram shows Component diagram for managing self machine, self machines types and retrieving machine usage.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/commercial-component-diagram-vehicle.puml)
##### This diagram shows Component diagram for managing all vehicle paths for municipality or district.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection.puml)
##### This diagram shows Component diagram for  creating and retrieving objection on a commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-expired.puml)
##### This diagram shows Component diagram for creating and retrieving permitted commercial types for expired objection.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-on-bill-fee.puml)
##### This diagram shows Component diagram for creating and retrieving objection on  commercial license bill fees.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-on-hold.puml)
##### This diagram shows Component diagram for creating and retrieving objection on a Suspended commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-on-not-belong.puml)
##### This diagram shows Component diagram for creating and retrieving objection on not belonging commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-on-not-license-transfered.puml)
##### This diagram shows Component diagram for creating and retrieving objection on not transferred commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/objections/commercial-component-diagram-objection-revoked.puml)
##### This diagram shows Component diagram for creating and retrieving objection on a cancelled commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-24-permit.puml)
##### This diagram shows Component diagram for granting and validating a 24 hours permits on a license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-hosue-hold-permit.puml)
##### This diagram shows Component diagram for granting and validating permits related to household.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-non-food-permit.puml)
##### This diagram shows Component diagram for granting and validating a nonfood vehicle permits on a license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-permit.puml)
##### This diagram shows Component diagram for managing Activities Permits Related To Commercial License.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-royal-gaurd_permit.puml)
##### This diagram shows Component diagram for granting and validating permits related to royal gaurd type.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-seasonal_permit.puml)
##### This diagram shows Component diagram for granting and validating permits related to seasonal type  for commercial license request.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-self-service-permit.puml)
##### This diagram shows Component diagram for granting and validating permits related to self-service machine.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-side-walk-permit.puml)
##### This diagram shows Component diagram for granting and validating a sidewalk permits type  on a commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-slaughter-permit.puml)
##### This diagram shows Component diagram for granting  slaughter permits on a commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-tobaco-permit.puml)
##### This diagram shows Component diagram for managing License Permits ,Cancelling Permits and Activities Permits Related To Commercial License For Tobacco.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-transfer_permit.puml)
##### This diagram shows Component diagram for granting and validating permits related to transfer of commercial license.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-transport_permit.puml)
##### This diagram shows Component diagram for granting and validating permits related to Transport.

![example-uml](http://www.plantuml.com/plantuml/proxy?cache=yes&src=https://raw.githubusercontent.com/mohamadsalahdarwish/commercial-uml/main/src/c4/component/permits/commercial-component-diagram-vheicle-parking_permit.puml)
##### This diagram shows Component diagram for granting and validating permits related to vehicle parking type.
