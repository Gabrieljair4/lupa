# lupa
Projeto para procura de perfis em redes sociais baseados em fotos.


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Social Profile Finder</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      background-color: #f4f4f4;
    }
    header {
      background-color: #4CAF50;
      color: white;
      width: 100%;
      text-align: center;
      padding: 1rem 0;
    }
    .container {
      max-width: 800px;
      width: 100%;
      background: white;
      padding: 20px;
      margin: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    input, textarea, select, button {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 4px;
      box-sizing: border-box;
    }
    button {
      background-color: #4CAF50;
      color: white;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background-color: #45a049;
    }
    .results {
      margin-top: 20px;
    }
    .progress-bar {
      width: 0;
      height: 20px;
      background-color: #4CAF50;
      border-radius: 4px;
      transition: width 0.3s;
    }
    @media (max-width: 600px) {
      .container {
        padding: 10px;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>Social Profile Finder</h1>
  </header>
  <div class="container">
    <h2>Upload Image</h2>
    <input type="file" id="imageUpload" accept="image/*">
    <canvas id="faceCanvas" style="display:none;"></canvas>

    <h2>Additional Information</h2>
    <input type="text" id="fullName" placeholder="Full Name">
    <input type="text" id="location" placeholder="Location (City, State, Country)">
    <input type="text" id="organization" placeholder="Company or Institution">
    <input type="number" id="age" placeholder="Approximate Age">
    <textarea id="interests" placeholder="Interests or Hobbies"></textarea>
    <input type="text" id="username" placeholder="Username (if known)">

    <button onclick="startSearch()">Search Profiles</button>

    <div class="progress-container">
      <div class="progress-bar" id="progressBar"></div>
    </div>

    <div class="results" id="results">
      <h3>Search Results</h3>
      <ul id="resultsList"></ul>
    </div>

    <div class="privacy">
      <h4>Privacy Notice</h4>
      <p>Your data is processed locally in your browser. No information is stored on our servers.</p>
    </div>

    <div class="instructions">
      <h4>How to Use</h4>
      <ol>
        <li>Upload a clear photo of the person.</li>
        <li>Fill in any known additional information.</li>
        <li>Click "Search Profiles" to begin the search.</li>
        <li>Review the results and visit the matched profiles.</li>
      </ol>
    </div>
  </div>

  <script>
    function startSearch() {
      const progressBar = document.getElementById('progressBar');
      progressBar.style.width = '0%';
      
      let progress = 0;
      const interval = setInterval(() => {
        if (progress >= 100) {
          clearInterval(interval);
          displayResults();
        } else {
          progress += 10;
          progressBar.style.width = progress + '%';
        }
      }, 300);
    }

    function displayResults() {
      const resultsList = document.getElementById('resultsList');
      resultsList.innerHTML = '';
      
      // Placeholder results
      const dummyResults = [
        {name: 'John Doe', platform: 'Facebook', link: '#'},
        {name: 'Jane Smith', platform: 'Instagram', link: '#'},
        {name: 'Mike Johnson', platform: 'LinkedIn', link: '#'}
      ];

      dummyResults.forEach(profile => {
        const li = document.createElement('li');
        li.innerHTML = `<a href="${profile.link}" target="_blank">${profile.name} (${profile.platform})</a>`;
        resultsList.appendChild(li);
      });
    }
  </script>
</body>
</html>
