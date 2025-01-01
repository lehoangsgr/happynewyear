# happynewyear
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy New Year 2025!</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            overflow: hidden; /* Prevents scrollbars from appearing */
            background-color: #000; /* Dark background for fireworks effect */
            color: #fff; /* White text color for contrast */
        }
        header {
            padding: 20px 0;
        }
        h1 {
            margin: 0;
            font-size: 3rem;
            font-family: 'Arial', sans-serif;
            animation: colorChange 5s infinite;
        }
        @keyframes colorChange {
            0% { color: red; }
            25% { color: yellow; }
            50% { color: green; }
            75% { color: blue; }
            100% { color: red; }
        }
        input {
            margin-top: 20px;
            padding: 10px;
            font-size: 1.2rem;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 1.2rem;
            color: white;
            background-color: #007bff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        .message {
            margin-top: 30px;
            font-size: 1.5rem;
            color: #fff;
            position: relative;
        }
        .video-container {
            position: relative;
            width: 100%;
            max-width: 800px; /* Max width to control the size on larger screens */
            margin: 20px auto; /* Center the container */
        }
        .video-container iframe {
            width: 100%;
            height: 450px;
            border: none;
        }
        @media (max-width: 768px) {
            .video-container {
                max-width: 100%; /* Full width on smaller screens */
            }
        }
        /* Fireworks CSS */
        .firework {
            position: absolute;
            width: 10px;
            height: 10px;
            background: transparent;
            border-radius: 50%;
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
            animation: explode 1s ease-out forwards;
        }
        @keyframes explode {
            0% { transform: scale(0); opacity: 1; }
            100% { transform: scale(3); opacity: 0; }
        }
    </style>
