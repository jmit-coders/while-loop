Last lesson we learned about arrays:
    1. they are a sequence of items
    2. they have a `length` property, telling us the number of items in the array
    3. we get items from the array using `[index]`, where index is the numerical position of the item in the array.
    4. we add an item to the end of the sequence using `push`
    5. we add an item to the beginning of the sequence using `shift`
    6. we remove an item from the end of the sequence using `pop`
    7. we remove an item from the beginning of the sequence using `unshift`

Also in the last lesson, we used multiple variables for setting up squares and moving them around. Even when we used an array, we had a lot of code that was nearly identical. In this lesson, we'll fix that using loops.

_Loops_ are a programming concept that allows us to _repeatedly_ run lines of code until a _condition_ is satisfied. 
    - A _condition_ is code that evaluates to `true` or `false`.
    - A _loop_ checks the condition, and stops running lines of code when the condition is `true`, and repeatedly runs the lines of code while the condition is `false`.

So what's an example of a condition? What does a condition look like?
    - `true === true` is a condition. Running it in the console evaluates to `true`. 
    - `4 > 3` could be a condition. If you run it in the console, it will evaluate to `true`.
    - `[0, 1, 2, 4].length === 5` could be a condition. Running that in the console will evaluate to `false`. 

Often times, a condition uses a _logical operator_ to **compare two things**. You might already be familiar with some of the operators if you've learned about inequalities in math.

|operator symbol |how to use it     | when it evaluates to `true`            | order of `a` and `b` matters |
|---------------:|-----------------:|---------------------------------------:|-----------------------------:|
|`===`           | `a === b`        | if `a` is equal to `b`                 | no                           |
|`!==`           | `a !== b`        | if `a` is not equal to `b`             | no                           |
|`<`             | `a < b`          | if `a` is less than `b`                | yes                          | 
|`>`             | `a > b`          | if `a` is greater than `b`             | yes                          |
|`<=`            | `a <= b`         | if `a` is less than or equal to `b`    | yes                          |
|`>=`            | `a >= b`         | if `a` is greater than or equal to `b` | yes                          |
|`&&`            | `a && b`         | if `a` and `b` both evaluate to `true` | no                           |
|`||`            | `a || b`         | if either `a` or `b` evaluate to `true`| no                           |

The last column is really important. If the order doesn't matter, switching `a` and `b` **will always** give the same result. But if the order does matter, switching `a` and `b` **will not always** give the same result. Confusing? Here are some examples.

| condition |result  |
|----------:|-------:|
| `3 === 4` |`false` |
| `4 === 3` |`false` |
| `3 !== 4` |`true`  |
| `4 !== 3` |`true`  |
| `3 < 4`   |`true`  |
| `4 < 3`   |`false` |
| `3 < 3`   |`false` |
| `3 < 3`   |`false` |

The last four examples are great examples of what's meant by **"will not always"** when order matters. When comparing 3 and 4, we can see that switching the order can change the result. When comparing 3 and 3, we get the same result, `false`. But would that always be the case if we compared any two numbers? No. Because when we compare 3 and 4 and switch the order, we get different answers. This is the big difference between **will always** and **will not always**, and it's an important difference we'll need to remember when we use these operators. 

Now that we know how to create conditions, we can look at the two types of loops we'll use in JavaScript, `while` and `for`. Let's start with a while loop.

_while loop_
```javascript
while(condition){
    //endless lines of code
    //as far as the eye can see
}
```

So we have `while`, followed by `condition` in parenthesis, and we put all of our code inside curly brackets (`{}`). As long as `condition` evaluates to `true,` the loop runs. Once `condition` evaluates to `false,` the loop stops. 

Now let's look at two simple while loops.

_the while that will never run_
```javascript
while(false){
    //this code will never run
    console.log("I'm inside the loop");
}
```

The condition inside the loop is always `false,`, so the while loop never runs the code in the curly brackets. Now for a more ~~obnoxious~~ interesting example.

_the infinite while loop, the loop that never ends_
```javascript
while(true){
    //this code will run forver
    console.log("This is the loop that never ends!");
    console.log("It just goes on, and on my friends!");
    console.log("Some people started running it, not knowing what it was.");
    console.log("And they continued running it forever just because...");
}
```

The condition inside this loop is always `true`, so the while loop will run the code inside curly brackets forever.

