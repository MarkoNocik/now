# Задача 10

Потребно е да се креира веб сајт за e-commerce
Пред да се влезе се дефинира корисник (user) кој ќе има username, password и balance (средства со кој ќе располага)

**Креирање на продукти:**
Секој продукт има свое име, број на такви продукти во продавницата и своја цена.

**Влезна страница**:
На влезната страница се прикажува поле во кое се внесува соодветниот username и password за тој user.
Не е дозволен влез за неточен  username или password.
Со кликање на копчето login се влегува во страницата во која се продаваат продуктите.

**Страната на продавницата**:  
По кликање на копчето login се влегува во страницата.
На страницата се прикажани сите продукти.
Во горниот десен агол стои balance односно средствата со кој располага корисникот.
При кликање на било кој од продуктите се појавува pop-up во кој:
Го пишува името на продуктот, неговата цена и во горниот десен агол има копче за излез од pop-up-от и најдолу има копче buy.
При кликање на копчето buy се купува одреден производ и се става во *Inventory*
Важно е да се напомене дека ако корисникот нема доволно средства за одреден продукт нема да може да го купи.
   
Во *Inventory*  стојат сите купени продукти и количината што е купена од одреден продукт.
Приказот на *Inventory* може да се види со кликање на копчето Cart
При кликање на копчето **Logout** се враќате на почетниот екран каде повторно треба да се внесат соодветниот username и password за тој user.

![](img/image1.png)

 *Изглед на log-in формата*
 

![](img/image2.png)
*Изглед на страницата по влез*



![](img/image3.png)
*Изглед на pop-up при кликање на некој од продуктите*



![](img/image4.png)

*Изглед на Inventory*



![](img/image5.png)
*При кликање на копчето Cart може да се види Inventory*



![](img/image6.png)
*При кликање на копчето Logout се излегува од страницата*

# Решение: 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>E-commerce Shop</title>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
            href="https://fonts.googleapis.com/css2?family=Roboto+Flex:opsz@8..144&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap"
            rel="stylesheet"
    />
    <style>* {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: "Roboto";
        scroll-behavior: smooth;
    }

    body {
        background-color: #f5f5f5;
    }

    .logo {
        text-align: center;
        margin-top: 20px;
    }

    .loginContainer {
        margin: 100px auto;
        max-width: 600px;
        background-color: #fff;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
    }

    .title {
        text-align: center;
        margin-bottom: 20px;
    }

    .formContainer {
        background: linear-gradient(to right, #cbfab5, #94ff66);
        padding: 30px;
        border-radius: 10px;
        border: 1px solid #ddd;
    }

    .formContainer h3 {
        text-align: center;
        margin-bottom: 20px;
    }

    .formContainer label {
        margin-bottom: 8px;
        color: #333;
    }

    .formContainer input[type="text"],
    .formContainer input[type="password"] {
        width: 100%;
        padding: 10px;
        margin-bottom: 20px;
        border: 1px solid #ddd;
        border-radius: 5px;
    }

    .formContainer button {
        width: 100%;
        padding: 10px;
        background-color: #000000;
        color: #fff;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        transition: 1s;
    }

    .formContainer button:hover {
        background-color: #ffffff;
        color: #000000;
    }

    .mainContainer {
        display: none;
        max-width: 1200px;
        margin: 0 auto;
        padding: 20px;
    }

    .navbar {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background: linear-gradient(to right, #cbfab5, #94ff66);
        padding: 30px;
        color: #000000;
        padding: 15px;
        border-radius: 8px;
        margin-bottom: 20px;
    }

    .navbar ul {
        list-style-type: none;
        display: flex;
    }

    .navbar ul li {
        margin-right: 20px;
        position: relative;
    }

    .navbar ul li a {
        text-decoration: none;
        color: #000000;
        position: relative;
    }
    .navbar ul li a::after {
        content: ""; 
        position: absolute; 
        left: 0;
        bottom: -5px; 
        width: 100%; 
        height: 2px; 
        background-color: #000000; 
        transition: all 0.3s ease; 
        transform: scaleX(0); 
    }
    .navbar ul li a:hover::after {
       
        transform: scaleX(1); 
    }

    .userBlock {
        background-color: rgba(255, 255, 255, 0.668);
        padding: 10px 20px;
        border-radius: 8px;
    }
 

    .productGrid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(500px, 1fr));
        gap: 20px;
    }

    .productCard {
        background-color: #fff;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        text-align: center;
    }
    .productCard:hover {
        cursor: pointer;
        transform: scale(1.1);
    }
    .popUp {
        display: none;
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: rgba(255, 255, 255, 0.9);
        padding: 20px 50px;
        border-radius: 10px;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
        z-index: 1000; 
    }

    .popUpContent {
        text-align: center;
    }

    .popUpContent h2 {
        margin: 5px 0;
    }
    .popUpContent p {
        margin: 5px 0;
    }
    .popUpContent button {
        margin: 5px 0;
    }

    .closePopUp {
        position: absolute;
        top: 10px;
        right: 10px;
        font-size: 20px;
        cursor: pointer;
    }

    .closeButton {
        background-color: #000000;
        color: #ffffff;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s;
    }

    .closeButton:hover {
        background-color: #ffffff;
        color: #000000;
    }
    .wp {
        margin: 50px 0;
    }
    .inventorySection {
        margin-top: 150px;
        padding: 20px;
        background-color: #f5f5f5;
    }

    .inventoryHeading {
        text-align: center;
        margin-bottom: 20px;
    }

    .inventoryGrid {
        display: flex;
        flex-direction: column;
        gap: 20px;
    }

    .inventoryCard {
        background-color: #fff;
        padding: 10px 20px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        text-align: center;
        display: flex;
        justify-content: space-between;
    }

    .inventoryCard button {
        background-color: #ff0000; 
        color: #fff;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s;
        margin: 0 10px;
    }

    .inventoryCard button:hover {
        background-color: #ff6666; 
    }

    .inventoryCard p {
        margin-top: 10px;
    }

    .inventoryCard .productName {
        font-weight: bold;
    }

    .inventoryCard .sellButton {
        margin-top: 10px;
    }
    .sellBlock {
        display: flex;
        justify-content: space-between;
        text-align: center;
        align-items: center;
    }
    </style>
