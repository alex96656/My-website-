<!-- Paste this below your <p>Welcome... line -->
<p>Enter TikTok username:</p>
<input type="text" id="usernameInput" placeholder="e.g., maikai04">
<button onclick="fetchStats()">Fetch Stats</button>

<p id="tiktok-stats">TikTok stats will appear here.</p>

<script>
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
</script>