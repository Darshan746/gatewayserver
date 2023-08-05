OAuth2 is delegated authorization framework which supports multiple use cases addressing different device capabilities

It supports Server-to-Server apps, browser based apps, mobile/native apps, IOT devices and console/Tv's


OAuth2 has various authorization grant flows like "Authorization code grant", "Client credential grant type"


Separtion of Auth logic
----------------------

	inside OAuth2, we have a Authorization server which recieves the request from the client for access token and issue them upon successfull authentication 
	
	this enable to maintain all the security logic in a single place , Regardless of on How many applications that the organization has, They all connect to Auth server to perform the login 
	operation
	
	
	
		All the user credentials and client application credentials will be maintained in the single location which is inside Auth server




No Need to share credentials
----------------------------

	If you plan to allow 3rd party applications and services to access your resources then there is no need to share your credentials


OAuth2 client credential flows
------------------------------
wheneve external system trying to communicate with the spring-cloud gateway where there is no enduser involved then we need to use the OAuth2 client  credentialgrant flow for authentication
and authorization



		for example to understand 
		
			here we will be having 3 components 
				1] External client application
				2] Resource server [wherever the resources to be protected then we call that as Resource server in OAuth2 framework] here in our example it is Spring-cloud-gateway which 
				     is entry point to the our microservice application
					 
			    3] Authorization server (KeyCloak)==> there are many authorization server are there like Okta, fusion Auth , since keycloak is open source we used here
				    
					
					
		1] first External clienta application trying to invoke /eazybank/accounts/sayHello
		
		2] gatewayserver/Resource server replies that "sorry buddy I can oly process the request who provides a access token from auth server , go and get access token from Auth server"
		
		3] Then external Application client asked keycloak which is Auth server for access token
		
		4] Auth server laughed and replied, I can't given access token just like that , In order to get access token from me, you need to register with me and same need to be approved by 
		   my admin
		   
		5] Then the external client application went to admin of the keycloak server and register as a valid client once the registration process is completed my keycloak admin has given 
		     a client id and client secret  to my external client application , So that same client id and client secret has to be used by client application whenever get the access token from the 
			 keycloak auth server
			 
		6] Now the External client asked keycloak which is Auth server for access token , but this time , It passed the client-Id and client-secret  which it recieved during the 
		     registration process that it did offline with the admin of the Auth server
			 
	    7] Auth server replied "congratulations buddy your details are correct ", here is your access token . All the best
			 
		8] Now  External clienta application trying to invoke /eazybank/accounts/sayHello with the access token that it recieved during the step 7 
		
		9] Now once the gateway recieved the access token from the external client , the gatew will send that access token to authorization server to validate the token
		
		10] Auth server will validate and respond back weather the token is valid or not 
		
		
		
		
		docker run -p 7080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:18.0.0 strat-dev
		
		
		Realm is a concept such as where you can maintain all your users claim credentials , which is specific to a group or which is specific to your environment 
		
		
		
		Path to access the client credential API on opencloak issue the below rest endpoint 
		
			localhost:7080/realms/master/.well-known/openid-configuration
		
		
		
	 from the above endpoint you would get the list of endpoints from their you copy the endpoint to get the access token 
	 
	  http://localhost:7080/realms/master/protocol/openid-connect/token
	  
	   and in the postman in Header section give the below key value pair
	   
	   
			client_id  --> id which is registered in the auth server
			client_secret ---> secret which you got from auth server during the registration
			scope----> openid-----> openid is a wrapper for OAuth2 which gives the basic info about the token like this token belong to the which user and client like that
									(we can understand what is the basic details of the client application or the enduser to whom this access token belongs
			grant_type ---> client_credentials ---> since we are doing api- to- api communication
	End of Client_credential code flow



Authorization_Code_flow
========================




