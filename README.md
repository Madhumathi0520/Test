# Test
const express = require('express');
const app = express();

app.use(express.json());

app.post('/api/transform', (req, res) => {
  try {
    const { sentence } = req.body;
    
    if (!sentence || typeof sentence !== 'string') {
      return res.status(400).json({ error: 'Invalid input: sentence must be a string' });
    }
    
    const words = sentence.split(' ');
    
    const wordCount = words.length;
    
    const uniqueWords = [...new Set(words.map(word => word.toLowerCase()))];
    
    const reversedSentence = words.reverse().join(' ');
    
    res.json({
      word_count: wordCount,
      unique_words: uniqueWords,
      reversed_sentence: reversedSentence
    });
  } catch (error) {
    res.status(500).json({ error: 'Internal server error' });
  }
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
