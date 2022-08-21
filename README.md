WINGSPAN:
---------

After playing a fairly decent game of Wingspan (scoring 93 points), my brother mentioned how cool it would be to calculate the maximum number of points achievable in a game of Wingspan. I checked and the world record is a whoping `186` points, which is frankly insane. But is there a way to do better? I am interested in the following question.

> What is the maximum possible score in a game of single-player Wingspan?

The reason I am exploring single-player Wingspan is because introducing a second player adds a whole lot of complexity. Does the second player play with perfect play favourably or adversarially? Favourable play is easier, but adversarial becomes very hard, since the second player's aim becomes to decrease the first player's score as much as possible, which makes the strategy a whole lot richer.

Because of the sheer number of possible games, our main aim to find the best possible lower bound on the number of points achievable in a single-player game.

More about Wingspan:
---------------------

What constitutes a game of single-player Wingspan? Well, we have a deck of `162` distinct bird cards, an initial hands of `5` cards, a set of `4` end of round goals, a hand of `2` initial bonus cards, a set of `3` initial picking birds, and a set of `8` turn cubes. This is all we need to capture the initial state of a single-player Wingspan game.

As the game progresses we also need to keep track of the birds placed, eggs layed... you get the idea. The game offers many possible strategies, in fact far too many to check them all. This is the challenge!

A silly upper bound:
---------------

Before we start with getting some lower bounds we look at a simplistic upper bound, which overshoots the maximum score by quite some way it seems. We can score points in five different ways:

	1. Feather points.
	2. Egg points.
	3. Food on card points.
	4. Tucked card points.
	5. Bonus card points.
	6. End of round points.

The maximum number of feather points is `5*9 + 8*8 + 2*7 = 123`.
The maximum number of egg points is `4*6 + 11*5 = 79`.
The maximum number of food on card points is `1 + 2 + 3 + 4 + 17*5 = 95`.
The maximum number of tucked card points is `2 + 4 + 6 + 8 + 17*10 = 190`.
The maximum number of bonus card points is `7*15*2 + 1*15*1 + 2*8 + 3*7 = 262`.
The maximum number of end of round points is `20`.

Therefore, we can definitely do no better than `123 + 95 + 190 + 262 + 20 = 690`. Although this is not very insightful because it's obviously unachievable: birds with higher feather points have lower egg points and worse powers, and birds with higher egg points have lower feather points. 

Lower bounds:
--------------

Since there are far too many possible games to brute-force, we resort to heuristics. We can develop a bird rank heuristic where we attempt to compute some rank amongst the other birds based on how costly the bird is to play, its feather points, egg potential, etc... . We can also develop a synergy score for a set of birds which summarises how strong a set of birds is.

We design an algorithm which given 15 bird cards selects their optimal positioning for maximising points. With 15 bird cards we can place them in <= 15! ways, which is already infeasibly large.


Further questions:
------------------

If we generalise the game of Wingspan such that we have `N` distinct bird cards, `B` distinct bonus cards, and `T` turn cubes, we can ask questions about the complexity of perfect play in terms of these parameters.

Consider the following decision problem:

> Alice is playing single-player generalised Wingspan. Assuming perfect play, can Alice score `>= X` points?

In other words, let `W` be the event that Alice scores `>= X` points, is `Pr[W]>0`?

What is the complexity of this problem? I aim to explore this question.

