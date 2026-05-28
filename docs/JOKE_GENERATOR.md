# Joke Generator Feature

## Overview
This feature implements a random joke generator that fetches jokes from external APIs.

## API Used
- **Primary API:** [Official Joke API](https://official-joke-api.appspot.com/)
  - Random Joke: `https://official-joke-api.appspot.com/random_joke`
  - By Type: `https://official-joke-api.appspot.com/jokes/{type}/random`

## Features

### 1. JokeGenerator Class (`src/joke_generator.py`)
- `get_random_joke()` - Fetches a random joke
- `get_joke_by_type(joke_type)` - Fetches jokes by type (general, knock-knock)
- `format_joke(joke)` - Formats joke data into readable format

### 2. CLI Interface
Run the CLI directly:
```bash
python src/joke_generator.py
```

Interactive menu with options to:
- Get a random joke
- Get a general joke
- Get a knock-knock joke
- Exit

### 3. REST API Endpoints (`src/api.py`)

#### Get Random Joke
```
GET /api/joke
```
Response:
```json
{
  "success": true,
  "data": {
    "type": "general",
    "setup": "Why did the chicken cross the road?",
    "punchline": "To get to the other side!",
    "id": 1,
    "source": "official-joke-api"
  }
}
```

#### Get Joke by Type
```
GET /api/joke/{type}
```

Supported types:
- `general`
- `knock-knock`

Response:
```json
{
  "success": true,
  "data": {
    "type": "general",
    "setup": "...",
    "punchline": "...",
    "id": 123,
    "source": "official-joke-api"
  }
}
```

#### Health Check
```
GET /api/health
```

## Installation & Setup

### Prerequisites
- Python 3.7+
- pip

### Install Dependencies
```bash
pip install -r requirements.txt
```

### Running the Application

#### CLI Mode
```bash
python src/joke_generator.py
```

#### API Server Mode
```bash
python src/api.py
```
The server will start on `http://localhost:5000`

### Running Tests
```bash
pytest tests/test_joke_generator.py -v
```

With coverage report:
```bash
pytest tests/test_joke_generator.py --cov=src
```

## Usage Examples

### Python
```python
from src.joke_generator import JokeGenerator

generator = JokeGenerator()

# Get a random joke
joke = generator.get_random_joke()
print(generator.format_joke(joke))

# Get a specific type
joke = generator.get_joke_by_type('knock-knock')
print(generator.format_joke(joke))
```

### cURL
```bash
# Get random joke
curl http://localhost:5000/api/joke

# Get general joke
curl http://localhost:5000/api/joke/general

# Get knock-knock joke
curl http://localhost:5000/api/joke/knock-knock

# Health check
curl http://localhost:5000/api/health
```

### JavaScript/Fetch
```javascript
// Get random joke
fetch('http://localhost:5000/api/joke')
  .then(response => response.json())
  .then(data => console.log(data));

// Get knock-knock joke
fetch('http://localhost:5000/api/joke/knock-knock')
  .then(response => response.json())
  .then(data => console.log(data));
```

## Error Handling
- Invalid joke types return 400 Bad Request
- API failures return 500 Internal Server Error
- Missing endpoints return 404 Not Found

## Future Improvements
- [ ] Add more joke APIs as fallback
- [ ] Implement caching mechanism
- [ ] Add rate limiting
- [ ] Support for multiple languages
- [ ] Database to store favorite jokes
- [ ] User preferences and ratings
- [ ] WebSocket for real-time joke delivery

## Testing
All functions are unit tested with mocked API responses. Run tests with:
```bash
pytest tests/test_joke_generator.py -v --cov=src
```

## Notes
- The API has no authentication requirement
- Response times typically 200-500ms
- Jokes are randomly selected each time
