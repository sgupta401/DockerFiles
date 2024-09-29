## How to run the applications Using Docker 

**System requirement**
1. Docker (Tested on Version - 27.1.1, build 6312585)
2. Docker Compose (Already installed in Docker desktop is installed) (Tested on version v2.29.1-desktop.1)  

## Steps

1. **Start Docker Desktop.**

   ![Docker Desktop](https://github.com/user-attachments/assets/786b4f2f-b859-4ce2-b12f-128f19c8f02d)

2. **Run the following command:**
   ```bash
   docker-compose up
3. **Two Docker containers will be started:**
   - **Container 1:** Runs the `s3-object-browser` Spring Boot app, which can be accessed at [http://localhost:8080/](http://localhost:8080/).
   - **Container 2:** Runs the `oidc-server` Spring Boot app, which can be accessed at [http://localhost:9000/](http://localhost:9000/).

## How to test the application 
### /object_metadata/file1.txt endpoint
1. Enter the url http://localhost:8080/object_metadata/file1.txt in browser
2. Page will be redirected to http://localhost:9000/oauth2/authorization endpoint
3. Enter test user credentials
    -     sgupta1/password
    -     sgupta2/password
    -     sgupta3/password
4. Click submit button
5. Page will be redirected to consent page. Accept consent and click submit button
6. Page will be redirected to http://localhost:8080/object_metadata/file1.txt with file1.txt metadata

### /audit_log endpoint
1. Enter url http://localhost:8080/audit_log in browser
2. If user is logged in, then audit details will be shown to user
3. If user is not logged in then page will be redirected to login page
4. Enter test user credentials given above and continue

### /health endpoint
1. Enter url http://localhost:8080/health in browser
2. If user is logged in, then audit details will be shown to user
3. If user is not logged in then page will be redirected to login page
4. Enter test user credentials given above and continue



## Running the application on IntelliJ
1. Clone OIDC Server repository
   ```bash
   git clone https://github.com/sgupta401/OIDC-Server.git
2. Clone s3-object-browser repository
   ```bash
   git clone https://github.com/sgupta401/s3-object-browser.git
3. Import both projects in IntelliJ as maven projects
4. Start OIDC server by running `com.intuit.oidc.Application` class

   <img width="400" alt="image" src="https://github.com/user-attachments/assets/f8161b1e-1f79-406f-81b2-003bd8b566fd">

5. Start s3-object-browser by running `com.intuit.S3ObjectBrowserApplication` class

   <img width="400" alt="image" src="https://github.com/user-attachments/assets/1276cf18-7a23-4d78-9629-e0ff20e382e7">

   
