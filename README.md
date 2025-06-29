# AI Travel Assistant

An intelligent travel booking assistant powered by AI agents and integrated with the Amadeus API for comprehensive travel services including flights, hotels, and travel planning.

## Features

- **Flight Search & Booking**: Search and compare flights using Amadeus API
- **Hotel Search & Recommendations**: Find and book accommodations
- **AI-Powered Travel Planning**: Intelligent travel recommendations using OpenAI Agents SDK
- **Real-time Travel Data**: Up-to-date flight information, pricing, and availability
- **Multi-Agent Architecture**: Specialized agents for different travel services
- **RESTful API**: Clean API endpoints for all travel services
- **Asynchronous Operations**: High-performance async/await implementation

## Quick Start

### Prerequisites

- Python 3.11 or higher
- [uv](https://docs.astral.sh/uv/) package manager (recommended)
- Amadeus API credentials
- OpenAI API key

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd ai-travel-assistant
   ```

2. **Install uv (if not already installed)**
   ```bash
   # On macOS/Linux
   curl -LsSf https://astral.sh/uv/install.sh | sh
   
   # On Windows
   powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
   
   # Or with pip
   pip install uv
   ```

3. **Create virtual environment and install dependencies**
   ```bash
   # Create and activate virtual environment
   uv venv
   
   # Activate virtual environment
   # On Windows:
   .venv\Scripts\activate
   # On macOS/Linux:
   source .venv/bin/activate
   
   # Install all dependencies
   uv sync
   
   # Or install production dependencies only
   uv install
   ```

4. **Set up environment variables**
   ```bash
   # Copy environment template
   cp .env.example .env
   
   # Edit .env file with your API credentials
   nano .env
   ```

   Required environment variables:
   ```env
   AMADEUS_CLIENT_ID=your_amadeus_client_id
   AMADEUS_CLIENT_SECRET=your_amadeus_client_secret
   AMADEUS_HOST=test  # or 'production' for live API
   OPENAI_API_KEY=your_openai_api_key
   ```

## Package Management with uv

### Installing Dependencies

```bash
# Install all dependencies (including dev dependencies)
uv sync

# Install production dependencies only
uv install

# Add a new dependency
uv add package-name

# Add a development dependency
uv add --dev package-name

# Add a specific version
uv add "package-name>=1.0.0"
```

### Development Dependencies

```bash
# Install with development dependencies
uv sync --group dev

# Add development dependencies
uv add --group dev pytest pytest-asyncio httpx
```

### Virtual Environment Management

```bash
# Create virtual environment
uv venv

# Create with specific Python version
uv venv --python 3.11

# Activate virtual environment
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

# Run commands in virtual environment
uv run python main.py
uv run pytest
```

## Running the Application

### Start the FastAPI Server

```bash
# Using uv (recommended)
uv run uvicorn src.app:create_app --factory --reload --host 0.0.0.0 --port 8000

# Or with activated virtual environment
uvicorn src.app:create_app --factory --reload --host 0.0.0.0 --port 8000
```

### Run Tests

```bash
# Run all tests
uv run pytest

# Run specific test file
uv run python src/test/test_amadeus_api.py

# Run tests with coverage
uv run pytest --cov=src

# Run async tests
uv run pytest src/test/test_amadeus_async.py
```

### Environment Testing

```bash
# Test environment variables
uv run python src/test/test_env_vars.py

# Test Amadeus API connection
uv run python src/test/test_amadeus_service.py
```

## Development

### Project Structure

```
ai-travel-assistant/
├── src/
│   ├── agents/              # AI agents for different services
│   │   └── hotel_agent.py
│   ├── config/              # Configuration settings
│   │   └── settings.py
│   ├── notebooks/           # Jupyter notebooks for exploration
│   │   └── hotel_agent.ipynb
│   ├── services/            # External API services
│   │   ├── amadeus_service.py
│   │   └── hotel_service.py
│   ├── test/               # Test files
│   │   ├── test_amadeus_api.py
│   │   ├── test_amadeus_async.py
│   │   └── ...
│   ├── utils/              # Utility functions
│   │   └── logger.py
│   └── app.py              # FastAPI application
├── .ruler/                 # Ruler configuration
│   ├── documentation/      # Generated documentation
│   ├── tests/             # Test documentation
│   └── mcp.json           # MCP server configuration
├── pyproject.toml         # Project configuration
├── uv.lock               # Dependency lock file
└── README.md             # This file
```

### Adding New Dependencies

```bash
# Add runtime dependency
uv add fastapi

# Add development dependency
uv add --group dev black

# Add optional dependency group
uv add --group notebook jupyter

# Remove dependency
uv remove package-name
```

### Code Quality

```bash
# Format code (if black is installed)
uv run black src/

# Type checking (if mypy is installed)
uv run mypy src/

# Linting (if ruff is installed)
uv run ruff check src/
```

## API Endpoints

Once running, the API will be available at `http://localhost:8000`

### Core Endpoints

- `GET /` - Health check
- `GET /docs` - Interactive API documentation (Swagger UI)
- `GET /redoc` - Alternative API documentation

### Flight Services

- `GET /api/flights/search` - Search for flights
- `GET /api/flights/airports` - Search airports

### Hotel Services

- `GET /api/hotels/search` - Search for hotels
- `GET /api/hotels/recommendations` - Get AI-powered hotel recommendations

### AI Agent Services

- `POST /api/agent/chat` - Chat with travel planning agent
- `POST /api/agent/plan` - Generate travel plans

## Testing

The project includes comprehensive tests for all components:

### Test Categories

- **API Tests**: Direct Amadeus API integration tests
- **Service Tests**: Business logic and service layer tests
- **Async Tests**: Asynchronous operation tests
- **Environment Tests**: Configuration and setup validation

### Running Specific Tests

```bash
# Test Amadeus API integration
uv run python src/test/test_amadeus_api.py

# Test async operations
uv run python src/test/test_amadeus_async.py

# Test service layer
uv run python src/test/test_amadeus_service.py

# Test environment setup
uv run python src/test/test_env_vars.py
```

## Documentation

- **Service Documentation**: `.ruler/documentation/amadeus_service.md`
- **Test Documentation**: `.ruler/tests/test_documentation.md`
- **API Documentation**: Available at `/docs` when server is running

## Security

- API credentials are managed through environment variables
- Sensitive information is masked in logs
- CORS is configured for cross-origin requests
- Input validation on all API endpoints

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes
4. Run tests: `uv run pytest`
5. Commit changes: `git commit -am 'Add feature'`
6. Push to branch: `git push origin feature-name`
7. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For support and questions:

1. Check the documentation in `.ruler/documentation/`
2. Review test examples in `src/test/`
3. Run environment tests to validate setup
4. Check API documentation at `/docs`

## Updates

To update dependencies:

```bash
# Update all dependencies
uv sync --upgrade

# Update specific dependency
uv add package-name@latest

# Check for outdated dependencies
uv tree --outdated
```