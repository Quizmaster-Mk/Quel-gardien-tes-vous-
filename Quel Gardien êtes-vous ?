<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quel Gardien de la Galaxie êtes-vous ?</title>
  <style>
    body {
      font-family: 'Courier New', monospace;
      background-color: #0b0c10;
      color: #fff;
      margin: 0;
      padding: 20px;
      text-align: center;
    }

    h1 {
      color: #00bcd4;
      text-shadow: 2px 2px 5px #00796b;
      font-size: 40px;
      margin-bottom: 20px;
    }

    img.logo {
      max-width: 200px;
      margin-bottom: 20px;
    }

    .question {
      margin: 20px 0;
      background-color: #1f2833;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 188, 212, 0.7);
    }

    .options button {
      background-color: #45a29e;
      color: #0b0c10;
      padding: 10px 20px;
      border: none;
      margin: 5px;
      font-size: 18px;
      cursor: pointer;
      border-radius: 5px;
      transition: all 0.3s ease;
    }

    .options button:hover {
      background-color: #66fcf1;
      transform: scale(1.1);
    }

    .result {
      background-color: #1f2833;
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      display: none;
      box-shadow: 0 0 10px rgba(0, 188, 212, 0.7);
    }

    .score {
      font-size: 18px;
      margin-top: 10px;
      color: #00bcd4;
    }
  </style>
</head>
<body>
  <img class="logo" src="https://zupimages.net/up/25/15/do18.png" alt="Logo Gardiens">
  <h1>Quel Gardien de la Galaxie êtes-vous ?</h1>

  <div id="quiz-container">
    <div class="question" id="question-container">
      <h2 id="question-text"></h2>
      <div class="options" id="options-container"></div>
    </div>
  </div>

  <div class="result" id="result-container">
    <h2>Vous êtes...</h2>
    <p id="result-text"></p>
    <p class="score">Votre résultat est basé sur vos choix !</p>
    <button onclick="startQuiz()">Recommencer le quiz</button>
  </div>

  <script>
    const questions = [
      { question: "Quel est votre passe-temps préféré ?", options: ["Écouter de la musique rétro", "Combattre", "Méditer", "Faire des blagues"], result: [0, 1, 2, 3] },
      { question: "Comment réagissez-vous au danger ?", options: ["Foncer tête baissée", "Analyser la situation", "Protéger les autres", "Lancer une punchline"], result: [4, 5, 6, 7] },
      { question: "Quel est votre plus grand défaut ?", options: ["Trop arrogant", "Trop brutal", "Trop mystérieux", "Trop bavard"], result: [8, 9, 0, 1] },
      { question: "Un mot pour vous définir ?", options: ["Loyal", "Imprévisible", "Sage", "Dingue"], result: [2, 3, 4, 5] },
      { question: "Votre arme de choix ?", options: ["Blasters", "Hache", "Pouvoir mental", "Armes biologiques"], result: [6, 7, 8, 9] },
      { question: "Votre plus grand rêve ?", options: ["Sauver la galaxie", "Être respecté", "Retrouver votre famille", "Être libre"], result: [0, 1, 2, 3] },
      { question: "Votre pire ennemi ?", options: ["L’autorité", "Les traîtres", "Vous-même", "Personne, je m’aime !"], result: [4, 5, 6, 7] },
      { question: "Un mot pour décrire votre équipe ?", options: ["Famille", "Bordélique", "Unique", "Incroyable"], result: [8, 9, 0, 1] },
      { question: "Quel type de musique aimez-vous ?", options: ["Années 70/80", "Rock", "Ambiante", "Tout ce qui bouge"], result: [2, 3, 4, 5] },
      { question: "Votre meilleure qualité ?", options: ["Charismatique", "Féroce", "Calme", "Loyal"], result: [6, 7, 8, 9] }
    ];

    const characters = [
      { name: "Star-Lord (Peter Quill)", description: "Charismatique, passionné de musique rétro et toujours prêt à sauver la galaxie avec style." },
      { name: "Drax le Destructeur", description: "Fonceur, littéral et loyal. Il n'a peur de rien et aime les bonnes bastons." },
      { name: "Groot", description: "Calme, protecteur, et doté d’un grand cœur. Il dit peu de mots, mais ils comptent." },
      { name: "Rocket Raccoon", description: "Sarcastique, inventif, et prêt à tout pour ses amis. Un génie du bricolage." },
      { name: "Gamora", description: "Sérieuse, stratège et puissante, elle cherche la rédemption pour son passé." },
      { name: "Mantis", description: "Empathique et douce, elle voit le monde avec innocence mais n'est pas à sous-estimer." },
      { name: "Nebula", description: "Froide mais déterminée, elle apprend à trouver sa place dans l’équipe." },
      { name: "Yondu", description: "Dur à cuire au cœur tendre, il n’hésite pas à se sacrifier pour ceux qu’il aime." },
      { name: "Cosmo", description: "Un chien télépathe russe avec un cœur d’or et beaucoup d’humour." },
      { name: "Adam Warlock", description: "Puissant et mystérieux, il cherche encore sa voie dans l’univers." }
    ];

    let currentQuestion = 0;
    let userAnswers = [];

    function startQuiz() {
      currentQuestion = 0;
      userAnswers = [];
      document.getElementById('result-container').style.display = 'none';
      document.getElementById('quiz-container').style.display = 'block';
      showQuestion();
    }

    function showQuestion() {
      const question = questions[currentQuestion];
      document.getElementById('question-text').innerText = question.question;

      const optionsContainer = document.getElementById('options-container');
      optionsContainer.innerHTML = '';

      question.options.forEach((option, index) => {
        const button = document.createElement('button');
        button.innerText = option;
        button.onclick = () => {
          userAnswers.push(question.result[index]);
          currentQuestion++;
          if (currentQuestion < questions.length) {
            showQuestion();
          } else {
            showResult();
          }
        };
        optionsContainer.appendChild(button);
      });
    }

    function showResult() {
      const resultIndex = userAnswers.reduce((a, b) => a + b, 0) % characters.length;
      const result = characters[resultIndex];

      document.getElementById('result-text').innerText = `${result.name} - ${result.description}`;
      document.getElementById('quiz-container').style.display = 'none';
      document.getElementById('result-container').style.display = 'block';
    }

    startQuiz();
  </script>
</body>
</html>
