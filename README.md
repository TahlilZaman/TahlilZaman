
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Live Cricket Scores</title>
</head>
<body>

<h1>Live Cricket Scores</h1>
<div id="live-scores"></div>

<script>
    // Replace 'YOUR_API_KEY' with your actual API key from a cricket data provider
    const apiKey = 'YOUR_API_KEY';
    const apiUrl = 'https://api.cricket-scores-provider.com/live-scores';

    async function getLiveScores() {
        try {
            const response = await fetch(`${apiUrl}?apiKey=${apiKey}`);
            const data = await response.json();
            
            // Display live scores on the webpage
            const scoresContainer = document.getElementById('live-scores');
            scoresContainer.innerHTML = '';

            if (data && data.matches) {
                data.matches.forEach(match => {
                    const matchElement = document.createElement('div');
                    matchElement.textContent = `${match.team1} vs ${match.team2}: ${match.score}`;
                    scoresContainer.appendChild(matchElement);
                });
            } else {
                scoresContainer.textContent = 'No live scores available.';
            }
        } catch (error) {
            console.error('Error fetching live scores:', error);
        }
    }

    // Fetch live scores on page load
    getLiveScores();

    // Update scores every 5 minutes (adjust the interval as needed)
    setInterval(getLiveScores, 300000);
</script>

</body>
</html>
