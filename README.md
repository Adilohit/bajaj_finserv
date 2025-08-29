# bajaj_finserv
# Spring Boot Webhook Auto Submitter

This is a Spring Boot application that automatically interacts with a webhook endpoint, generates a webhook URL, and submits the final SQL solution.

---

##  Project Structure

```
Spring-boot-webhook-auto-submitter/
├── pom.xml
├── src/
│   ├── main/
│   │   ├── java/com/example/webhook/
│   │   │   ├── WebhookAutoSubmitterApplication.java
│   │   │   ├── AppProperties.java
│   │   │   ├── WebhookClient.java
│   │   │   ├── dto/
│   │   │   │   ├── GenerateWebhookResponse.java
│   │   │   │   ├── SolutionRequest.java
│   │   │   ├── StartupRunner.java
│   │   └── resources/
│   │       ├── application.yml
│   │       ├── solution.sql
│   │       ├── solution-final.sql (generated)
```

---

##  Configuration

Update the following values in `src/main/resources/application.yml`:

```yaml
app:
  user:
    name: "Your Name"
    regNo: "Your Registration Number"
    email: "Your Email"
```

---

##  Build and Run

### 1. Build the project
```bash
mvn -DskipTests clean package
```

### 2. Run the application
```bash
java -jar target/spring-boot-webhook-auto-submitter-0.0.1-SNAPSHOT.jar
```

---

##  How it Works

1. On startup, the app sends a POST request to `generateWebhook/JAVA` with your name, regNo, and email.
2. It receives a response containing:
   - **webhook URL**
   - **access token**
3. The app reads your SQL query from `solution.sql` and writes it into `solution-final.sql`.
4. It then sends `{ "finalQuery": "<SQL query>" }` to the returned webhook URL with authorization.

---

##  Files to Check

- `pom.xml` → Maven dependencies and build config.
- `application.yml` → Your details (update before running).
- `solution.sql` → Contains your SQL query (input).
- `solution-final.sql` → Generated file containing the final query (output).
- `WebhookClient.java` → Handles all HTTP requests.
- `StartupRunner.java` → Runs workflow after app startup.

---

##  Example Output

When the app runs successfully, you should see logs like:

```
Generated webhook: https://<some-webhook-url>
Access token: <token>
Final solution submitted successfully!
```
