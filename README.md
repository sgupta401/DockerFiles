## How to run the applications

**System requirement**
1. Docker (Version - 27.1.1, build 6312585)
2. Docker Compose (Already installed in Docker desktop is installed) (version v2.29.1-desktop.1)  

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

   
