# Задача 3

Потребно е за секој филм од листата од филмови movies да се направи p елемент со насловот и авторот на филмот и да се додаде на страната.
За приказ да се користи ul. Филмовите кои не се гледани да се обојат со црвено. 
Информациите потребни за филмовите се дадени во листа од објекти за секој филм која содржи: 
наслов, режисер и променлива за дали е гледан филмот.

  ![](img/image1.png)

# Решение:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>My movie list</h1>
<script>

    const movies = [ // низа од филмови со наслов, режисер и далиСеГледани
        {title: 'Goodfellas',
            director: 'Martin Scorsese',
            alreadyWatched: true
        },
        {title: 'Django Unchained',
            director: 'Quentin Tarantino',
            alreadyWatched: false
        },
        {title: 'Scarface',
            director: 'Brian de Palma',
            alreadyWatched: false
        }];

    let movieList = document.createElement('ul'); // креирање на unordered list

    for (let i = 0; i < movies.length; i++) { // итерирање низ филмовите
        let movieItem = document.createElement('li'); // креирање на елемент
        let movieDescription = document.createTextNode(movies[i].title + ' by ' + movies[i].director); // опис на филмот

        movieItem.appendChild(movieDescription);//се додава описот на филмот на соодветниот елемент

        if (!movies[i].alreadyWatched) { // ако е гледан филмот се бои црвено
            movieItem.style.color = 'red';
        }
        movieList.appendChild(movieItem);// се додава елементот на листата
    }

    document.body.appendChild(movieList);//се додава листата на документот
</script>

</body>
</html>
```