</head>
<body>
<h1 class="logo">SHOPIFY</h1>
<div class="loginContainer">
    <h1 class="title">Welcome to Our Shop</h1>
    <form class="formContainer">
        <h3>Login</h3>
        <label for="username">Username</label>
        <input type="text" id="username" required />
        <label for="password">Password</label>
        <input type="password" id="password" required />
        <button type="submit" class="submit">Login</button>
    </form>
</div>
<div class="mainContainer">
    <nav class="navbar">
        <ul>
            <li><a href="#">Home</a></li>
            <li><a href="#">Products</a></li>
            <li><a href="#inventory">Cart</a></li>
            <li><a href="#">Logout</a></li>
        </ul>
        <div class="userBlock">Username</div>
    </nav>
    <section class="productGrid">
        <!-- Product cards -->
        <div class="productCard">Product 1</div>
        <div class="productCard">Product 2</div>
        <div class="productCard">Product 3</div>
        <div class="productCard">Product 4</div>
        <div class="productCard">Product 5</div>
        <div class="productCard">Product 6</div>
        <div class="productCard">Product 7</div>
        <div class="productCard">Product 8</div>
        <div class="productCard">Product 9</div>
        <div class="productCard">Product 10</div>
    </section>
    <div class="popUp">
        <div class="popUpContent">
            <span class="closePopUp">&times;</span>
            <h2 class="wt">Product Details</h2>
            <p class="wd">This is a sample product description.</p>
            <button class="closeButton">Buy</button>
        </div>
    </div>
    <section class="inventorySection" id="inventory">
        <h2 class="inventoryHeading">Inventory</h2>
        <div class="inventoryGrid">
            <!-- <div class="inventoryCard">
              <p>MARKO DISKOCAR</p>
              <div class="sellBlock">
                <p>x3</p>
                <button class="sellButton">Sell</button>
              </div>
            </div> -->
        </div>
    </section>
</div>

