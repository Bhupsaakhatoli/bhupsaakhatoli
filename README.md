### Hi there 👋

<!--
**Bhupsaakhatoli/bhupsaakhatoli** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
<?php
// Include the class.youtube.php file that contains the logic for fetching and downloading the video links
require_once 'class.youtube.php';

// Create an instance of the YouTube class
$yt = new YouTube();

// Check if the user has submitted a video URL
if (isset($_POST['url'])) {
  // Get the video URL from the POST data
  $url = $_POST['url'];

  // Validate the video URL
  if ($yt->validateURL($url)) {
    // Get the video information and formats
    $video = $yt->getVideoInfo($url);

    // Check if the video information and formats are available
    if ($video) {
      // Display the video title and thumbnail
      echo '<h1>' . $video['title'] . '</h1>';
      echo '<img src="' . $video['thumbnail'] . '" alt="Thumbnail">';

      // Display the download links for each format
      echo '<ul>';
      foreach ($video['formats'] as $format) {
        echo '<li><a href="' . $format['url'] . '" download>' . $format['type'] . ' - ' . $format['quality'] . '</a></li>';
      }
      echo '</ul>';
    } else {
      // Display an error message if the video information and formats are not available
      echo '<p>Sorry, the video information and formats are not available.</p>';
    }
  } else {
    // Display an error message if the video URL is not valid
    echo '<p>Sorry, the video URL is not valid.</p>';
  }
}
?>

<!-- Display an HTML form for entering the video URL -->
<form method="post" action="">
  <label for="url">Enter a YouTube video URL:</label>
  <input type="text" id="url" name="url" placeholder="https://www.youtube.com/watch?v=...">
  <input type="submit" value="Download">
</form>
