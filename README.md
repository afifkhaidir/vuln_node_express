# Vulnerable Node Express

This is a vulnerable Node Express service meant to be used as a target for security testing tools.

## Build and Run

### Install NPM Dependencies
```shell script
npm install
```

### Initialize SQLite DB
```shell
node bootstrapdb.js
```

### Run
```shell script
DEBUG=myapp:* npm start
```

## Build and Run with Docker

### Build Docker Image
```shell script
docker build --tag stackhawk/nodeexpressvulny .
```

### Run Docker Container
```shell script
docker run --rm --publish 3000:3000 --name nodeexpressvulny stackhawk/nodeexpressvulny
```

### Build and Run in Docker Compose
```shell script
docker-compose up --build --detach
```

## Known Vulnerabilities
* SQL Injection via search box. - `item%' union all select * from user; -- ` 
* Cross Site Scripting via search box. - `<script>alert("hey guy");</script>`

## Key Takeaways
### 3 Types of Security Testing

1. SCA (SW Composition Analysis)
example: dependabot, snyk, FOSSA
  - operates on static code
  - scanning vuln on library/modules used by SW
  - fast
2. SAST (Static Application Security Testing)
example: CodeQL, sonarqube, checkmarx
  - operates on static code
  - scanning vuln by pattern on codebase
  - high false positives
  - slow
3. DAST (Dynamic Application Security Testing)
example: StackHawk, OWASP ZAP, burp suite
  - Operates on running code
  - Reports on suspected vuln
  - Slow
