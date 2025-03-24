# Generating README Templates

## Prompt 1: Creating Project README
```
Intent: To help developers create comprehensive README files for their projects.

Context: You are creating a README file for a new project. The project details are as follows:

Project_name: {project_name}
Project_description: {project_description}
Technologies_used: {technologies_used}

Generate a README template, including:
- Project title and description.
- Installation and setup instructions.
- Usage examples and documentation.

Example:
Project_name: "Weather API Client"
Project_description: "A client library for accessing weather data from multiple providers."
Technologies_used: "Python, Requests, pytest"

README Template:
```markdown
# Weather API Client

A client library for accessing weather data from multiple providers.

## Features
- Support for multiple weather data providers
- Simple, consistent API
- Comprehensive error handling

## Installation
```bash
pip install weather-api-client
```

## Usage
```python
from weather_client import WeatherClient

client = WeatherClient(api_key="your_api_key")
weather = client.get_current_weather(city="New York")
print(f"Temperature: {weather.temperature}°C")
```

## Development
1. Clone the repository
2. Install dependencies: `pip install -r requirements.txt`
3. Run tests: `pytest`

## License
MIT
```
```