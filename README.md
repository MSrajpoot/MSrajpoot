// index.js (entry point of the server)

const express = require('express');
const app = express();
const port = process.env.PORT || 3000;

// Routes
const politicianRoutes = require('./routes/politicianRoutes');
const feedbackRoutes = require('./routes/feedbackRoutes');

// Middleware
app.use(express.json());

// Routes
app.use('/politicians', politicianRoutes);
app.use('/feedback', feedbackRoutes);

// Start the server
app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
