# Flight CLI Application

A command-line interface (CLI) client for interacting with the Flight Management API. This application performs HTTP GET requests to the server and provides an interactive menu for retrieving information about flights, airports, aircraft, and passengers.

## About This Project

I developed this Java CLI application as part of my DevOps midterm sprint project. It serves as a client interface for the Flight API, allowing users to query flight-related data through an intuitive command-line menu system.

## Features

The application provides four main query options:

1. **Airports by City** - View all airports located in each city
2. **Aircraft by Passenger** - See which aircraft types each passenger has flown
3. **Airports by Aircraft** - Display airports used by each aircraft type  
4. **Airports by Passenger** - Show all airports visited by each passenger

## System Requirements

- **Java 17** or higher
- **Maven 3.6+** for building the project
- Access to a running Flight API server (default: `http://localhost:8080`)

## Installation & Setup

### 1. Clone the Repository
```bash
git clone <repository-url>
cd cli-client
```

### 2. Build the Project
```bash
mvn clean package
```

### 3. Running the Application

**Run with default settings:**
```bash
java -cp target/flight-cli-0.0.1-SNAPSHOT.jar com.example.flightcli.FlightCliApplication
```

**Run with custom server URL:**
```bash
java -cp target/flight-cli-0.0.1-SNAPSHOT.jar com.example.flightcli.FlightCliApplication http://localhost:9090
```

## Usage

After launching the application, you'll see an interactive menu:

```
==== Flight Connections CLI ====
Type 1-4 to pick a question or q to quit.

1) Airports in each city
2) Aircraft flown by each passenger  
3) Airports used by each aircraft
4) Airports used by passengers
Your choice:
```

Simply enter a number (1-4) to select your query or 'q' to quit the application.

## Project Structure

```
cli-client/
├── src/
│   ├── main/java/com/example/flightcli/
│   │   ├── FlightCliApplication.java    # Main application entry point
│   │   ├── cli/
│   │   │   └── FlightCli.java          # CLI interface logic
│   │   ├── http/
│   │   │   ├── HttpRequester.java      # HTTP client interface
│   │   │   └── JavaHttpRequester.java  # HTTP client implementation
│   │   ├── model/                      # Data models
│   │   │   ├── AircraftAirportsView.java
│   │   │   ├── CityAirportsView.java
│   │   │   ├── PassengerAircraftView.java
│   │   │   └── PassengerAirportsView.java
│   │   └── service/
│   │       └── FlightApiClient.java    # API client service
│   └── test/java/                      # Unit tests
├── pom.xml                             # Maven configuration
└── README.md
```

## Dependencies

This project uses the following key dependencies:

- **Jackson Databind 2.16.1** - For JSON parsing and deserialization
- **JUnit Jupiter 5.10.2** - For unit testing framework
- **Mockito 5.11.0** - For mocking in tests

## Testing

### Run Tests Locally
```bash
mvn test
```

### Run with Coverage Analysis
```bash
mvn verify
```

### Continuous Integration

I've configured this project with GitHub Actions for automated testing. Every push or pull request to the `main` branch triggers automated testing via `mvn verify`.

The CI configuration can be found in `.github/workflows/ci.yml`.

## API Endpoints

The application interacts with the following API endpoints:

- `GET /airports-by-city` - Retrieve airports grouped by city
- `GET /aircraft-by-passenger` - Get aircraft types flown by passengers
- `GET /airports-by-aircraft` - Fetch airports used by aircraft types
- `GET /airports-by-passengers` - Get airports visited by passengers

## Development Notes

I implemented this CLI using a modular architecture with separate concerns for:
- HTTP communication (`http` package)
- Data models (`model` package) 
- API client logic (`service` package)
- CLI interface (`cli` package)

This separation makes the code maintainable and testable, with proper dependency injection for easy mocking in unit tests.

## Author

**Alex (Oleksii Bezkibalnyi)**  
DevOps Midterm Sprint Project

## Troubleshooting

### "Connection refused" Error
- Ensure the API server is running and accessible
- Verify the server URL is correct
- Check that the port isn't blocked by firewall

### "No data found" Message
- Confirm the server database contains test data
- Check server logs for any errors
- Verify API endpoints are responding correctly

### Build Issues
- Ensure Java 17+ is installed and configured
- Verify Maven settings and repository access
- Check for any dependency conflicts in `pom.xml`

## Future Enhancements

Potential improvements I'm considering:
- Add configuration file support for server settings
- Implement caching for API responses
- Add more detailed error handling and logging
- Support for additional output formats (JSON, CSV)
