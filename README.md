<!DOCTYPE html><html>
<head>
  <title>TikTok Stats</title>
  <meta charset="UTF-8">
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 50px;
      background: #f5f5f5;
    }
    input, button {
      padding: 10px;
      font-size: 1rem;
      margin: 5px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    button {
      cursor: pointer;
      background-color: #007bff;
      color: white;
      border: none;
      transition: background 0.3s;
    }
    button:hover {
      background-color: #0056b3;
    }
    #tiktok-stats {
      margin-top: 20px;
      font-size: 1.2rem;
    }
  </style>
</head>
<body>
  <h1>TikTok Stats Fetcher</h1>
  <input type="text" id="usernameInput" placeholder="Enter TikTok username">
  <button onclick="fetchStats()">Fetch Stats</button>
  <p id="tiktok-stats">Stats will appear here.</p>  <script>
    const statsElement = document.getElementById("tiktok-stats");
    const input = document.getElementById("usernameInput");

    async function fetchStats() {
      const username = input.value.trim();
      if (!username) {
        statsElement.textContent = "Please enter a username.";
        return;
      }
      statsElement.textContent = "Loading...";
      try {
        const response = await fetch(`https://nekoweb.vercel.app/api/tiktok?user=${username}`);
        const data = await response.json();
        if (data.error) {
          statsElement.textContent = "Failed to load TikTok stats. Make sure the username is correct.";
          return;
        }
        statsElement.innerHTML = `
          🎵 <strong>${data.username}</strong><br>
          Followers: ${data.followers.toLocaleString()}<br>
          Likes: ${data.likes.toLocaleString()}<br>
          Videos: ${data.videos}
        `;
      } catch (err) {
        statsElement.textContent = "Error fetching TikTok stats.";
        console.error(err);
      }
    }
  </script></body>
</html>