</head>
<body>
    <header>
        <h1>DH23CN Chúc Mừng Năm Mới 2025 tới các bạn!</h1>
    </header>
    <div>
        <input type="text" id="fullName" placeholder="Nhập họ và tên của bạn">
        <button onclick="generateWish()">Nhận câu chúc năm mới</button>
        <div class="message" id="message"></div>
    </div>
    <div class="video-container">
        <iframe src="https://www.youtube.com/embed/w8znloDg_Yk" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>

    <audio id="fireworkSound" src="path_to_your_firework_sound.mp3" preload="auto"></audio>

    <script>
        const wishes = [
            "Chúc bạn HỌ TÊN một năm học mới tràn đầy thành công và khám phá tại Đại học Nông Lâm TP.HCM!",
            "Năm mới hạnh phúc HỌ TÊN! Hãy tận hưởng mỗi khoảnh khắc học tập tại Đại học Nông Lâm TP.HCM.",
            "Chúc bạn HỌ TÊN đạt được mọi ước mơ và mục tiêu trong năm học mới!",
            "HỌ TÊN chúc bạn luôn kiên trì và nỗ lực trong hành trình học tập tại Đại học Nông Lâm TP.HCM.",
            "Mong rằng năm 2025 sẽ mang đến cho bạn HỌ TÊN nhiều cơ hội học hỏi và trưởng thành!",
            "HỌ TÊN chúc bạn luôn tìm thấy niềm vui và ý nghĩa trong học tập tại Đại học Nông Lâm TP.HCM.",
            "Chúc bạn HỌ TÊN khám phá được nhiều điều thú vị trong học tập và cuộc sống tại trường.",
            "Năm mới vui vẻ HỌ TÊN! Hãy biến 2025 thành năm của tri thức và thành tựu.",
            "Chúc bạn HỌ TÊN luôn gặt hái nhiều thành công trong học tập và cuộc sống tại Đại học Nông Lâm TP.HCM.",
            "HỌ TÊN chúc bạn một năm học mới đầy cảm hứng và sáng tạo!",
            "Chúc bạn HỌ TÊN luôn giữ vững lòng kiên trì và đạt được những điều tuyệt vời!",
            "HỌ TÊN chúc bạn luôn tràn đầy năng lượng và sự quyết tâm trong năm học mới.",
            "Năm mới chúc bạn HỌ TÊN sẽ có những trải nghiệm học tập tuyệt vời tại Đại học Nông Lâm TP.HCM.",
            "Chúc bạn HỌ TÊN luôn khám phá được niềm đam mê mới trong học tập!",
            "HỌ TÊN chúc bạn đạt được mọi mục tiêu học tập và ngày càng tiến xa!",
            "Năm mới an khang, thịnh vượng và đầy cảm hứng học tập HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn tìm thấy niềm vui và ý nghĩa trong mỗi bài học!",
            "HỌ TÊN chúc bạn một năm học mới đầy cơ hội để phát triển bản thân!",
            "HỌ TÊN chúc bạn luôn gặt hái nhiều thành quả trong học tập và cuộc sống!",
            "Năm mới là cơ hội tuyệt vời để bạn HỌ TÊN học hỏi và khám phá!",
            "Chúc bạn HỌ TÊN luôn tự tin và mạnh mẽ để đối mặt với mọi thử thách!",
            "Năm 2025 sẽ là một năm đáng nhớ với những thành tựu rực rỡ HỌ TÊN!",
            "HỌ TÊN chúc bạn giữ vững đam mê và theo đuổi ước mơ học vấn của mình!",
            "Chúc bạn HỌ TÊN luôn có động lực và năng lượng để học tập mỗi ngày!",
            "Năm mới chúc bạn HỌ TÊN sẽ có những trải nghiệm học tập tuyệt vời!",
            "HỌ TÊN chúc bạn phát triển toàn diện và đạt được những thành công lớn!",
            "HỌ TÊN hãy để năm mới là một hành trình đầy thú vị và bổ ích!",
            "Chúc bạn HỌ TÊN luôn đạt điểm cao và hoàn thành mọi mục tiêu!",
            "Năm 2025 sẽ là năm của sự tiến bộ và thành công vượt bậc HỌ TÊN!",
            "HỌ TÊN chúc bạn học thật giỏi và luôn là niềm tự hào của gia đình!",
            "HỌ TÊN hãy bước vào năm mới với sự tự tin và khát vọng lớn lao!",
            "Chúc bạn HỌ TÊN luôn mạnh mẽ và bền bỉ trên con đường học vấn!",
            "HỌ TÊN hãy làm cho năm mới trở nên đặc biệt với những thành tựu đáng nhớ!",
            "Chúc bạn HỌ TÊN sẽ khám phá được niềm đam mê mới trong học tập!",
            "Năm mới chúc bạn HỌ TÊN luôn tiến xa hơn và đạt được mọi điều mong muốn!",
            "HỌ TÊN hãy để tri thức là người bạn đồng hành tuyệt vời trong năm 2025!",
            "Chúc bạn HỌ TÊN luôn có niềm vui và sự hứng khởi trong học tập!",
            "Năm mới chúc bạn HỌ TÊN thành công trong mọi mục tiêu đã đề ra!",
            "HỌ TÊN chúc bạn luôn tràn đầy nhiệt huyết và niềm tin vào bản thân!",
            "HỌ TÊN hãy làm cho mỗi ngày trong năm 2025 là một ngày học tập ý nghĩa!",
            "Chúc bạn HỌ TÊN đạt được những điều tuyệt vời nhất trong học tập!",
            "Năm mới an lành, hạnh phúc và đầy thành công HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn tìm thấy niềm vui trong từng bài học!",
            "Năm mới chúc bạn HỌ TÊN luôn có những ý tưởng sáng tạo và đột phá!",
            "HỌ TÊN chúc bạn vững vàng trên con đường học vấn đầy thử thách!",
            "Hãy để năm mới là một bước ngoặt đầy ý nghĩa trong sự nghiệp học tập HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn tự tin và khám phá những chân trời tri thức mới!",
            "Chúc bạn HỌ TÊN đạt được những ước mơ lớn trong năm 2025!",
            "Hãy để niềm đam mê học tập dẫn dắt bạn đến thành công HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn giữ vững tinh thần lạc quan và yêu đời!",
            "Năm mới hạnh phúc, thịnh vượng và đầy ý nghĩa HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn được truyền cảm hứng để học tập mỗi ngày!",
            "Hãy để năm 2025 là một chương mới đầy thành công trong cuộc đời bạn HỌ TÊN!",
            "Chúc bạn HỌ TÊN khám phá được những tiềm năng mới trong năm mới!",
            "Chúc bạn HỌ TÊN luôn kiên định và mạnh mẽ trên con đường chinh phục tri thức!",
            "Hãy để năm mới là một hành trình tuyệt vời với nhiều bài học quý giá HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn tràn đầy động lực và sự sáng tạo!",
            "Năm mới chúc bạn HỌ TÊN luôn được quý nhân phù trợ và gặp nhiều may mắn!",
            "Chúc bạn HỌ TÊN luôn tìm thấy những người bạn đồng hành tốt trong học tập!",
            "Hãy để năm mới là năm của sự bứt phá và thành công vượt bậc HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn học giỏi và nhận được sự công nhận từ mọi người!",
            "HỌ TÊN hãy sống và học tập hết mình để không hối tiếc trong năm mới!",
            "Chúc bạn HỌ TÊN khám phá được nhiều điều mới mẻ trong năm 2025!",
            "HỌ TÊN hãy luôn giữ vững tinh thần học hỏi và cầu tiến trong năm mới!",
            "Chúc bạn HỌ TÊN sẽ tìm thấy niềm vui trong từng thử thách của học tập!",
            "Hãy để tri thức dẫn dắt bạn đến những chân trời mới trong năm mới HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn thành công và hạnh phúc trong hành trình học vấn!",
            "Hãy biến năm mới thành một năm của sự phát triển vượt bậc HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn gặt hái được nhiều thành tựu trong học tập và cuộc sống!",
            "Hãy để năm 2025 là một năm đầy cảm hứng và ý nghĩa với bạn HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn tìm thấy niềm vui và ý nghĩa trong mỗi bài học!",
            "Năm mới chúc bạn HỌ TÊN luôn mạnh mẽ và kiên trì để vượt qua mọi thử thách!",
            "Hãy để năm mới là cơ hội để bạn HỌ TÊN học hỏi và phát triển bản thân!",
            "Chúc bạn HỌ TÊN luôn đạt được những kết quả tốt trong học tập và cuộc sống!",
            "Hãy tận hưởng từng khoảnh khắc của năm mới và học tập thật tốt HỌ TÊN!",
            "Chúc bạn HỌ TÊN sẽ khám phá được những tiềm năng mới trong năm 2025!",
            "Hãy để năm mới là một chương sách đầy ý nghĩa trong cuộc đời bạn HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn tràn đầy cảm hứng và sự quyết tâm trong học tập!",
            "Chúc bạn HỌ TÊN gặt hái được nhiều thành công trong mọi lĩnh vực bạn tham gia!",
            "Hãy để niềm đam mê và nỗ lực dẫn dắt bạn đến thành công HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn giữ vững tinh thần học hỏi và khám phá tri thức mới!",
            "Hãy để năm 2025 là một hành trình đầy thú vị và bổ ích cho bạn HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn đạt được những điều bạn mong muốn trong học tập và cuộc sống!",
            "Hãy để mỗi ngày trong năm mới là một ngày tràn đầy ý nghĩa và học hỏi HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn giữ vững sự nhiệt huyết và đạt được thành công lớn trong năm mới!",
            "Chúc bạn HỌ TÊN sẽ có một năm học tập hiệu quả và đạt được nhiều thành tích cao!",
            "Hãy để năm mới là năm của sự thành công và hạnh phúc với bạn HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn tiến xa hơn và đạt được những mục tiêu lớn trong học tập!",
            "Hãy để tri thức là người bạn đồng hành tuyệt vời trong năm mới của bạn HỌ TÊN!",
            "Chúc bạn HỌ TÊN luôn vững bước trên con đường học vấn và đạt được nhiều thành tựu lớn!",
            "HỌ TÊN chúc bạn một năm học mới đầy cảm hứng và sáng tạo!",
            "HỌ TÊN chúc bạn khám phá được nhiều điều thú vị trong học tập và cuộc sống tại trường.",
            "Chúc bạn HỌ TÊN luôn gặt hái nhiều thành công trong học tập và cuộc sống tại Đại học Nông Lâm TP.HCM.",
            "HỌ TÊN hãy để năm mới là một hành trình đầy thú vị và bổ ích!",
            "Chúc bạn HỌ TÊN luôn đạt điểm cao và hoàn thành mọi mục tiêu!",
            "HỌ TÊN hãy bước vào năm mới với sự tự tin và khát vọng lớn lao!",
            "Chúc bạn HỌ TÊN luôn mạnh mẽ và bền bỉ trên con đường học vấn!",
            "HỌ TÊN hãy làm cho năm mới trở nên đặc biệt với những thành tựu đáng nhớ!",
            "Chúc bạn HỌ TÊN sẽ khám phá được niềm đam mê mới trong học tập!",
            "HỌ TÊN chúc bạn luôn tìm thấy niềm vui và ý nghĩa trong học tập tại Đại học Nông Lâm TP.HCM!"
        ];

        function generateWish() {
            const fullName = document.getElementById('fullName').value;
            if (!fullName) {
                alert("Vui lòng nhập họ và tên của bạn!");
                return;
            }
            const randomWishIndex = Math.floor(Math.random() * wishes.length);
            const wishTemplate = wishes[randomWishIndex];
            const message = wishTemplate.replace('HỌ TÊN', fullName);
            const messageElement = document.getElementById('message');
            messageElement.textContent = message;
            showFireworks(messageElement);
            playSound();
        }

        // Function to show fireworks effect
        function showFireworks(element) {
            for (let i = 0; i < 20; i++) {
                const firework = document.createElement('div');
                firework.className = 'firework';
                firework.style.left = `${Math.random() * 100}%`;
                firework.style.top = `${Math.random() * 100}%`;
                element.appendChild(firework);
                setTimeout(() => {
                    firework.remove();
                }, 1000); // Remove firework after animation
            }
        }

        // Function to play sound
        function playSound() {
            const sound = document.getElementById('fireworkSound');
            sound.play();
        }
    </script>
</body>
</html>
