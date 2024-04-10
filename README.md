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
// routes/politicianRoutes.js

const express = require('express');
const router = express.Router();
const politicianController = require('../controllers/politicianController');

// GET all politicians
router.get('/', politicianController.getAllPoliticians);

// POST a new politician
router.post('/', politicianController.createPolitician);

// GET politician by ID
router.get('/:id', politicianController.getPoliticianById);

// PUT update politician details
router.put('/:id', politicianController.updatePolitician);

// DELETE politician
router.delete('/:id', politicianController.deletePolitician);

module.exports = router;
// controllers/politicianController.js

const Politician = require('../models/Politician');

// Example controller functions
exports.getAllPoliticians = async (req, res) => {
  try {
    const politicians = await Politician.find();
    res.json(politicians);
  } catch (err) {
    res.status(500).json({ message: err.message });
  }
};

exports.createPolitician = async (req, res) => {
  const politician = new Politician({
    name: req.body.name,
    party: req.body.party,
    // other fields
  });

  try {
    const newPolitician = await politician.save();
    res.status(201).json(newPolitician);
  } catch (err) {
    res.status(400).json({ message: err.message });
  }
};

// Other controller functions (update, delete, etc.) would follow a similar pattern

