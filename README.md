
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Cold War Spy Clue Board</title>
  <style>
    body {
      font-family: 'Courier New', Courier, monospace;
      background-color: #f2e6c9;
      color: #2c2c2c;
      padding: 20px;
      text-align: center;
    }

    h1 {
      color: #800000;
      font-size: 32px;
      border-bottom: 2px solid #800000;
      display: inline-block;
      padding-bottom: 5px;
      margin-bottom: 20px;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(6, 1fr);
      gap: 15px;
      max-width: 1000px;
      margin: 0 auto;
    }

    .card {
      background: #111;
      color: #f0f0f0;
      padding: 20px;
      cursor: pointer;
      border: 2px solid #800000;
      border-radius: 4px;
      min-height: 90px;
      box-shadow: 2px 2px 6px rgba(0,0,0,0.4);
      transition: all 0.3s ease-in-out;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 14px;
      text-align: center;
    }

    .card:hover {
      background: #2c2c2c;
    }

    .card.revealed {
      background-color: #fff;
      color: #111;
      font-weight: bold;
    }

    #resetBtn {
      margin-top: 25px;
      padding: 10px 20px;
      background-color: #800000;
      color: white;
      border: none;
      font-size: 16px;
      border-radius: 4px;
      cursor: pointer;
      font-family: 'Courier New', Courier, monospace;
    }

    #resetBtn:hover {
      background-color: #a00000;
    }

    .instructions {
      font-size: 16px;
      margin-bottom: 20px;
    }
  </style>
</head>
<body>

  <h1>🕵️ OPERATION BLACKOUT</h1>
  <p class="instructions">
    Some intelligence is real. Some is false. Some is locked behind security.
  </p>

  <div class="grid" id="clueGrid"></div>

  <button id="resetBtn">🧹 Hide All Clues</button>

  <script>
    const clues = [
      { type: "normal", content: "Weiss collapsed five hours after the reception." },
      { type: "blank" },
      { type: "normal", content: "A witness saw the suspect speaking with Weiss in the Library." },
      { type: "firewall", content: "Tatiana never served Weiss.", question: "What military branch was Tatiana formerly part of?", answer: "Red Army" },
      { type: "normal", content: "Castor oil residue was found in the Smoking Room." },
      { type: "firewall", content: "Ludmila's notebook contained Soviet chemical formulas.", question: "What color was Ludmila's notebook?", answer: "Red" },

      { type: "blank" },
      { type: "normal", content: "Kruger left the party early, before the poisoning occurred." },
      { type: "blank" },
      { type: "normal", content: "Erich was in the Garden Courtyard all night." },
      { type: "firewall", content: "Only Ludmila and Kruger had chemical expertise.", question: "Name one suspect with chemical knowledge.", answer: "Ludmila" },
      { type: "normal", content: "The poison had no immediate taste and caused no convulsions." },

      { type: "blank" },
      { type: "normal", content: "Chernov was seen in the Lounge, far from the Smoking Room." },
      { type: "firewall", content: "A drink was swapped before Weiss left the Library.", question: "Where was Weiss last seen?", answer: "Library" },
      { type: "blank" },

      { type: "firewall", content: "Stasi intercepted a message: 'Operation Ricin is a go.'", question: "What was the operation name?", answer: "Operation Ricin" },
      { type: "blank" },

      { type: "firewall", content: "Kruger's lab was under Western surveillance.", question: "Which intelligence agency was watching Kruger?", answer: "CIA" },

      /* 🔒 NEW FIREWALL CLUES */
      { type: "firewall", content: "The poison was not fast-acting.", question: "Did Weiss die immediately? (yes/no)", answer: "no" },
      { type: "firewall", content: "The Smoking Room was accessed after midnight.", question: "Which room contained castor residue?", answer: "Smoking Room" },
      { type: "firewall", content: "The killer carried written chemical notes.", question: "Which suspect had a notebook?", answer: "Ludmila" },
      { type: "firewall", content: "The poison came from castor beans.", question: "What poison is made from castor beans?", answer: "Ricin" }
    ];

    const grid = document.getElementById('clueGrid');

    function createClueCard(clue, index) {
      const card = document.createElement('div');
      card.className = 'card';
      card.innerText = `Clue #${index + 1}`;

      card.onclick = () => {
        if (card.classList.contains("revealed")) return;

        if (clue.type === "normal") {
          card.innerText = clue.content;
        } else if (clue.type === "blank") {
          card.innerText = "✖ No intel found.";
        } else if (clue.type === "firewall") {
          const userAnswer = prompt("🔒 SECURITY CHECK:\n" + clue.question);
          if (userAnswer && userAnswer.trim().toLowerCase() === clue.answer.toLowerCase()) {
            card.innerText = clue.content;
          } else {
            card.innerText = "🛑 ACCESS DENIED.";
          }
        }

        card.classList.add("revealed");
      };

      grid.appendChild(card);
    }

    function renderGrid() {
      grid.innerHTML = "";
      clues.forEach((clue, index) => createClueCard(clue, index));
    }

    document.getElementById('resetBtn').onclick = renderGrid;

    renderGrid();
  </script>
</body>
</html>
