# palette-generator
#html code
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Mood Palette</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <div class="container">
    <h1>Mood Palette Generator 🎨</h1>
    <select id="mood-select">
      <option value="">-- Select your mood --</option>
      <option value="happy">😊 Happy</option>
      <option value="sad">😢 Sad</option>
      <option value="relaxed">😌 Relaxed</option>
      <option value="energetic">⚡ Energetic</option>
    </select>
    <button onclick="generatePalette()">Generate Palette</button>
    <div id="palette" class="palette"></div>
  </div>
  <script src="script.js"></script>
</body>
</html>
#css code
body {
  font-family: 'Segoe UI', sans-serif;
  background-color: #f9f9f9;
  text-align: center;
  padding: 50px;
}

.container {
  max-width: 600px;
  margin: auto;
}

h1 {
  margin-bottom: 20px;
}

select, button {
  padding: 10px;
  margin: 10px;
  font-size: 16px;
}

.palette {
  margin-top: 30px;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 10px;
}

.color-box {
  width: 100px;
  height: 100px;
  border-radius: 8px;
  cursor: pointer;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  box-shadow: 0 2px 6px rgba(0,0,0,0.2);
  transition: transform 0.2s ease;
}

.color-box:hover {
  transform: scale(1.05);
}
#java script
const palettes = {
  happy: ['#FFD700', '#FFA500', '#FF69B4', '#FFB6C1', '#FFFFE0'],
  sad: ['#5D5C61', '#379683', '#7395AE', '#557A95', '#B1A296'],
  relaxed: ['#A8E6CF', '#DCEDC1', '#FFD3B6', '#FFAAA5', '#FF8B94'],
  energetic: ['#FF3E4D', '#FF9A00', '#FFCD02', '#00B8A9', '#6A0572']
};

function generatePalette() {
  const mood = document.getElementById('mood-select').value;
  const paletteDiv = document.getElementById('palette');
  paletteDiv.innerHTML = '';

  if (!mood || !palettes[mood]) {
    paletteDiv.innerHTML = '<p>Please select a mood to generate a palette.</p>';
    return;
  }

  palettes[mood].forEach(color => {
    const box = document.createElement('div');
    box.className = 'color-box';
    box.style.backgroundColor = color;
    box.textContent = color;

    box.onclick = () => {
      navigator.clipboard.writeText(color);
      box.textContent = 'Copied!';
      setTimeout(() => box.textContent = color, 1000);
    };

    paletteDiv.appendChild(box);
  });
}
