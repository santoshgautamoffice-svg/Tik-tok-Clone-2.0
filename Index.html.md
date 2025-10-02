<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>TikTok-Style Scrolling Video Feed</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    html, body {
      margin: 0;
      padding: 0;
      background: #000;
      height: 100%;
      width: 100vw;
      font-family: Arial, sans-serif;
      overflow-x: hidden;
    }
    .feed {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 24px;
      padding: 0;
      margin: 0 auto;
      width: 100vw;
      max-width: 420px;
    }
    .video-container {
      position: relative;
      width: 100vw;
      max-width: 420px;
      height: 80vh;
      background: #222;
      border-radius: 20px;
      overflow: hidden;
      box-shadow: 0 4px 24px rgba(0,0,0,0.5);
    }
    video {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
      background: #000;
    }
    .overlay {
      position: absolute;
      bottom: 24px;
      left: 16px;
      right: 16px;
      color: #fff;
      font-size: 1.5rem;
      font-weight: bold;
      text-shadow: 0 2px 8px rgba(0,0,0,0.7);
    }
    @media (max-width: 600px) {
      .video-container {
        height: 88vh;
        border-radius: 0;
        max-width: 100vw;
      }
      .feed {
        max-width: 100vw;
      }
    }
  </style>
</head>
<body>
  <div class="feed">
    <div class="video-container">
      <video src="https://www.w3schools.com/html/mov_bbb.mp4" autoplay muted loop playsinline></video>
      <div class="overlay">Big Buck Bunny</div>
    </div>
    <div class="video-container">
      <video src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4" autoplay muted loop playsinline></video>
      <div class="overlay">Beautiful Flowers</div>
    </div>
    <div class="video-container">
      <video src="https://www.w3schools.com/html/movie.mp4" autoplay muted loop playsinline></video>
      <div class="overlay">Bear in the Wild</div>
    </div>
  </div>
  <script>
    // Play only video in view
    const videos = document.querySelectorAll("video");
    const config = { threshold: 0.6 };
    function handleEntry(entries) {
      entries.forEach(entry => {
        const video = entry.target;
        if (entry.isIntersecting) {
          video.play();
        } else {
          video.pause();
        }
      });
    }
    const observer = new IntersectionObserver(handleEntry, config);
    videos.forEach(video => observer.observe(video));
    // Prevent autoplay policies from blocking playback
    document.addEventListener('click', () => {
      videos.forEach(v => v.play());
    }, { once: true });
  </script>
</body>
</html>