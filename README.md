<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chúc Mừng Kỷ Niệm</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #ffc0cb, #ffb6c1, #ff9a9e); /* Lighter, softer gradient */
            font-family: 'Brush Script MT', cursive; /* More elegant font */
            text-align: center;
            overflow: hidden;
            position: relative;
            flex-direction: column;
        }

        .heart-container {
            position: relative;
            width: 400px;
            height: 400px;
            cursor: pointer;
            animation: pulse 1.5s infinite alternate; /* Heartbeat pulse */
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            100% { transform: scale(1.05); }
        }

        .fill {
            position: absolute;
            top: 100%;
            left: 0;
            width: 400px;
            height: 0;
            background: linear-gradient(45deg, #ff6b6b, #ff4d4d); /* More vibrant red */
            clip-path: path("M200 50 C250 0, 400 0, 400 150 C400 300, 200 400, 200 400 C200 400, 0 300, 0 150 C0 0, 150 0, 200 50 Z");
            transition: height 6s ease-in-out;
            border-radius: 200px 200px 0 0;  /* Smooth rounded top */
        }

        .click-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 2rem; /* Larger text */
            color: white;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5); /* Text shadow */
            animation: glow 1.5s infinite alternate;
        }
        @keyframes glow {
            0% { text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5); }
            100% { text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.7); }
        }

        .content-container {
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            padding: 20px;
            width: 80%; /* Limit width for better readability */
            max-width: 800px; /* Max width */
        }

        .anniversary-text {
            font-size: 3rem; /* Larger text */
            font-weight: bold;
            color: #ff55aa;
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 2s ease-out, transform 2s ease-out;
            margin-bottom: 30px;  /* Space between text and grid */
            text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.3);
            font-family: 'Brush Script MT', cursive;
        }

        .photo-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); /* Responsive grid */
            gap: 15px; /* Increased gap */
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 2s ease-out 2s, transform 2s ease-out 2s;
            margin-bottom: 40px; /* Space between grid and player */
        }

        .photo-frame {
            width: 100%; /* Responsive size */
            aspect-ratio: 1 / 1; /* Maintain square aspect ratio */
            border: 6px solid #ffb3cc; /* Thicker, lighter border */
            background-color: white;
            box-shadow: 0 4px 8px rgba(255, 105, 180, 0.5); /* Softer shadow */
            overflow: hidden;
            border-radius: 20px; /* More rounded corners */
            transition: transform 0.3s, box-shadow 0.3s;
            position: relative; /* For absolute positioning of elements inside */
        }
        .photo-frame:before { /* Decorative corner */
            content: '';
            position: absolute;
            top: -5px;
            left: -5px;
            width: 20px;
            height: 20px;
            background-color: #ffb3cc;
            clip-path: polygon(0% 0%, 100% 0%, 0% 100%);
            z-index: 1; /* Ensure it's on top */

        }

        .photo-frame img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: filter 0.5s ease; /* Smooth filter transition */
        }

        .photo-frame:hover {
            transform: scale(1.05); /* Slightly larger on hover */
            box-shadow: 0 6px 12px rgba(255, 105, 180, 0.7); /* Stronger shadow */
        }
        .photo-frame:hover img{
             filter: grayscale(50%); /* Apply grayscale on hover */
        }

        #spotify-player {
            width: 80%;
            max-width: 400px; /* Limit width */
            height: 80px;
            border-radius: 10px; /* Rounded corners */
            opacity: 0; /* Initially hidden */
            transition: opacity 1s ease 1s; /* Fade in after delay */

        }

        .spotify-wrapper {
            display: flex;
            justify-content: center;
            margin-top: 30px;  /* More space */

        }

        .falling-heart {
            position: absolute;
            font-size: 1.5rem;
            color: #ff69b4; /* Pink hearts */
            text-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
            animation: fallDown linear infinite;
            top: -50px;
            pointer-events: none; /*  Makes hearts non-clickable */
        }

        @keyframes fallDown {
            from { opacity: 1; transform: translateY(0) rotate(0deg); }
            to { transform: translateY(100vh) rotate(360deg); opacity: 0; }
        }

        .note {
            position: absolute;
            background-color: rgba(255, 255, 255, 0.9); /* More opaque white */
            color: #333; /* Darker text */
            border-radius: 15px; /* More rounded */
            padding: 10px;
            z-index: 8;
            text-align: center;
            display: none;
            justify-content: center;
            align-items: center;
            white-space: normal;
            word-break: break-word;
            font-size: 1rem;  /* Consistent font size */
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* Shadow on note */
            transition: opacity 0.3s ease, transform 0.3s ease;
            opacity: 0;
            transform: scale(0.8);
        }
        .note.show {
            display: flex; /* Use flexbox for centering */
            opacity: 1;
            transform: scale(1);
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
          width: 8px; /* Width of the scrollbar */
        }
        ::-webkit-scrollbar-track {
          background: #f0f0f0; /* Color of the track */
          border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb {
          background: #ff69b4; /* Color of the scrollbar handle */
          border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb:hover {
          background: #ff4d4d; /* Color of the handle on hover */
        }


    </style>
</head>
<body>
    <div class="heart-container" onclick="fillHeart()">
        <div class="fill" id="fill"></div>
        <div class="click-text">Click here! 💖</div>
    </div>

    <div class="content-container" id="contentContainer">
        <div class="anniversary-text">💓 Congratulations on your graduation! Your hard work has finally paid off. 💖</div>

        <div class="photo-grid">
            <div class="photo-frame" data-note=" Chúc Bé Yêu Sẽ Luôn Thành Công ❤️ ">
                <img id="photo1" src="Phạm Lưu Quỳnh Như [20-03-2025 23_14]/3ff9ce167696c7c89e872.jpg" alt="Ảnh 1">
            </div>
            <div class="photo-frame" data-note="Đậu Được HSK4 Và Tiếng Pháp 🎉">
                <img id="photo2" src="Phạm Lưu Quỳnh Như [20-03-2025 23_14]/04b70c5ab4da05845ccb4.jpg" alt="Ảnh 2">
            </div>
            <div class="photo-frame" data-note="Sớm Có Người Yêu Nha🥳 ">
                <img id="photo3" src="Phạm Lưu Quỳnh Như [20-03-2025 23_14]/8e245dcae54a54140d5b3.jpg" alt="Ảnh 3">
            </div>
            <div class="photo-frame" data-note="InAnhXink Luôn Bên Em 🎪 ">
                <img id="photo4" src="Phạm Lưu Quỳnh Như [20-03-2025 23_14]/e2a02e4f96cf27917ede1.jpg" alt="Ảnh 4">
            </div>
        </div>
        <div class="spotify-wrapper">
            <iframe id="spotify-player"
                    src="https://open.spotify.com/embed/track/4nXrVH5xwN1w6TpmP7uu8n"
                    frameborder="0"
                    allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture">
            </iframe>
        </div>

    </div>
      <div class="note" id="note"></div>

    <script>
        function fillHeart() {
            document.getElementById('fill').style.height = `100%`;
            document.getElementById('fill').style.top = `0%`;
            setTimeout(() => {
                document.querySelector('.heart-container').style.display = 'none';
                document.getElementById('contentContainer').style.display = 'flex';
                document.querySelector('.anniversary-text').style.opacity = 1;
                document.querySelector('.photo-grid').style.opacity = 1;
                document.getElementById('spotify-player').style.opacity = 1;

                // Preload images before showing content (optional, but good for smoother loading)
                const images = document.querySelectorAll('.photo-grid img');
                let loadedCount = 0;
                const imageLoaded = () => {
                  loadedCount++;
                  if (loadedCount === images.length) {
                    document.getElementById('contentContainer').style.display = 'flex'; // Show content

                  }
                }

                images.forEach(img => {
                    if (img.complete) { // Check if already loaded (cached)
                        imageLoaded();
                    } else {
                        img.onload = imageLoaded;
                        img.onerror = imageLoaded; // Handle potential loading errors
                    }
                });
            }, 6000);

        }
        function createFallingHearts() {
            let heart = document.createElement("div");
            heart.innerHTML = "💖"; //
            heart.classList.add("falling-heart");
            document.body.appendChild(heart);
            heart.style.left = Math.random() * window.innerWidth + "px";
            heart.style.animationDuration = Math.random() * 3 + 3 + "s";
            heart.style.fontSize = Math.random() * 1.5 + 1 + "rem"; // Varying heart sizes
            setTimeout(() => heart.remove(), 5000);
        }

        setInterval(createFallingHearts, 500); // More frequent hearts

        let imageStates = {}; //

        function showNote(element) {
            const imageId = element.id;
            const photoFrame = element.closest('.photo-frame'); // Use closest()
            const noteText = photoFrame.dataset.note;
            const noteDiv = document.getElementById('note');

            if (imageStates[imageId] === undefined) {
                imageStates[imageId] = true;
            }

            if (imageStates[imageId]) {
                // element.style.opacity = '0'; // Hide image - NO, we use the note now
                noteDiv.textContent = noteText;
                // noteDiv.style.display = 'flex'; // Moved to CSS class

                const rect = photoFrame.getBoundingClientRect();
                noteDiv.style.left = rect.left + 'px';
                noteDiv.style.top = rect.top + 'px';
                noteDiv.style.width = rect.width + 'px';
                noteDiv.style.height = rect.height + 'px';

                // NO dynamic font size adjustment needed, it's in CSS now.
                noteDiv.classList.add('show'); // Use a class for showing

            } else {
                // element.style.opacity = '1'; // Show image - NO
                // noteDiv.style.display = 'none'; // Moved to CSS class
                noteDiv.classList.remove('show'); // Use a class for hiding
            }

            imageStates[imageId] = !imageStates[imageId];
        }

    </script>
</body>
</html>