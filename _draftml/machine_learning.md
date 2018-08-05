---
topic: "Collaborative Filtering "
desc: " A Quick Look at Stalking People Online"
---

<h1> Topics Covered in this DOPE GUIDE </h1>
Manhattan distance<br>
Euclidean distance<br>
Minkowski distance<br>
Pearson Correlation Coefficient<br>
Cosine similarity<br>
Implementing k-nearest neighbors in Python<br>

<h1> Now to get into some real cool stuff, familia </h1>
<img src='http://static1.zipso.net/wp-content/uploads/2014/03/doge-mining.jpg' style="width: 400px">
<p> A Data Mining Expert </p>

<h1> So what is Collaborative Filtering, anyway, other than "just a data mining technique"? </h1>

<p> A recommendation system wherein I collaborate with friends to filter out your online information for pertinent data and then use it to stalk your movements online. JKJKJKJKJKJKJK LMAO!!! </p>

<p> Collaborative Filtering is a recommendation system where I use people with similar interests to recommend some sort of data, like a movie. In this way, the data points in your set "collaborate" to produce some sort of prediction. Suppose I need to recommend you an album to listen to on Spotify: I would go through the other users on Spotify to find one that is similar to you in music tastes. Once I find this person, I can look at music that they listen to that you don't and recommend you those artists.</p>

<p> The following guide will go over some of those oh-so-sweet details on how this process works. </p>

<h1> BUT HOW DO WE MEASURE SIMILARITY BASED-GOD MAXWELL? </h1>
<h2> Manhattan Distance </h2>

<p> Imagine yourself and Harambe the gorilla, rating your preferences on different movies. Harambe, of course, rates Free Willy a 10/10 and rates Pulp Fiction a solid 8/10. You, on the other hand, rate Pulp Fiction a solid 10/10, and Free Willy a 3/10. What is the simplest manner in which we can measure your similarity to this majestic primitive? Distance. We would plot your opinions on Free Willy on the x axis, and your opinions on Pulp Fiction on the y axis, and then calculate how many blocks a cab driver in matthattan would have to move in order to get from Harambe to You.</p>

<p>| x1 - x2| + | y1 - y2 |</p>

<p>| 10 - 3 | + | 8 - 10 | = 9 </p>

<p> And so your manhattan distance from dank memes is a 9. Now lets talk about Rare Pepe's. Pepe rates Free Will a 0/10, and feels meh about Pulp Fiction, rating it a 7/10. His manhattan distance from you is therefore</p>

<p>| 3 - 0 | + | 10 - 7 | = 6 </p>

<p> Thus you are closer to Pepe than you are to Harambe. This is the simplest form of measuring similarity </p>

<h2> Euclidean Distance and the Illuminati </h2>

<p> So, everyone knows that the Illuminati are watching our every move, and to perfect the measure of similarity, they forced Pythagoras to churn out the Famous  triangular theorem, creating the concept of Euclidean Distance. You will hopefully have learned this in high school and I will be killed if I tell you more, but it is pretty straight forward that measuring the exact distance between two points will give you a slightly more accurate representation of similarity. Here's the equation: </p>

<p> sqrt( (x1 - x2)^2 + (y1 - y2)^2 ) </p> 

<h2> WE NEED TO GO DEEPER. </h2>

<h1> DEEPER. </h1>

<h1> WE MUST GO DEEPER INTO HIGHER DIMENSIONS. </h1>

<p> Thinking of how the concepts of Manhattan Distance and Euclidean Distance apply when we have ratings of more than one movie is relatively straight-forward. Instead of just x and y coordinates, we have x, y, and z, coordinates, a 3-D distance, and with four movies, we have x, y, z, and theta coordinates, and so forth. The associated measures of distance change intuitively. </p>

<p> Manhattan Distance becomes | x1 - x2 | + | y1 - y2 | + | z1 - z2 | + ... </p>

<p> Euclidean Distance becomes sqrt( (x1 - x2)^2 + (y1 - y2)^2 + (z1 - z2)^2 + ... ) </p>

<p> And boom, you're a space explorer mathmatician extrodinate working in 5 dimensional space. E. Z. P. Z. MIND FREKING BLOWN GAME OVER SHOW DONE WE"RE OUT OF HERE. BEAUTIFUL. AMAZING. 10/10 BEST NEW MATHEMATICAL CONCEPT. </p>

<img src='https://pbs.twimg.com/media/CbSoeXOVAAAkASg.png' style="width: 600px">

