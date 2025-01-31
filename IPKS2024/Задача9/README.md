# Задача 9

Потребно е да се креира игра каде треба да се спарат сите парови на карти. 
Дадени се 6 парови на карти. Најпрво потребно е тие да се размешаат.
Потоа се ставаат на свое место.
При клик на картата таа се отвара.
Во случај да се отворени две карти кои се исти во истиот момент тие остануваат отворени, во 
спротивно повторно се затвораат. Играта завршува кога сите парови на карти ќе бидат спарени. 
Во тој случај се појавува на екран "Congratulations!"
Потребно е да се овозможи копче кое при клик повторно ќе генерира нова игра.

  ![](img/image1.png)
  *Изглед на играта при играње*
  
  (Картите кои се спарени остануваат отворени, тие кои не се добро спарени повторно се свртени наопаку)

  ![](img/image2.png)
  *Изглед на играта кога ќе заврши*

  # Решение:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Memory Card Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        h1 {
            color: #333;
            margin-bottom: 20px;
        }

        .card-container {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 20px; /* Increased the gap between cards */
        }

        .card {
            width: 100px;
            height: 150px;
            border: 2px solid #000;
            cursor: pointer;
            background: url('https://pixabay.com/vectors/card-game-deck-of-cards-card-game-48980/') no-repeat;
            background-size: cover;
            transition: transform 0.3s ease;
        }

        .card:hover {
            transform: scale(1.05);
        }

        .btn {
            opacity: 0;
            background-color: #4caf50;
            color: white;
            border: none;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin-top: 20px;
            cursor: pointer;
            transition: opacity 0.3s ease;
        }

        .btn:hover {
            opacity: 0.8;
        }
    </style>
</head>
<body>
<button class="btn">Play again!</button>

<h1>Memory Card Game</h1>
<div id="gameBoard" class="card-container"></div>

<script>
    const cards = [ // низа од 6 пара од различни карти
        'https://cdn.pixabay.com/photo/2013/07/13/13/46/playing-card-161494_640.png', 'https://cdn.pixabay.com/photo/2013/07/13/13/46/playing-card-161494_640.png',
        'https://cdn.pixabay.com/photo/2013/07/13/13/46/playing-card-161495_640.png', 'https://cdn.pixabay.com/photo/2013/07/13/13/46/playing-card-161495_640.png',
        'https://cdn.pixabay.com/photo/2014/04/03/10/54/playing-card-311679_640.png', 'https://cdn.pixabay.com/photo/2014/04/03/10/54/playing-card-311679_640.png',
        'https://cdn.pixabay.com/photo/2013/07/13/13/46/playing-card-161493_640.png', 'https://cdn.pixabay.com/photo/2013/07/13/13/46/playing-card-161493_640.png',
        'https://cdn.pixabay.com/photo/2015/08/11/11/56/hearts-884177_640.png', 'https://cdn.pixabay.com/photo/2015/08/11/11/56/hearts-884177_640.png',
        'https://cdn.pixabay.com/photo/2015/08/11/11/56/spades-884170_640.png', 'https://cdn.pixabay.com/photo/2015/08/11/11/56/spades-884170_640.png'
    ];
    let flippedCards = []; // низа од карти кои се свртени
    let matchedCards = []; // низа од карти кои се спарени

    function createGameBoard() { // функција за креирање на HTML елемент за секоја карта
        const gameBoard = document.getElementById('gameBoard');


        shuffle(cards); // мешање на картите

        cards.forEach((card, index) => { // креирање на елемент и додавање на секој елемент и додавање на gameBoard
            const cardElement = document.createElement('div');
            cardElement.classList.add('card');
            cardElement.setAttribute('data-index', index);
            cardElement.addEventListener('click', flipCard);
            gameBoard.appendChild(cardElement);
        });
    }

    function shuffle(array) {//мешање на картите од array низата
        for (let i = array.length - 1; i > 0; i--) { // for кој почнува од последниот елемент
            const j = Math.floor(Math.random() * (i + 1)); // рандом број од 0 до i
            [array[i], array[j]] = [array[j], array[i]]; // менување на вредноста на i и ј
        }
    }

    function flipCard() {
        if (flippedCards.length < 2 && !flippedCards.includes(this)) {
            // овој if проверува дали две карти се превртени и дали картата this
            //е веќе превртена
            this.style.backgroundImage = `url('${cards[this.dataset.index]}')`; // се менува лицето на картата
            flippedCards.push(this); // се става во низата на превртени карти
            if (flippedCards.length === 2) { // ако се превртени 2 карти
                // се дава на играчот една секунда да ја види картата која се превртува
                setTimeout(checkMatch, 1000);
            }
        }
    }

    const body = document.querySelector('body');
    const title = document.querySelector('h1');
    const button = document.querySelector('.btn');

    function checkMatch() {// функција која проверува дали 2 карти се исти
        const card1 = flippedCards[0];
        const card2 = flippedCards[1];
        if (cards[card1.dataset.index] === cards[card2.dataset.index]) { // го споредува url-то на двете карти
            matchedCards.push(card1, card2);//ако е исполнето се ставаат во низата
            if (matchedCards.length === cards.length) { // ако се спарени сите карти
                body.style.backgroundColor = '#4caf50'; // се менува позадината и се прикажува порака
                title.textContent = 'Congratulations!';
                button.style.opacity = 1;
            }
        } else { // ако не се исти двете карти се превртуваат
            card1.style.backgroundImage = 'url("card-back.png")';
            card2.style.backgroundImage = 'url("card-back.png")';
        }
        flippedCards = []; // се ресетира низата
    }

    button.addEventListener('click', function (e) { // кога ќе се кликне копчето Play again
        e.preventDefault();
        body.style.backgroundColor = '#f4f4f4'; // се враќа позадината
        title.textContent = 'Memory Card Game'; // се враќа насловот
        button.style.opacity = 0; // се крие копчето Play again
        document.querySelectorAll('.card').forEach(card => card.remove());// се отсрануваат сите елементи од GameBoard
        createGameBoard(); // се креира нова игра
    });

    window.onload = createGameBoard;
</script>
</body>
</html>
```
