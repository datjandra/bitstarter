# Bitstarter

A full-stack Node.js web application demonstrating server-side JavaScript development with Bitcoin/Coinbase payment integration and a question-answering interface.

## Project Overview

**Bitstarter** is an educational and practical example of building a modern web application using Node.js and Express. The project integrates multiple technologies to create a complete platform that processes orders through the Coinbase API and provides a question-answering interface powered by Wikipedia search.

## Key Features

### 1. **Bitcoin/Coinbase Payment Integration**
- Syncs and processes orders from the Coinbase API
- Stores completed Bitcoin transactions in a PostgreSQL database
- Automatically tracks order status and amounts in BTC
- RESTful endpoints for retrieving and refreshing orders

### 2. **Question-Answering System**
- **Vocifery**: A semantic question-answering engine that processes natural language queries
- Searches Wikipedia for relevant information
- Decomposes questions into semantic features (answer type, action, focus, target, qualifiers)
- Ranks and displays search results with supporting evidence
- Validates questions to ensure they follow proper format (start with question word, end with "?")

### 3. **Contact Management**
- Email notification system using Gmail SMTP
- Contact form integrated into the web interface
- Server-side email handling with nodemailer

### 4. **HTML/DOM Validation Tools**
- **grader.js**: Command-line utility for validating HTML structure
- Checks for presence of specific HTML tags and attributes
- Supports both local file checking and remote URL validation
- Uses Cheerio for efficient server-side DOM parsing

## Technology Stack

### Backend
- **Runtime**: Node.js v0.10.12
- **Framework**: Express.js v3.3.4
- **Database**: PostgreSQL with Sequelize ORM v2.0.0-alpha2
- **Template Engine**: EJS v0.8.4
- **HTTP Client**: Restler
- **Email**: Nodemailer
- **Utilities**: Async.js v0.2.9

### Frontend
- **Styling**: Bootstrap CSS Framework with responsive design
- **DOM Manipulation**: jQuery v1.10.1
- **Analytics**: Google Analytics
- **Social Sharing**: AddThis buttons
- **Fonts**: Ubuntu, Roboto custom fonts

### Development Tools
- **HTML Validation**: Cheerio (server-side jQuery-like DOM parsing)

## Project Structure

```
bitstarter/
├── index.html          # Main UI for Vocifery question-answering system
├── landing.html        # Landing page
├── web.js             # Express.js application server
├── grader.js          # HTML validation utility
├── checks.json        # Validation checks configuration
├── package.json       # Node.js dependencies and metadata
├── Procfile           # Heroku deployment configuration
├── models/            # Sequelize ORM models
├── views/             # EJS template files
├── bootstrap/         # Front-end static assets (CSS, JS)
└── url.csv            # Sample URLs for testing
```

## Getting Started

### Installation

```bash
# Install dependencies
npm install

# Set up environment variables
export PORT=8080
export COINBASE_API_KEY="your_coinbase_api_key"
```

### Running the Application

```bash
node web.js
```

The server will start on `http://localhost:8080`

### Using the HTML Validator

```bash
# Validate a local HTML file
node grader.js -f index.html -c checks.json

# Validate a remote URL
node grader.js -u https://example.com -c checks.json
```

## Main Endpoints

### Web Interface
- **`GET /`** - Home page with Vocifery question-answering interface
- **`GET /orders`** - Display all completed Bitcoin orders from the database

### API Endpoints
- **`POST /email`** - Send contact form emails
- **`GET /refresh_orders`** - Sync latest orders from Coinbase API to database

## How It Works

### Order Processing Flow
1. User triggers `/refresh_orders` endpoint
2. Application fetches orders from Coinbase API using API key
3. Filters completed orders only
4. Checks if order already exists in PostgreSQL database
5. Converts satoshi amounts to BTC (dividing by 100,000,000)
6. Stores new orders with Coinbase ID, amount, and timestamp
7. Displays orders on the `/orders` page

### Question-Answering Flow (Vocifery)
1. User enters a question starting with a question word (when, where, why, who, what, which, how)
2. Question must end with a question mark
3. System parses question and extracts semantic features
4. Searches Wikipedia using extracted keywords
5. Ranks results by keyword matches in titles
6. Fetches full content from top matches
7. Processes results to identify and display relevant answers with evidence snippets

## Database Schema

The application uses Sequelize ORM with PostgreSQL for data persistence.

### Order Model
- `coinbase_id` - Unique identifier from Coinbase
- `amount` - Order amount in BTC
- `time` - Order creation timestamp
- Auto-incrementing primary key

## Configuration Files

### `checks.json`
JSON array of CSS selectors used to validate the presence of HTML elements in pages.

### `Procfile`
Heroku deployment configuration specifying how to start the application.

### `package.json`
- Node.js version: 0.10.12
- npm version: 1.2.30
- Dependencies locked to specific versions for stability

## Security Considerations

**Note**: This is an educational project. Production deployments should:
- Use environment variables for sensitive credentials (API keys, database credentials)
- Implement proper authentication and authorization
- Use HTTPS for all communications
- Sanitize user inputs to prevent injection attacks
- Never commit credentials to version control
- Implement rate limiting on API endpoints

## Use Cases

1. **Learning Node.js Development**: Complete example of Express.js application structure
2. **Payment Integration**: Demonstrates Coinbase API integration for Bitcoin payments
3. **Question Answering System**: Example of semantic analysis and information retrieval
4. **HTML Validation**: Automated testing tools for web page structure
5. **Heroku Deployment**: Ready-to-deploy Node.js application

## License

This project is licensed under the [Creative Commons Attribution-ShareAlike 3.0](http://creativecommons.org/licenses/by-sa/3.0/) license.

## Author

Created by Donny Tjandra (@datjandra)

## Related Resources

- [Coinbase API Documentation](https://coinbase.com/)
- [Express.js Guide](http://expressjs.com/)
- [Sequelize Documentation](http://docs.sequelizejs.com/)
- [Cheerio Documentation](https://cheerio.js.org/)

---

**Last Updated**: May 2026
