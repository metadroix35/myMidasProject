
# Forage Midas Core Banking Simulation

This project is a Spring Boot–based microservice application built as part of the **JPMorgan Chase Software Engineering Virtual Internship on Forage**. It simulates a simplified banking system with the ability to produce and consume Kafka events, query and update user balances, handle incentives, and process transactions. User data is pre-populated, transactions are streamed through Kafka, and balances are updated in real time, accessible through REST endpoints. The application demonstrates backend development with Java 17, Spring Boot, Maven, JUnit, and Apache Kafka, following modular and industry-relevant engineering practices.

## Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/<metadroix35>/forage-midas.git
cd forage-midas
````

### 2. Build the project

```bash
mvn clean install
```

### 3. Run the Spring Boot application

```bash
mvn spring-boot:run
```

### 4. Start Kafka locally (if not already running)

```bash
# Start Zookeeper
bin/zookeeper-server-start.sh config/zookeeper.properties

# Start Kafka broker
bin/kafka-server-start.sh config/server.properties
```

---

##  Configuration

Edit `src/main/resources/application.yml`:

```yaml
server:
  port: 33400

general:
  incentive-api-url: http://localhost:33401/incentive
```

---

##  API Endpoints

### Get Balance

**Request:**

```
GET /balance?userId={id}
```

**Example:**

```
GET http://localhost:33400/balance?userId=1
```

**Response:**

```json
{
  "amount": 2500.0
}
```

### Get Incentive

**Request:**

```
GET /incentive?userId={id}
```

**Response:**

```json
{
  "amount": 150.0
}
```

---

##  Running Tests

Run all JUnit test cases:

```bash
mvn test
```

The `TaskFiveTests` will:

* Populate users
* Send Kafka transactions
* Query balances
* Print results in the logs

---

##  Project Structure

```
src/
 ├─ main/
 │   ├─ java/com/jpmc/midascore/
 │   │   ├─ controller/       # REST controllers
 │   │   ├─ component/        # BalanceQuerier, IncentiveQuerier, FileLoader, etc.
 │   │   ├─ kafka/            # Kafka producer/consumer
 │   │   ├─ foundation/       # Domain models (Balance, Transaction, etc.)
 │   │   └─ MidasCoreApplication.java
 │   └─ resources/
 │       └─ application.yml   # Config
 └─ test/
     └─ java/com/jpmc/midascore/
         └─ TaskFiveTests.java
```

---

##  Sample Output (from TaskFiveTests)

```
---begin output ---
Balance {amount=5000.0}
Balance {amount=4200.0}
Balance {amount=3100.0}
...
---end output ---
```

---

##  Acknowledgements

This project was developed as part of the
**JPMorgan Chase Software Engineering Virtual Experience** on Forage.

---

##  Author

metadroix35

---

##  Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

---

##  License

This project is licensed under the **MIT License**.