Onto something more interesting. Let's look at making a counter. What if we wanted to count from 0 up to 10, and display each number in the console? And once we reach 10, we want to stop counting? And can we do it using a while loop? Yes.

To do this, we'll use a variable called `x` to keep track of the current number. We'll also start with all of the code inside of a loop, and start with the condition being `false`.

```javascript
while(false){
    var x = 0;
    console.log(x);
    x = x + 1;
}
```

Will this work? No. We know that since the condition is `false`, the code inside the loop will never run. Let's try changing the conditon.

```javascript
while(true){
    var x = 0;
    console.log(x);
    x = x + 1;
}
```

Will this work? No. We know that it will run forever because the condition is always `true`. But there's also another problem. The only number being displayed in the console is 0. Why? It's because of where we create our variable `x`. The last line in the code increases `x` by 1. But when the last line is ran, we loop back to first line which... recreates our variable `x` and sets it to 0. To fix, we need to think of how many times we want to create `x` and set it to 0. The answer is once. Since loops repeatedly run code, it's a bad place to put code that needs to happen once. So a better place is move it outside of the loop.

```javascript
while(true){
    console.log(x);
    x = x + 1;
}

var x = 0;
```

Will this work? No. We get a `reference not defined` error. `x` is created after the loop, so it doesn't exist for the code inside the loop. This let's us know that the order of the code is important.

1. We want `x` to be created and assigned to 0 once.
2. We want `x` to exist before the loop begins.

The only other place for creating `x` is before the loop.

```javascript
var x = 0;

while(true){
    console.log(x);
    x = x + 1;
}
```

Will this work? No, but we're counting so that's progress. The problem is that counts forever. What we can do is change the condition by using a logical operator. Since we want to stop at 10, let's use a logical operator that allows us to compare if a number is less than or equal to 10.

```javascript
var x = 0;

while(0 <= 10){
    console.log(x);
    x = x + 1
}
```

Will this work? No. We're still counting, but it counts past 10. The problem is still the condition. 0 _is always_ less than equal to 10. Since the condition never changes and is always trye, it's the same as writing an infite loop. What we really want is a condition that can change. We need to compare 10 to something that's changing. So what if use our `x` variable? It's changing  on each _iteration_ or cycle of the loop.

```javascript
var x = 0;

while(x <= 10){
    console.log(x);
    x = x + 1
}
```

Will this work? Yes. Were all the examples necessary? Yes. All the examples walked us through what we should consider when making our while loop. 
1. We need to know the stop or end condition. This determines when we want the loop to stop.
2. We then determine how to write it as a _while_ condition. This determines when the while loop will stop. 
2. To write the _while_ condition, we need to use something that changes so the loop doesn't run forever.


Are there other ways we could write the condition and get the same result? Yes.

_using `<`_
```javascript
var x = 0;

while(x < 11){
    console.log(x);
    x = x + 1;
}
```

_using `>=`_
```javascript
var x = 0;

//notice that we change the order in the condition
while(10 >= x){
    console.log(x);
    x = x + 1;
}
```

_using `>`_
```javascript
var x = 0;

//notice that we change the order in the condition
while(11 > x){
    console.log(x);
    x = x + 1;
}
```

_using `!=`_
```javascript
var x = 0;

while(x !== 11){
    console.log(x);
    x = x + 1;
}
```
These examples show that we can write different code, and get the exact same result. This allows us to be flexibile and creative. 

_using some creativity_
```javascript
var x = "";

while(x != "           "){
    console.log(x.length);
    x = x + " ";
}
```

Now that we can write while loops, let's apply them to arrays. We'll walkthrough building another counter, but our variable will be an array which has the numbers 0 through 10. Let's start with a program that creates the array and loops forever.

```javascript
//our array of numbers 0 through 10
var array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

//our infinite loop. notice the condition
while(true){
    console.log(array);
}
```

This code displays the entire array forever, and that's not what we want. We want to display each number in the array, one at a time. We know we can use square brackets (`[]`) and an item's position to get a specific item from the array. So what if we start with just getting the first item from the array? And remember that the first item in the array is at position 0, not 1.

```javascript
//our array of numbers 0 through 10
var array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

//our infinite loop. notice the condition
while(true){
    //using indexing to get the first item from the array
    console.log(array[0]);
}
```

We're not displaying the entire array anymore, so that's progress. But, our code only displays the first number in the array and we stil have an infinite loop. On each cycle of the loop, we want to display the next number in the array. What we need is something that let's us change the position in the array, so we can get numbers at different positions. For that, we can use another variable.

