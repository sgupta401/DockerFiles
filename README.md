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
   ```
   Above command build the images from two docker files
   1. OIDC Server: https://github.com/sgupta401/DockerFiles/blob/main/Dockerfile.OIDC
   2. s3-object-browser: https://github.com/sgupta401/DockerFiles/blob/main/Dockerfile.s3

   Both docker files are based on eclipse-temurin:17-jdk base image, and pull the code from the git hub repositories. THe jars are then built using maven and the containers are started on ports
   1. s3-object-browser: 8080
   2. oidc server: 9000
   
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

## Sample Response and screenshot
1. `/object_metadata/file1.txt`
```bash
   {
     "objectName": "file1.txt",
     "loggedInUser": "sgupta1",
     "versionId": "9A7kFIDydBjhoTlyu34MY3GOrJ_rKjWZ",
     "serverSideEncryption": "AES256",
     "lastModifiedDate": "2024-09-27T11:02:18Z"
   }

```
2. `/health`
```bash
{
  "status": "UP",
  "components": {
    "db": {
      "status": "UP",
      "details": {
        "database": "H2",
        "validationQuery": "isValid()"
      }
    },
    "diskSpace": {
      "status": "UP",
      "details": {
        "total": 245107195904,
        "free": 63301312512,
        "threshold": 10485760,
        "path": "/Users/siddharthgupta/Siddharth/intuit/s3-object-browser/.",
        "exists": true
      }
    },
    "ping": {
      "status": "UP"
    },
    "s3": {
      "status": "UP",
      "details": {
        "buckets": 1
      }
    }
  }
}
```
3. `/audit_log`
```bash
{
  "audits": [
    {
      "id": 1952,
      "fileName": "file1.txt",
      "accessBy": "sgupta1",
      "accessTime": "2024-09-29T11:20:07.266370Z"
    },
    {
      "id": 1953,
      "fileName": "file1.txt",
      "accessBy": "sgupta2",
      "accessTime": "2024-09-29T11:20:29.555149Z"
    },
    {
      "id": 2002,
      "fileName": "file1.txt",
      "accessBy": "sgupta3",
      "accessTime": "2024-09-29T11:22:19.892096Z"
    },
    {
      "id": 2052,
      "fileName": "file1.txt",
      "accessBy": "sgupta1",
      "accessTime": "2024-09-29T12:17:50.432943Z"
    }
  ],
  "loggedInUser": "sgupta1"
}

```
## Test Screenshots
<img width="400" alt="image" src="https://github.com/user-attachments/assets/c986bb68-0cdc-4c8e-b379-3e169b8cb8ba">

<img width="400" alt="image" src="https://github.com/user-attachments/assets/0bb64fcd-148e-45f4-be0c-e8e0c2e4fdb1">

## Test Data 
### Users 
    -     sgupta1/password
    -     sgupta2/password
    -     sgupta3/password
### Files 
    -     file1.txt (http://localhost:8080/object_metadata/file1.txt) 
    -     file2.txt (http://localhost:8080/object_metadata/file2.txt)
    -     file3.txt (http://localhost:8080/object_metadata/file3.txt)

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

   
