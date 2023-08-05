What are the micro services involed here

  1] Config-server
  2] Eureka-server
  3] gateway-server(Spring-cloud-gateway)
  4] Account
  5] cards
  6] loans
  7] microservices-config


order of micro services we have to start as mentioned above


for related to Zipkin and cloakAuth server we have to downlaod the application and run through Docker

docker run -p 7080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:18.0.0 start-dev