```javascript
//our array of numbers 0 through 10
var array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

//our variable for tracking position in the array
var index = 0;

//our infinite loop. notice the condition
while(true){
    //using indexing to get the next item from the array
    console.log(array[index]);
}
```

Even with the new variable we're getting the same result as last time: the code displays 0 forever. We still need to add code to change the position on each cycle of the loop. Luckily, we wrote code like this in our original example of making a counter. Remember the line `x = x + 1` which increased `x` each cycle of the loop? We can use the same approach for increasing `index`.

```javascript
//our array of numbers 0 through 10
var array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

//our variable for tracking position in the array
var index = 0;

//our infinite loop. notice the condition
while(true){
    //using indexing to get the next item from the array
    console.log(array[index]);

    //increase the position so we can get the next item in the array
    index = index + 1;
}
```

Now we're displaying all the numbers in the array, but after 10 our code displays undefined forever. A table might help us out. `index` starts at 0, and we increase`index` by 1 on each cycle of the loop. `array[index]` gives us the number positioned at `index`.

|`index`| `array[index]`|
|------:|--------------:|
|0      |0              |
|1      |1              |
|2      |2              |
|3      |3              |
|4      |4              |
|5      |5              |
|6      |6              |
|7      |7              |
|8      |8              |
|9      |9              |
|10     |10             |
|11     |?              |

Using the table, we see that after we display 10, `index` becomes 11. But we don't have anything in the array after 10, which means when `index` reaches 11 we're not positioned at anything in the array. Hence, we get back `undefined`. We have this problem to fix, plus the issue of the infinite loop. But we know how to fix this from our previous counter example. How do we control when the loop stops looping? The condition! We can fix both of these issues by changing the condition. We'll need a condition that doesn't let the loop run forever, and stops the loop once all the values have been displayed. But how? Let's look at a modified version of the above table by adding a column for `array.length`.

|`index`|`array.length`|
|------:|-------------:|
|0      |11            |
|1      |11            |
|2      |11            |
|3      |11            |
|4      |11            |
|5      |11            |
|6      |11            |
|7      |11            |
|8      |11            |
|9      |11            |
|10     |11            |
|11     |11            |

If we think back to our previous counter example, our condition compared a _constant_ value of 10 and a _variable_ value which was `x`. In that example, 10 was our value that let us know we should stop displaying numbers and `x` was the next number to be displayed. We can use a similar approach to fix the condition for our current problem.

Using the table, we can look for a value that's constant and a value that changes. It looks like `array.length` is constant because it's always 11. And it looks like `index` changes during each cycle of the loop. Now that we have two values to compare, how should we compare them? What logical operator should we use? To help determine that, let's merge the last two tables into one.

|`array.length`|`index`| `array[index]`|
|-------------:|------:|--------------:|
|11            |0      |0              |
|11            |1      |1              |
|11            |2      |2              |
|11            |3      |3              |
|11            |4      |4              |
|11            |5      |5              |
|11            |6      |6              |
|11            |7      |7              |
|11            |8      |8              |
|11            |9      |9              |
|11            |10     |10             |
|11            |11     |`undefined`    |

We've made `index` the middle column so it's easier to compare it with `array.length` and `array[index]`. We see that `array[index]` gives us back 10, the last number in the array, when `index` is 10. When `index` increases to 11, we get `undefined`. And what's the relationship between `index` and `array.length` when that happens? They're both equal, since `index` and `array.length` are both 11. So is that the right condition, `index === array.length`?

```javascript
//our array of numbers 0 through 10
var array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

//our variable for tracking position in the array
var index = 0;

//loop while `index` is equal to `array.legnth`
while(index === array.length){
    //using indexing to get the next item from the array
    console.log(array[index]);

    //increase the position so we can get the next item in the array
    index = index + 1;
}
```
We've fixed the infinite loop so that's more progress, but we're not displaying any numbers anymore. We still need to tweak our condition. Let's recall how while loops works. With while loops, the code inside of the curly brackets only runs while the condition is `true`. So what is the result of our condition? We can use another table to help us.

|`index`| `array.length`| `index === array.length`|
|------:|--------------:|------------------------:|
|0      | 11            | `false`                 |

