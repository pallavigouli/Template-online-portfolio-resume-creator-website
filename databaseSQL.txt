// Require the mysql library
const mysql = require('mysql');

// Create a connection to the MySQL database
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: 'password',
  database: 'portfolio'
});

// Connect to the MySQL database
connection.connect((err) => {
  if (err) {
    console.error('Could not connect to MySQL', err);
    return;
  }
  console.log('Connected to MySQL');
});

// Define a SQL query for creating a portfolio table
const createPortfolioTableQuery = `
CREATE TABLE IF NOT EXISTS portfolio (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  portfolio VARCHAR(255) NOT NULL
)`;

// Execute the SQL query to create the portfolio table
connection.query(createPortfolioTableQuery, (err, result) => {
  if (err) {
    console.error('Could not create portfolio table', err);
    return;
  }
  console.log('Portfolio table created');
});

// Define a SQL query for inserting a portfolio record
const insertPortfolioRecordQuery = `
INSERT INTO portfolio (name, email, portfolio) VALUES (?, ?, ?)`;

// Define the portfolio data
const portfolioData = ['John Doe', 'john@example.com', 'https://johndoe.com'];

// Execute the SQL query to insert the portfolio record
connection.query(insertPortfolioRecordQuery, portfolioData, (err, result) => {
  if (err) {
    console.error('Could not insert portfolio record', err);
    return;
  }
  console.log('Portfolio record inserted');
});

// Define a SQL query for retrieving all portfolio records
const getAllPortfolioRecordsQuery = `
SELECT * FROM portfolio`;

// Execute the SQL query to retrieve all portfolio records
connection.query(getAllPortfolioRecordsQuery, (err, result) => {
  if (err) {
    console.error('Could not retrieve portfolio records', err);
    return;
  }
  console.log('All portfolio records:', result);
});

// Define a SQL query for retrieving a specific portfolio record by ID
const getPortfolioRecordByIdQuery = `
SELECT * FROM portfolio WHERE id = ?`;

// Define the portfolio ID to retrieve
const portfolioId = 1;

// Execute the SQL query to retrieve the portfolio record by ID
connection.query(getPortfolioRecordByIdQuery, portfolioId, (err, result) => {
  if (err) {
    console.error('Could not retrieve portfolio record by ID', err);
    return;
  }
  console.log('Portfolio record by ID:', result[0]);
});
