c33 Topic : Debugging Tips and Tricks

GOAL:

Learn how to minimize errors and bugs in the code.
Learn different techniques to debug codes.
Debug the Angry Bird trajectory when shooting multiple times.
any computer programmer in their lifetime will spend more time debugging than writing a new code!
Debugging is a normal part of programming.
This is because we are giving instructions to a computer and we are trying to think like a computer.
However, we are humans and we don't think naturally like computers.
Good programmers accept that there will always be bugs in their code and they ENJOY the process of debugging and fixing errors in their code.
Debugging is both an art and a science that way. It is like detective work where you try to find which line of code or thought patterns in your mind lead you to write something which is causing an error.
What is the first thing to do when you realize that the code is not doing what you want it to do?

The very first thing is to NOT PANIC! Good programmers don't panic.
They realize that debugging is a normal part of programming.
Bugs are normal.
Every program will have bugs.
You will be in a much better position to find and solve these bugs if you are calm and composed.
The second thing to do is to check the console log for errors!

If there are any error messages in the console, they often tell you what happened and why this error occurred or point you in that direction.

Often you can fix the errors in your code by reading these error messages.

You can open the console in your browser by pressing Ctrl + Shift + J

The most common errors are

Typos: You accidentally misspelled a variable or a function name which computer doesn't understand.

Incorrect Use of function: You used a function in a way it wasn't intended to be used.

Using variables outside their scope: If you are using variables outside their scope, the computer wouldn't know the value of these variables.

Often there are no error messages in the console and yet your program is not behaving in the expected way.

Or the error message doesn't tell you everything that needs to be fixed.

There are a few techniques which will help you identify what is causing the bug or which section of your code is leading to this bug.

Commenting sections of your code: You can comment certain sections of your code to simplify your code and check if your code still throws errors. In this way you can narrow down to the part of the code which is causing this error.
Printing values of variables in the console: You can print the values of critical variables in the console to visually see how they are changing in the code. If they are not changing as you intend them to, there is something unexpected happening. You can manipulate the variable values to identify what is happening.
Print messages in your code: You can print messages in your code to visually understand how the code is running. For example: You can print messages in the console to understand if while executing the code, an ‘if block’ is getting executed or the ‘else block.’
You can also combine all the 3 steps.
Writing clean modular code, formatting your code correctly, giving proper name to your functions, objects and variables, adding proper comments - all these take only a little time but saves a lot of time when you are debugging your code. It makes your code easier to read/understand and thus easier to identify the errors.
Before running the code, one should always have what they expect in their mind and see the difference between what's actually happening.
Writing clean modular code, formatting your code correctly, giving proper name to your functions, objects and variables, adding proper comments - all these take only a little time but saves a lot of time when you are debugging your code. It makes your code easier to read/understand and thus easier to identify the errors.
Debugging Steps:
BUG:

In the last class, we didn't allow player to take multiple shots at the pigs.

Let's change the code to allow the player to take as many shots at the pigs as they want.

comments and uncomments parts of text which would allow the player to take multiple shots at the target.

~~~javascript
function mouseDragged(){
//    if (gameState!=="launched"){
        Matter.Body.setPosition(bird.body, {x: mouseX , y: mouseY});
 //   }
}

function keyPressed(){
    if(keyCode === 32)
    {
      

```javascript
 slingshot.attach(bird.body);
}
```

}
~~~


Run the code and takes multiple shots at the pigs.
What is the bug / unwanted behavior we have in the code?
There are multiple trajectories of the bird on the screen. When we reset the bird back to the slingshot.
We would want the previous trajectory to be deleted.
The bird swings rapidly when it is reset. This is not desired. Also it causes additional trajectory mark.
Debugging :

Do you expect any errors in the console for this bug?

NO

Because, The code is not doing anything unexpected. Only the result is undesirable to us.

identify the part of the code which is responsible for drawing the trajectory?

points to the trajectory and the display function in the console where the image of trajectory is being drawn.

~~~javascript
class Bird extends BaseClass {
  constructor(x,y){
    super(x,y,50,50);
    this.image = loadImage("sprites/bird.png");
    this.smokeImage = loadImage("sprites/smoke.png");
    this.trajectory =[ ];
  }

  display() {
    //this.body.position.x = mouseX;
    //this.body.position.y = mouseY;

    super.display();
    
    if(this.body.velocity.x > 10 && this.body.position.x > 200){
      var position = [this.body.position.x, this.body.position.y];
      this.trajectory.push(position);
    }


```javascript
for(var i=0; i<this.trajectory.length; i++){
  image(this.smokeImage, this.trajectory[i][0], this.trajectory[i][1]);
}
```

  }
}
~~~

what would you do if you wanted to remove the trajectory when the space key is pressed?
All the positions of the birds are stored in the array property of the Bird called trajectory. We can simply empty this array whenever the space key is pressed.
You can simply empty an array by assigning no value inside empty brackets.

```javascript
function keyPressed()
{
    if(keyCode === 32)
    {
    bird.trajectory = [ ];
       slingshot.attach(bird.body);
    }
}
```

the old trajectory seems to get removed when the bird resets.
BUG :

the old trajectory seems to get removed when the bird resets.
BUG :

The bird swings widely when attaching to the slingshot.

Why does that happen?

What can we do so that it doesn’t swing so much?

Because the bird gets attached to the slingshot right from its last position.

We can reset the position of the bird when space is pressed.

use Matter.Body.setPosition , to position the bird.

```javascript
function keyPressed()
{
    if(keyCode === 32  )
    {
    bird.trajectory = [ ];
Matter.Body.setPosition(bird.body,{x:200, y:50});      
      slingshot.attach(bird.body);
    }
}
```


allow resets only when the bird has stopped moving by adding an additional condition in the if statement.

```javascript
function keyPressed()
{
    if(keyCode === 32 && bird.body.speed<1 )
    {
    bird.trajectory = [ ];
Matter.Body.setPosition(bird.body,{x:200, y:50});       slingshot.attach(bird.body);
    }
}
```