<h1> BUT WHAT IS WRONG WITH THIS PICTURE? </h1>

<h1> WAIT, NO, NOT THE PICTURE ABOVE. WHAT IS WRONG WITH THE METHODS OF CALCULATING EUCLIDEAN AND MANHATTAN DISTANCE? </h1>

<p> This one is a little bit harder to explain without giving a specific example. Imagine trying to apply these measurements of similarity when there are a large number of ratings. Users will have incredibly different overlaps. I might have rated 5 movies, and Harambe has rated the same five, while Pepe has rated two of the ones that I've rated and 3 movies that I have never seen. Now, when we try to draw a comparison between me, harambe, and Pepe, there may be a large skew in the results. My distance to harambe may be larger simply because of the larger number of dimensions between us, even if in reality we are closer. This, as well as many other problems, can arise. Bad news, and it is actively being researched as we speak. We will talk more about this later, hopefully, and adress ways in which his bias may be corrected. For now, let us discuss the generalized distance measurement (its really freaking cool, though the math is a little less intuitive.)</p>

<h1> NEVER PANIC </h1>

<p> Math is not for geniuses. Everything is generally understandable given enough time and experience. So don't panic. Good Will Hunting is a lie. Still, we will take it slow, but I promise that nothing in the following sections, and the rest of this book, will go unexplained. </p>

<h2> Now let's get to the good stuff, the Minkowski Distance Metric, this big boy. </h2>

<img src='https://wikimedia.org/api/rest_v1/media/math/render/svg/33aa1151bd324808aeb7d7bd1262f6b8c515ec14' style="width: 600px">

<p> Note: If you have not encountered the notation above for dealing with series, heres a quick and easy explanation: <a href='https://www.youtube.com/watch?v=haK3oC0L_a8'> YouTube. </a> .  </p>

<p> So let's break it down. When p = 1, we have the manhattan distance: </p>

<img src='http://angiogenesis.dkfz.de/oncoexpress/software/cs_clust/dist_004.gif' style="width: 600px">

<p> And when p = 2, we've got Euclidean: </p>

<img src='http://mines.humanoriented.com/classes/2010/fall/csci568/portfolio_exports/lguo/image/euclidean_distance.jpg' style="width: 600px">

<p> And so we get a rough idea of what this formula is communicating.</p>

<h1>DISTANCE. IT REVEALS A FUNDAMENTAL TRUTH ABOUT THE MEASUREMENT OF DISTANCE IN TWO DIMENSIONAL SPACE. THIS EQUATION, MINKOWSKI DISTANCE, GIVEN DIFFERENT P VALUES, REVEALS DIFFERENT POSSIBLE MEASURES OF DISTANCE, EACH OF WHICH WEIGHS THE IMPORTANCE OF THE RATIO BETWEEN X AN Y VALUES DIFFERENTLY. SOUNDS AND SEEMS COMPLICATED, BUT THE EASIEST WAY TO THINK ABOUT IT FOR MYSELF IS THAT IT IS JUST A FUNCTION THAT WILL RETURN TO YOU A DIFFERENT WAY TO MEASURE DISTANCE GIVEN DIFFERENT INPUTS. P COOL RIGHT? MATH IS BEAUTIFUL. JUST, LIKE, THIS THING, THESE COUPLE OF SYMBOLS, CONDENSE LITERALLY AN INFINITE NUMBER OF DIFFERENT WAYS TO MEASURE DISTANCE IN TWO DIMENSIONAL SPACE. HERES A PICTURE OF THESE WAYS, DEPICTED AS SHAPES, SEE HOW THE CIRCLE IS EUCLIDEAN WHEREAS THE DIAMOND IS MANHATTAN? THIS IS BECAUSE THE MEASURE OF DISTANCE IN MANHATTAN TERMS IS "TRIANGULAR", A SIMPLE ADDITION OF THE SUMS, WHEREAS THE MEASURE IN EUCLIDEAN TERMS RELIES UPON THE SQUARE ROOT OF THE SUM OF THE SQUARES, E.G. "CIRCULAR". IT IS KIND OF FUNNY TO TALK ABOUT AND IM NOT SURE THE BEST WAY TO GO ABOUT IT, BUT HOPEFULLY YOU KIND OF GET WHAT I MEAN. AT THE VERY LEAST TODAY YOU LEARNED ABOUT MINKOWSKI DISTANCE WHICH MAY OR MAY NOT BE IMPORTANT TO YOU OR YOUR FUTURE EMPLOYMENT, BUT WHO CARES LMAO? MATH IS GREAT AND THAT'S WHAT REALLY COUNTS.</h1>

