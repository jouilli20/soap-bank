# soap-bank (Spring Boot + Spring-WS)

## Build & Run
```bash
mvn clean package
mvn spring-boot:run
```

## WSDL
Open:
http://localhost:8080/ws/bank.wsdl

## Postman tests
- Method: POST
- URL: http://localhost:8080/ws
- Header: Content-Type: text/xml; charset=utf-8
- Body: raw (XML)

### GetAccount
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:ban="http://example.com/bank">
  <soapenv:Header/>
  <soapenv:Body>
    <ban:GetAccountRequest>
      <ban:accountId>A100</ban:accountId>
    </ban:GetAccountRequest>
  </soapenv:Body>
</soapenv:Envelope>
```

### Deposit
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:ban="http://example.com/bank">
  <soapenv:Header/>
  <soapenv:Body>
    <ban:DepositRequest>
      <ban:accountId>A100</ban:accountId>
      <ban:amount>20.00</ban:amount>
    </ban:DepositRequest>
  </soapenv:Body>
</soapenv:Envelope>
```

### Fault (amount <= 0)
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:ban="http://example.com/bank">
  <soapenv:Header/>
  <soapenv:Body>
    <ban:DepositRequest>
      <ban:accountId>A100</ban:accountId>
      <ban:amount>-5</ban:amount>
    </ban:DepositRequest>
  </soapenv:Body>
</soapenv:Envelope>
```
## Analyse du contrat
- XSD: src/main/resources/bank.xsd
- Namespace (WSDL): ...
- Operations (portType): GetAccount, Deposit, Withdraw
- Endpoint: http://localhost:8080/ws
- WSDL: http://localhost:8080/ws/bank.wsdl

## Fonctionnalité ajoutée
- Operation ajoutée: Withdraw (retrait)

## Fichiers modifiés
- src/main/resources/bank.xsd
- ...Endpoint.java
- (éventuellement) ...Service.java

## Tests Postman
- GetAccount A100: OK (capture)
- Deposit A100 20.00: OK (capture)
- Fault (amount <= 0 ou compte inexistant): OK (capture)
- Withdraw nominal: OK (capture)
- Withdraw Fault (solde insuffisant): OK (capture)