We see that at the start of the loop, the condition is false so the code in the curly brackets never runs. What we want is a condition that starts as `true` and eventually becomes `false`. To be more specific, we want a condition to become `false` once `index` *is equal to* `array.length`. Which means, as long as `index` *is less than* `array.length`, we want the loop to run our code. Let's look at another table using `<` and see if it'll work.

|`index`| `array.length`| `index < array.length` |
|------:|--------------:|-----------------------:|
|0      | 11            | `true`                 |
|1      | 11            | `true`                 |
|2      | 11            | `true`                 |
|3      | 11            | `true`                 |
|4      | 11            | `true`                 |
|5      | 11            | `true`                 |
|6      | 11            | `true`                 |
|7      | 11            | `true`                 |
|8      | 11            | `true`                 |
|9      | 11            | `true`                 |
|10     | 11            | `true`                 |
|11     | 11            | `false`                |

Looks promising. And if we try it.

```javascript
//our array of numbers 0 through 10
var array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

//our variable for tracking position in the array
var index = 0;

//loop while `index` is less than `array.legnth`
while(index < array.length){
    //using indexing to get the next item from the array
    console.log(array[index]);

    //increase the position so we can get the next item in the array
    index = index + 1;
}
```

Success! But of curiosity, what if we had used `<=` instead of `<`?

```javascript
//our array of numbers 0 through 10
var array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

//our variable for tracking position in the array
var index = 0;

//loop while `index` is less than or equal to `array.legnth`
while(index <= array.length){
    //using indexing to get the next item from the array
    console.log(array[index]);

    //increase the position so we can get the next item in the array
    index = index + 1;
}
```

It almost works. We all the numbers displayed, but we also display `undefined`. Why? Let's look at another table.

|`index`| `array.length` | `index <= array.length`| `array[index]`|
|------:|---------------:|-----------------------:|--------------:|
|0      | 11             | `true`                 |0              |
|1      | 11             | `true`                 |1              |
|2      | 11             | `true`                 |2              |
|3      | 11             | `true`                 |3              |
|4      | 11             | `true`                 |4              |
|5      | 11             | `true`                 |5              |
|6      | 11             | `true`                 |6              |
|7      | 11             | `true`                 |7              |
|8      | 11             | `true`                 |8              |
|9      | 11             | `true`                 |9              |
|10     | 11             | `true`                 |10             |
|11     | 11             | `true`                 |`undefined`    |

The table shows that the condition is still `true` when `index` and `array.length` are equal, and that makes sense since `11 <= 11` is `true`. And once `index` is 11, `array[index]` will give us `undefined`, and that also makes since because our array doesn't have any numbers at that position. So how could we fix this without changing the operator back to `<`? Let's look for another relationship between the values in our condition, `index` and `array.length`.

We know the last valid position in the array is 10 and the array has a length of 11. So it looks the last valid position is 1 less than the array length. In other words, `last valid positon = array length - 1`. So what if we subtract 1 from `array.length`?

|`index`|`array.length - 1`| `index <= (array.length - 1)`| `array[index]`|
|------:|-----------------:|-----------------------------:|--------------:|
|0      |10                | `true`                       |0              |
|1      |10                | `true`                       |1              |
|2      |10                | `true`                       |2              |
|3      |10                | `true`                       |3              |
|4      |10                | `true`                       |4              |
|5      |10                | `true`                       |5              |
|6      |10                | `true`                       |6              |
|7      |10                | `true`                       |7              |
|8      |10                | `true`                       |8              |
|9      |10                | `true`                       |9              |
|10     |10                | `true`                       |10             |
|11     |10                | `false`                      |`undefined`    |

Again, looks promising. Let's try it.

```javascript
//our array of numbers 0 through 10
var array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

//our variable for tracking position in the array
var index = 0;

//loop while `index` is less than or equal to `array.legnth`
while(index <= (array.length - 1)){
    //using indexing to get the next item from the array
    console.log(array[index]);

    //increase the position so we can get the next item in the array
    index = index + 1;
}
```
More success! We now have two ways of making a working counter using an array. This is another example that we can write different code and get the same result. Here's another creative example.

_a creative way of getting numbers from the array for counting_
```javascript
//our array of numbers 0 through 10
var array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

//our variable for tracking position in the array
var index = array.length;

//loop while `index` is less than or equal to `array.legnth`
while(index > 1){
    
    //using a creative approach for indexing
    console.log(array[array.length - index]);
    index = index - 1;
}
```