<img src='https://upload.wikimedia.org/wikipedia/commons/thumb/0/00/2D_unit_balls.svg/2250px-2D_unit_balls.svg.png' style="width: 100vw">

<h1> Getting back to the topic at hand. Distance is important, especially for Data Science, as, if we want to recommend a good book to Miles Jones, our best bet is most likely to look for the person most similar to Miles, in terms of distance, and recommend a book that this "closest neighbor" liked that Miles Jones has not read. </h1>

<h1> Time for the Pearson Correlation Coefficient, otherwise known as the thing I tell literally everyone about when they ask me about Data Science. </h1>

<p> CAPS LOCK IS CRUISE CONTROL FOR COOL.</p>

<p> So people are different, and rate things differently. I might rate things on a scale of 1 to 10, whereas Harambe might only rate them on a scale of 4 to 5. So things aren't objective. How do data scientists deal with this "grade inflation?" As with anything dank, there is a math equation. The Pearson Correlation Coefficient describes the similarity of two people for whom the grading scale is subjective. It is pretty sick, but before I get into it, lets get into some dank memes. </p>

<img src='https://s-media-cache-ak0.pinimg.com/564x/f1/4e/16/f14e1605521c8b37db3dc7e290bb51a4.jpg' style="width: 100vw">
<img src='http://media.lolusercontent.com/api/embedly/1/image/resize?url=http%3A%2F%2Fimgur.com%2Fy1JvdCP.jpg&key=a45e967db0914c7fb472fd4381e6c85b&width=425' style="width: 100vw">
<img src='https://img.ifcdn.com/images/8a607a62f1caa8eb22410cda40d962766c4a7838675dcde3a6a1dfc14828fac7_1.jpg' style="width: 100vw">

<h1> That's good, now let's get into some real stuff familia. The Pearson Correlation Coefficient: </h1>

<img src='http://ww2.tnstate.edu/ganter/BIO311-Ch12-Eq8.gif' style="width: 100vw">

<p> This equation will pop out a number betweeen -1 and 1, with 0 being no correlation between two people's subjective ratings and 1 being a really high correlation. Negative one is a really high correlation of disagreement. Simply put, if I rate this on a scale of 4 and 5, whereas you rate things on a scale from one to five, we can be in really good agreement, even if our scales are different, really good disagreement, or not really compatible measurements. This, of course, allows us to make measures of similarity even with skewed data. </p>

<h1> HOWEVER, THE EQUATION ABOVE IS REALLY A PAIN TO COMPUTE, SO WE WILL USE THIS ONE INSTEAD. </h1>

<img src='https://lh6.googleusercontent.com/7DYEG48coma6lbAYYa7K-tz9SuBbF0Aw3N8tGtZ9zSepsoIxkwh4Ix9C0i2o6iqwS-QuX68TsrFQarQ=w1366-h680' style="width: 100vw">

<h1> LMAOOOOOOOO!!! </h1>

<p> Kay, don't be scared. We're going to walk through what this means. But then again, I'm v lazy so I'm going to steal an explanation from another book, and then explain "why" it works. </p> 


<img src='https://lh6.googleusercontent.com/i0xsJq1BLsb_ZEJCn--CwEdzSIWsG6SqLRJeaC3H9-pA3BhGErx8Ozm6O0yfErxrBc-qDuSTMmWb6WQ=w1366-h680' style="width: 100vw">

<img src='https://lh5.googleusercontent.com/vDom8SrjUwKH_0a9j1MddRcrKzvNfgyP0HTqkVVtgXv3skoCctOnRxVrxEuWkqAzyL_bWBZROVyZxDQ=w1366-h680' style="width: 100vw">

<img src='https://lh4.googleusercontent.com/VApkEmNaSGDdoHXGj5YQLn853beDBoqgWAY5Rr2ptC9BXzngpPokAcCMYJCbskH0N1j9K0CUTYuJYMw=w1366-h680' style="width: 100vw">

<img src='https://lh3.googleusercontent.com/BW6jI29YHLCciQxS8gecmC-ksL-TrR7Z9Gd37DlUnCSNTSn3WNUDhtkRyovyT9rn-fgVh_-wFbp2cR4=w1366-h680' style="width: 100vw">
