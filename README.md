## Doe, oh my doe

The deer is inaccessible hidden behind all these shrubs. Heracles stays on the lookout, waiting for her to get out of there. For that, the animal would already have to be able to move!

The deer is going to be a monster with a somewhat particular behavior, in particular because it will be able to move, which is not the case for the other monsters.

> SOLID Note: You could implement deer-specific behavior directly in `Monster`. However, our hero still has a lot of beasts to fight and therefore as many specificities, which would ultimately make the `Monster` class very busy and certainly full of conditions specific to this or that subtype of monsters.

> Another solution is not to touch `Monster` directly, and to create a `Hind` class, inheriting from `Monster`, which will contain the code specific to the hinds. For each new type of monster with its own specificity, you add a new class. And it is still possible to instantiate a "basic" monster if you wish. This is the "Open/Close Principle" of SOLID. The classes, once defined, should remain "closed" to any modification (which would not concern all the objects of this class). If you happen to encounter such a case, the class must however be open to an extension, you must be able to create a child class easily.

In your new `Hind` class, add an `image` property with the value *hind.svg*.
Remember to import your new class in the *index.html* (Pay attention to the order of imports)

In the *index.js* file, modify the instantiation of a `Monster` by a `Hind`.

1. Each time the hero has finished moving, the monsters with the ability to move will do so, using the `move()` method themselves, which already contains all the movement logic (directions, tile checking...). We must therefore modify our `move()` methods so that it can react to different *moveable* `Fighters`. So add a second `fighter` parameter (The `Fighter` moved) to the method and fix the code accordingly.

2. The *gameplay* will be as follows: the hero moves then, if his move was successful, all the monsters that have the ability move in turn. To differentiate which `Fighters` can move, add a `moveable` property to Fighters which is `false` by default. Pass it to `true` in `Hero` and `Hind` class.

3. Heroes and monsters will use the same `move()` method to manage their movement, in order to benefit from the checks specific to all `moveable`. To manage this, we use the `globalMove(direction, hero)` method, this one is already taken into account.

> Hint: In the `globalMove(direction, hero)` method, our hero is already moving thanks to `move()`. Consider passing the `hero` parameter to it to update your code with your previous developments

5. Then still in `globalMove()` loop on monsters implementing `moveable` to `true`.
- Generate a direction by creating a new method in monsters `getDirection()` which will return `N/S/W/E` randomly.
- Then move the monster in that direction by reusing the `move()` method.
- To be able to move, we must modify our `CheckNoMonster()` method so as not to take it into account if the monster in the box is the one that is moving... Watch out for your brain

6. You can restart the game, you should see the deer move after each move of Heracles.

> If you want to test, you can also add a second Hind and a Monster, the hinds should move and not the monster because it does not implement `moveable`! Then go back to a single doe on the map.

## Cache cache

Last point, our doe moves but is blocked behind the bushes. Let's change that. If Heracles doesn't know how to get through the thorny bushes in the forest, that's no problem for the deer. So we're going to make the Bush tile non-traversable, **except** for a doe!

1. To do this, create the `isCrossable()` method in Tile which returns the value of `crossable` by default. It takes an instance of `Monster` as a parameter. In `Arena`, when you use `isCrossable()`, pass in parameter what is trying to move on this tile.

2. In `Bush` now, redefine `isCrossable()` so that the function returns *true* if and only if `moveable` is an instance of `Hind`. Use the `js` *instanceOf* method for this. Otherwise, returns the value of the `crossable` property (which must be *false*). In other words, the tile is not traversable unless it's a deer trying!

3. In *Arena.js*, fix the call to the `crossable` check by your new `isCrossable(fighter)` method.

Perform several movements, you will see that the doe should end up crossing the bushes, it's the long-awaited moment, catch her!

> We won't be looking to implement Heracles actually capturing the Doe as that would take quite a bit of extra effort, but as always, if you'd like to give it a try, don't hesitate!
