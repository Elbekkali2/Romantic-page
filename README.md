<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Romantic Page</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #111;
            color: #fff;
            text-align: center;
            margin: 0;
            padding: 0;
            overflow: hidden;
        }

        .container {
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        .visible {
            display: flex;
        }

        h1, p {
            margin: 20px;
        }

        button {
            padding: 10px 20px;
            margin: 10px;
            font-size: 16px;
            cursor: pointer;
        }

        /* Animation des cœurs */
        .heart {
            position: absolute;
            width: 20px;
            height: 20px;
            background: pink;
            clip-path: polygon(50% 0, 61% 13%, 85% 20%, 90% 50%, 75% 85%, 50% 100%, 25% 85%, 10% 50%, 15% 20%, 39% 13%);
            animation: fall 5s infinite ease-in-out, glow 3s infinite ease-in-out;
            opacity: 0.8;
        }

        @keyframes fall {
            0% {
                transform: translateY(-10vh) scale(0.8);
                opacity: 0.9;
            }
            50% {
                opacity: 1;
            }
            100% {
                transform: translateY(110vh) scale(1.2);
                opacity: 0;
            }
        }

        @keyframes glow {
            0%, 100% {
                background: pink;
                box-shadow: 0 0 10px rgba(255, 192, 203, 0.6);
            }
            50% {
                background: hotpink;
                box-shadow: 0 0 20px rgba(255, 105, 180, 0.8);
            }
        }
    </style>
</head>
<body>
    <!-- Étape 1 : Salutation -->
    <div id="step1" class="container visible">
        <h1 id="intro"></h1>
    </div>

    <!-- Étape 2 : Question -->
    <div id="step2" class="container">
        <h1 id="question"></h1>
        <button id="yes">Oui</button>
        <button id="no">Non</button>
    </div>

    <!-- Étape 3 : Curseur -->
    <div id="step3" class="container">
        <h1>Définis ton niveau d'amour !</h1>
        <input type="range" id="loveRange" min="0" max="100" value="50">
        <div id="percentageDisplay">50%</div>
        <button id="confirmLevel">Confirmer</button>
    </div>

    <!-- Étape 4 : Félicitation -->
    <div id="step4" class="container">
        <h1>Wa Aaaari chi Biyssa!</h1>
        <p>Nmout Elik ANASTASIA dyali hhhhhh 💖</p>
    </div>

    <!-- Cœurs animés -->
    <div id="heartsContainer"></div>

    <script>
        const texts = {
            intro: "Afeen a Hobbi Me3AK Yaassiine o db Ghansowlek brooojola",
            question: "Do u love me do you do you do uuuuu ?"
        };

        const step1 = document.getElementById("step1");
        const step2 = document.getElementById("step2");
        const step3 = document.getElementById("step3");
        const step4 = document.getElementById("step4");
        const introElement = document.getElementById("intro");
        const questionElement = document.getElementById("question");
        const noButton = document.getElementById("no");
        const yesButton = document.getElementById("yes");
        const loveRange = document.getElementById("loveRange");
        const percentageDisplay = document.getElementById("percentageDisplay");
        const confirmLevelButton = document.getElementById("confirmLevel");
        const heartsContainer = document.getElementById("heartsContainer");

        // Étape 1 : Salutation
        function typeWriter(element, text, callback) {
            let index = 0;
            function write() {
                if (index < text.length) {
                    element.textContent += text[index];
                    index++;
                    setTimeout(write, 50);
                } else if (callback) {
                    setTimeout(callback, 1000);
                }
            }
            write();
        }

        typeWriter(introElement, texts.intro, () => {
            step1.classList.remove("visible");
            step2.classList.add("visible");
            typeWriter(questionElement, texts.question);
        });

        // Étape 2 : Question
        noButton.addEventListener("mouseover", function () {
            const randomX = Math.random() * (window.innerWidth - noButton.offsetWidth);
            const randomY = Math.random() * (window.innerHeight - noButton.offsetHeight);
            noButton.style.position = "absolute";
            noButton.style.left = randomX + "px";
            noButton.style.top = randomY + "px";
        });

        yesButton.addEventListener("click", function () {
            step2.classList.remove("visible");
            step3.classList.add("visible");
        });

        // Étape 3 : Mise à jour du pourcentage
        loveRange.addEventListener("input", function () {
            percentageDisplay.textContent = loveRange.value + "%";
        });

        confirmLevelButton.addEventListener("click", function () {
            step3.classList.remove("visible");
            step4.classList.add("visible");
            startHeartsEffect();
        });

        // Effets des cœurs
        function startHeartsEffect() {
            function createHeart() {
                const heart = document.createElement("div");
                heart.className = "heart";
                heart.style.left = Math.random() * 100 + "vw";
                heart.style.animationDelay = Math.random() * 3 + "s";
                heart.style.width = Math.random() * 40 + 10 + "px"; // Taille aléatoire
                heart.style.height = heart.style.width;

                heartsContainer.appendChild(heart);

                // Supprimer le cœur après l'animation
                setTimeout(() => {
                    heart.remove();
                }, 5000);
            }

            // Générer plusieurs cœurs à intervalle régulier
            setInterval(createHeart, 200);
        }
    </script>
</body>
</html>