<script>
    const user1 = { // корисник со username, password i balance
        name: "Marko",
        password: "ipks2023",
        balance: 100,
    };
    const product1 = { // продукти со име, цена и број парчиња од тој продукт
        name: "product 1",
        price: 10,
        quantity: 1,
    };
    const product2 = {
        name: "product 2",
        price: 20,
        quantity: 2,
    };
    const product3 = {
        name: "product 3",
        price: 30,
        quantity: 3,
    };
    const product4 = {
        name: "product 4",
        price: 40,
        quantity: 4,
    };
    const product5 = {
        name: "product 5",
        price: 50,
        quantity: 5,
    };
    const product6 = {
        name: "product 6",
        price: 60,
        quantity: 6,
    };
    const product7 = {
        name: "product 7",
        price: 70,
        quantity: 7,
    };
    const product8 = {
        name: "product 8",
        price: 80,
        quantity: 8,
    };
    const product9 = {
        name: "product 9",
        price: 90,
        quantity: 9,
    };
    const product10 = {
        name: "product 10",
        price: 100,
        quantity: 10,
    };

    const users = [user1]; // низа од корисници
    const products = [ // низа од продукти
        product1,
        product2,
        product3,
        product4,
        product5,
        product6,
        product7,
        product8,
        product9,
        product10,
    ];
    const orders = []; // низа од нарачки

    const labelUsername = document.querySelector("#username");
    const labelPassword = document.querySelector("#password");
    const btnSubmit = document.querySelector(".submit");
    const userBlock = document.querySelector(".userBlock");
    const formContainer = document.querySelector(".loginContainer");
    const containerMain = document.querySelector(".mainContainer");
    const iconClosePopUp = document.querySelector(".closePopUp");
    const windowPopUp = document.querySelector(".popUp");
    const cards = [...document.querySelectorAll(".productCard")];
    const windowTitle = document.querySelector(".wt");
    const windowDescription = document.querySelector(".wd");
    const buttonLogout = document.querySelector(
        "body > div.mainContainer > nav > ul > li:nth-child(4) > a"
    );
    const buttonBuy = document.querySelector(".popUpContent button");
    const gridInventory = document.querySelector(".inventoryGrid");
    const cardsInventory = document.querySelectorAll(".inventoryCard");

    const updateUI = () => { //Функција која го менува корисничкиот интерфејс врз основа на различни настани.
        formContainer.style.display = "none"; // ја крие login формата
        containerMain.style.display = "block"; // се прикажува containerMain
        userBlock.textContent = `Balance: ${user1.balance.toFixed(2)}$`; // се прикажуват парите на корисникот
    };

    btnSubmit.addEventListener("click", (e) => { // при клик на login
        e.preventDefault();
        const username = labelUsername.value;
        const password = labelPassword.value;
        if (username === user1.name && password === user1.password) { // проверува дали внесениот username и password
            // се точни
            labelUsername.value = "";// ги ресетира вредностите
            labelPassword.value = "";
            labelPassword.blur(); // прави blur на password
            updateUI();
        }
    });

    const displayPopUp = (name) => { // при клик на одреден продукт
        const product = products.find((p) => p.name === name.toLowerCase()); // го бара продуктот во низата
        windowTitle.textContent = product.name.toUpperCase(); // го става насловот и описот на продуктот
        windowDescription.textContent = `${product.price.toFixed(2)}$`;
        windowPopUp.style.display = "block";
    };

    iconClosePopUp.addEventListener("click", () => { // при исклучување на PopUp-от
        windowPopUp.style.display = "none";
    });
    cards.forEach((card) => { // за секоја карта при клик се повикува displayPopUp функција
        card.addEventListener("click", () => {
            displayPopUp(card.textContent);
        });
    });
    buttonLogout.addEventListener("click", () => { // при клик на Logout копчето
        formContainer.style.display = "block";//Кога ќе се кликне, го крие главниот контејнер и
        // ја прикажува формата за најавување
        containerMain.style.display = "none";
    });

    const displayInventory = (orders) => { // приказ на Inventory
        gridInventory.innerHTML = "";
        const setOrders = new Set(orders);
        setOrders.forEach((o) => { // итерира низ различните продукти (преку set)
            const counter = orders.filter((p) => p.name === o.name).length;
            // за секој продукт го калкулира квантитетот односно бројот на купени
            // продукти од ист тип
            const html = `<div class="inventoryCard">
    <p>${o.name}</p>
    <div class="sellBlock">
      <p>x${counter}</p>
      <button class="sellButton">Sell</button>
    </div>
  </div>`;
            gridInventory.insertAdjacentHTML("afterbegin", html); // го додава
        });
    };

    buttonBuy.addEventListener("click", () => { // при клик на копчето Buy
        const name = windowTitle.textContent.toLowerCase();
        const product = products.find((p) => p.name === name);

        if (user1.balance >= product.price) { // ако корисникот има пари за да го купи продуктот
            orders.push(products.find((p) => p.name === name));
            console.log(orders);
            user1.balance -= product.price;
            const counter = orders.filter((p) => p.name === product.name).length;
            // Ако корисникот има доволно пари, се додава производот во низата на нарачки, се одзема цената
            // на производот од салдото на корисникот и се ажурира приказот на залихи и интерфејсот
            if (counter > 1) {

                updateUI();
                displayInventory(orders);
                windowPopUp.style.display = "none";
            } else {
                displayInventory(orders);
                updateUI();
                windowPopUp.style.display = "none";
            }
        } else { // во случај корисникот да нема доволно средства
            alert("You do not have enough money to buy this product!");
        }
    });

</script>
</body>
</html>
```

