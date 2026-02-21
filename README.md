<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Flashcards</title>
<style>
  body {
    font-family: Arial, sans-serif;
    text-align: center;
  }
  
  #flashcard {
    border: 1px solid #ccc;
    padding: 20px;
    margin: 20px auto;
    max-width: 80%;
    background-color: #f9f9f9;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  table {
    border-collapse: collapse;
    width: 80%;
    margin: 20px auto;
  }
  
  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }
  
  input[type="text"], button {
    padding: 10px;
    margin: 10px;
    width: 200px;
  }

  button {
    font-weight: bold;
  }
</style>
</head>
<body>
  
  <div id="flashcard"></div>
  
  <button onclick="toggleWordList()">Word List</button>
  <button onclick="startGame()">Start</button>
  <input type="file" id="fileInput" accept=".xlsx">

  <table id="wordListTable" style="display:none;"></table>
  
  <script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.0/dist/xlsx.full.min.js"></script>
  <script>
    const flashcards = [];
    const wordListTable = document.getElementById("wordListTable");
    let currentFlashcardIndex = -1; // Track the current flashcard index

    function toggleWordList() {
      wordListTable.style.display = wordListTable.style.display === 'none' ? 'table' : 'none';
    }

    function startGame() {
      if (flashcards.length > 0) {
        showRandomFlashcard();
      } else {
        alert("Upload Excel file to continue.");
      }
    }

    function showRandomFlashcard() {
      // Pick a random flashcard
      const randomIndex = Math.floor(Math.random() * flashcards.length);
      currentFlashcardIndex = randomIndex;

      const randomFlashcard = flashcards[randomIndex];
      document.getElementById("flashcard").innerHTML = `
        <h3>${randomFlashcard.phrase}</h3>
        <input type="text" id="definitionGuess" style="width: 80%;" placeholder="Enter Definition" onkeydown="if(event.key==='Enter') checkAnswer('${randomFlashcard.definition}')">
        <button onclick="checkAnswer('${randomFlashcard.definition}')">Check Answer</button>
      `;
      document.getElementById("definitionGuess").focus(); // Keep the input focused
    }

    function checkAnswer(correctAnswer) {
      const userAnswer = document.getElementById("definitionGuess").value;
      const flashcard = document.getElementById("flashcard");
      
      if (userAnswer.trim().toLowerCase() === correctAnswer.toLowerCase()) {
        flashcard.style.backgroundColor = "lightgreen";
        setTimeout(() => {
          flashcard.style.backgroundColor = "#f9f9f9";
          showRandomFlashcard(); // Show a new random flashcard
        }, 1000);
      } else {
        flashcard.style.backgroundColor = "lightcoral";
        flashcard.innerHTML += `<p style="color: red; font-weight: bold;">Correct Answer: ${correctAnswer}</p>`;
        setTimeout(() => {
          flashcard.style.backgroundColor = "#f9f9f9";
        }, 1000);
      }
      document.getElementById("definitionGuess").value = "";
      document.getElementById("definitionGuess").focus(); // Keep the input focused
    }

    document.getElementById('fileInput').addEventListener('change', handleFile);

    function handleFile(e) {
      const file = e.target.files[0];
      const reader = new FileReader();

      reader.onload = function(event) {
        const data = new Uint8Array(event.target.result);
        const workbook = XLSX.read(data, { type: 'array' });

        const sheetName = workbook.SheetNames[0];
        const sheet = workbook.Sheets[sheetName];
        const jsonData = XLSX.utils.sheet_to_json(sheet, { header: 1 });

        populateFlashcards(jsonData);
        renderWordListTable(jsonData);
      };

      reader.readAsArrayBuffer(file);
    }

    // Populate the flashcards array with data from the Excel file
    function populateFlashcards(data) {
      // Skip the header row (index 0) and process the remaining rows
      const rows = data.slice(1);

      rows.forEach(row => {
        if (row[0] && row[1]) { // Ensure both phrase and definition are provided
          flashcards.push({ phrase: row[0], definition: row[1] });
        }
      });
    }

    function renderWordListTable(data) {
      const headers = data[0];
      const rows = data.slice(1);

      const headerRow = `<tr>${headers.map(header => `<th>${header}</th>`).join('')}</tr>`;
      const bodyRows = rows.map(row => `<tr>${row.map(cell => `<td>${cell}</td>`).join('')}</tr>`);

      wordListTable.innerHTML = `<thead>${headerRow}</thead><tbody>${bodyRows.join('')}</tbody>`;
      wordListTable.style.display = 'none'; // Initially hide the table
    }
  </script>
</body>
</html>
