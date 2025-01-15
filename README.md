# Custom Newsfeed Application

## Overview
**Custom Newsfeed Application** is a web-based application designed to serve the user relevant, up to date news based on his country which he signed up with. It features user account management, a seamless experience, and an admin-account-only page with extra functionalities, such as deactivating or deleting users.
The project is divided into two main components:
- **Frontend**: Built using Angular.
- **Backend**: Developed with Java 17, with a MySQL database for data storage.

---

## Requirements
To run this application,after pulling both repositories, you will need the following installed on your system:

### Backend Requirements
- **Java 17**  
  Ensure Java 17 is installed and properly set up. Verify installation:
  ```
  java -version
  ```
-MySQL
A running MySQL server is required. Create a database and configure the connection in the backend project.
Use your connection string, username and password for mySQL on the application-test.properties file ( or application.properties, if you disable the spring.rpfoiles.active = test line )
- **IMPORTANT!!**
there's a commented out line on application-test properties: 
```
#spring.sql.init.mode=always
#spring.sql.init.data-locations=classpath:sql/countries.sql,classpath:sql/countries.sql
```
make sure to uncomment it when you first run spring so that it will create the countries database and then comment it again!

- **IMPORTANT!!**
for security reasons, you need to manually add a user with role = ADMIN in the database. However since there's password encoding aswell this is cumbersome.
An easy and fast way to do this is to go to:
```
service/UseService
```
on the very first method, saveUser() there is a commented line:
```
//            user.setRole(Role.ADMIN);
```
just uncomment it, run the app, and the very next user that is created in the database through the REST server will be an ADMIN account!
**REMEMBER** to comment it out again unless you want everyone to have admin rights.

- **Swagger docs for REST server**
```http://localhost:8080/swagger-ui/index.html```
- finally:
```
./gradlew bootRun
```
### Frontend Requirements
-Node.js
Install the latest stable version of Node.js, which includes npm (Node Package Manager).
Verify installation:
```
node -v
npm -v
```
-Angular CLI
Install Angular CLI globally:
```
npm install -g @angular/cli
```
Make sure angular will run on http://localhost:4200 , otherwise you may have to modify the java cors file. ( corsConfigurationSource() on security/SecurityConfig file, cors.Configuration.setAllowedOrigins )

- Frontend thankfully is easier. all you need after cloning frontend is to install dependencies :

```
npm install
```
- and then start the server:
```
ng serve
```

### **App Features**
- REST provides authorization through login and authentication through checking user roles. Same goes through the frontend as there are authorization interceptors to handle user access and admin access to pages.
- Password Encoding in the database. Nobody may see other people's password, not even the database user.
- JWT based authentication for everything. Tokens last 3 hours, but its very easy to configure that amount of time,based on the developer's preference! (JwtService)
- This is evident through the swagger docs, but there are all the expected CRUD operations for such an application. Some require admin rights and some require simple authentication, or either. REST backend may be used as basis for other similar applications and was designed with that in mind.
- Users get a seamless and modern experience, never seeing an error page. The frontend client handles are non-authorized requests gracefully.
- The application incorporates https://newsapi.org/ to provide the custom-made news feed for the User, so that they can stay informed with up-to-date, localized news effortlessly. it is configured so that it will serve news from today and yesterday and bases it on the user's country, as set in his account. If you use it, it is better that you get your own key from them rather than the one i provided.
- Validations on the backend, validations on the frontend.Using the power of regex we require strong passwords and valid emails! We also make sure,by checking with our database, that the User may not enter an invalid Country name.
- When a user is trying to enter some invalid value the frontend informs them in a user-friendly way what needs fixing!

### **Contributing**
- Feel free to fork this repository and submit pull requests. Contributions are welcome!
