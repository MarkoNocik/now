# Задача 8

Потребно е да се креира игра каде треба да се погоди број од 1 до 10
Играчот на играта треба да го погодува бројот се додека не е истиот со претходно генерираниот број. 
Се генерира еден рандом број помеѓу 1 и 10.
Играчот внесува број во полето.
Моменталниот резултат на играчот е прикажан од страна. 
Резултатот е всушност бројот на погодоци потребни на играчот да го погоди бројот.
При внес на број се појавува порака дали рандом генерираниот број е поголем или помал од внесениот.     
Од страната се чува и highscore односно најдобриот резултат од сите погодоци.
При погодување на бројот: се појавува порака која не известува дека сме погодиле и завршува играта. По завршување може да се кликне копчето Повторно! преку кое ќе почнете со нова игра.

  ![](img/image1.png)
  *Изглед на играта и поставеност на работите додека се игра*
  
  (на местото на "Почнете со погодување..." при клик на копчето Провери! треба да се прикаже пораката за тоа дали внесениот број е помал или поголем од генерираниот)
  
  ![](img/image2.png)
  *Изглед на играта кога играчот ќе го погоди бројот*

# Решение: 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <link rel="stylesheet" href="style.css" />
    <title>Погоди го бројот!</title>
</head>
<body>
<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    html {
        font-size: 62.5%;
        box-sizing: border-box;
    }

    body {
        font-family: 'Courier New', Courier, monospace;
        color: #eee;
        background-color: #222;
    }

    /* LAYOUT */
    header {
        position: relative;
        height: 15vh;
        border-bottom: 7px solid #eee;
        text-align: center;
    }

    main {
        height: 85vh;
        color: #eee;
        display: flex;
        align-items: center;
        justify-content: space-around;
    }

    .left {
        width: 30rem;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .right {
        width: 30rem;
        font-size: 2rem;
    }

    /* ELEMENTS STYLE */
    h1 {
        font-size: 3rem;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    .number {
        background: #eee;
        color: #333;
        font-size: 6rem;
        width: 15rem;
        padding: 3rem 0rem;
        text-align: center;
        display: none;
    }

    .between {
        font-size: 1.4rem;
        position: absolute;
        top: 2rem;
        right: 2rem;
    }

    .again {
        position: absolute;
        top: 2rem;
        left: 2rem;
    }

    .guess {
        background: none;
        border: 4px solid #eee;
        font-family: inherit;
        color: inherit;
        font-size: 3rem;
        padding: 1.5rem;
        width: 15rem;
        text-align: center;
        display: block;
        margin-bottom: 3rem;
    }

    .btn {
        border: none;
        background-color: #eee;
        color: #222;
        font-size: 2rem;
        font-family: inherit;
        padding: 1.5rem 2rem;
        cursor: pointer;
    }

    .btn:hover {
        background-color: #ccc;
    }

    .message {
        margin-bottom: 4rem;
        height: 3rem;
    }

    .label-score {
        margin-bottom: 2rem;
    }
</style>
<header>
    <h1>Погоди го бројот!</h1>
    <p class="between">(Помеѓу 1 и 10)</p>
    <button class="btn again">Повторно!</button>
    <div class="number">?</div>
</header>
<main>
    <section class="left">
        <input type="number" class="guess" />
        <button class="btn check">Провери!</button>
    </section>
    <section class="right">
        <p class="message">Почнете со погодување...</p>
        <p class="label-score">Резултат: <span class="score">10</span></p>
        <p class="label-highscore">
            Највисок резултат: <span class="highscore">0</span>
        </p>
    </section>

</main>
<script >
    let secretNumber = Math.trunc(Math.random() * 10) + 1; // декларирање на random број од 1 до 10
    let score = 10; // моментален score
    let highscore = 0;

    const displayMessage = function (message) { // прикажување пораки
        document.querySelector('.message').textContent = message;
    };

    document.querySelector('.check').addEventListener('click', function () { //при кликање на копчето check
        const guess = Number(document.querySelector('.guess').value);// се споредува вредноста на
        console.log(guess, typeof guess); // корисникот и random бројот

        if (!guess) { //ако не е внесен број
            displayMessage('Не е внесен број!');
        } else if (guess === secretNumber) { // во случај да се пофоди бројот
            displayMessage('Погодивте!'); // се прикажува соодветна порака и се менува стилот
            document.querySelector('.number').textContent = secretNumber;

            document.querySelector('body').style.backgroundColor = '#60b347';
            document.querySelector('.number').style.width = '30rem';

            if (score > highscore) { // update на highscore
                highscore = score;
                document.querySelector('.highscore').textContent = highscore;
            }
        } else if (guess !== secretNumber) { // ако не е погоден бројот
            if (score > 1) {
                displayMessage(guess > secretNumber ? ' Премногу високо!' : 'Премногу ниско!');
                // се прикажува соодветна порака ако е внесен поголем или помал број од random бројот
                score--;// се намалува score при секое погодување
                document.querySelector('.score').textContent = score;
            } else { // во случај да не се погоди бројот
                displayMessage('Изгубивте!');
                document.querySelector('.score').textContent = 0;
            }
        }

    });

    document.querySelector('.again').addEventListener('click', function () {// ако се кликне Повторно!
        score = 10;// се ресетира score
        secretNumber = Math.trunc(Math.random() * 10) + 1; // се креира нов random број

        displayMessage('Почнете со погодување...'); // ресетирање на вредностите
        document.querySelector('.score').textContent = score;
        document.querySelector('.number').textContent = '?';
        document.querySelector('.guess').value = '';

        document.querySelector('body').style.backgroundColor = '#222';
        document.querySelector('.number').style.width = '15rem';
    });

</script>
</body>
</html>
```