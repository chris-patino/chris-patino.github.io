---
layout: Template
---

<div id = "can">
<div id = "scoreBox"></div>
<div id = "box1"></div>
<div id = "but1"></div>
<div id = "butin1"></div>
<div id = "but2"></div>
<div id = "butin2"></div>
<div id = "but3"></div>
<div id = "butin3"></div>
<div id = "light1"></div>
<div id = "light2"></div>
<div id = "light3"></div>
<div id = "user"></div>
<div id = "box2"></div>

<p id = "winText">Congrats, you win! <br>
Try again to improve your score?</p>
</div>
<p id = "demo">Press f to start. <br>
avoid the red box. <br>
Kill it as fast as you can with the lights.<br>
bring the lights down by jumping through hoops<br>
Move with wasd</p>

<style>
#can {
  position: absolute;
  left: 0px;
  top: 0px;
  height: 400px;
  width: 400px;
  background: grey;
  border: solid;
  border-color: black;
  border-width: 4px;
}

#user {
  position: absolute;
  left: 350px;
  bottom: 40px;
  height: 20px;
  width: 20px;
  background: blue;
}

#box1 {
  position: absolute;
  bottom: 0px;
  height: 40px;
  width: 400px;
  background: black;
}

#box2 {
  position: absolute;
  bottom: 40px;
  height: 40px;
  width: 40px;
  background: red;
}

#scoreBox {
  position: absolute;
  left: 180px;
  width: 50px;
  height: 50px;
  background: black;
  color: white;
  font-size: 34pt;
  text-align: center;
  font-family: analde mono;
}

#demo {
  position: absolute;
  top: 590px;
  left: 450px;
  font-size: 18pt;
}

#but1 {
  position: absolute;
  left: 40px;
  bottom: 90px;
  height: 40px;
  width: 40px;
  background: blue;
  display: block;
}

#butin1 {
  position: absolute;
  left: 45px;
  bottom: 95px;
  height: 30px;
  width: 30px;
  background: grey;
  display: block;
}

#but2 {
  position: absolute;
  left: 300px;
  bottom: 80px;
  height: 40px;
  width: 40px;
  background-color: blue;
  display: none;
}

#butin2 {
  position: absolute;
  left: 305px;
  bottom: 85px;
  height: 30px;
  width: 30px;
  background-color: grey;
  display: block;
}

#but3 {
  position: absolute;
  left: 230px;
  bottom: 40px;
  height: 40px;
  width: 40px;
  background-color: blue;
  display: none;
}

#butin3 {
  position: absolute;
  left: 235px;
  bottom: 45px;
  height: 30px;
  width: 30px;
  background-color: grey;
  display: block;
}

#light1 {
  position: absolute;
  left: 150px;
  bottom: 380px;
  height: 20px;
  width: 20px;
  background-color: yellow;
  display: block;
}

#light2 {
  position: absolute;
  left: 70px;
  bottom: 380px;
  height: 20px;
  width: 20px;
  background-color: yellow;
}

#light3 {
  position: absolute;
  left: 340px;
  bottom: 380px;
  height: 20px;
  width: 20px;
  background-color: yellow;
}

#winText {
  position: absolute;
  left: 30px;
  bottom: 100px;
  font-size: 24pt;
  color: #61FF00;
  display: none;
}
</style>

<script>

//Neccesary globals
var userx = 300;
var usery = 40;
var userColor = "blue";


var box2x = 0;
var box2y = 40;
var box2Top = box2y + 40;


var i = 0;
var score = 0;
var k = 0;
var speed = 1;
var moveRight = 0;
var moveLeft = 0;

//hoop and ball stuff
var level = 1; //regulates which hoop is active & visible
var butdisp1 = "block";
var butdisp2 = "none";
var butdisp3 = "none";
var but1x = 40;
var but1y = 90;
var but2x = 300;
var but2y = 80;
var but3x = 230;
var but3y = 40;




var light1x = 150;
var light1y = 380;
var light2x = 70;
var light2y = 380;
var light3x = 340;
var light3y = 380;


//These make loops
var j = setInterval(moveUser, speed);
var m = setInterval(moveUser, speed);
var r = setInterval(moveUser, speed);
var l = setInterval(moveUser, speed);
var s = setInterval(stopMoveUser, speed);
var h = setInterval(blueHoops, speed);
var f = setInterval(blueHoops, speed);
var c = setInterval(collision, speed);



function moveUser (event) {

addEventListener("keydown", moveUser);

document.getElementById("user").style.left = userx + "px";
document.getElementById("user").style.bottom = usery + "px";
document.getElementById("user").style.background = userColor;

document.getElementById("box2").style.left = box2x + "px";
document.getElementById("box2").style.bottom = box2y + "px";


if (event.keyCode == 68 && moveRight != 1 && moveLeft != 1) {
  moveRight = 1;
  r = setInterval(userMoveRight, speed);

} else if (event.keyCode == 65 && moveLeft != 1 && moveRight != 1) {
  moveLeft = 1;
  l = setInterval(userMoveLeft, speed);

} else if (event.keyCode == 87 && k == 0) {
  j = setInterval(jump, speed);
  speed -= 1;
  clearInterval(m);//the above and below lines make speed increase with every jump
  m = setInterval(autoMoveBox2, speed);

} else if (event.keyCode == 70 && i == 0) {
  m = setInterval(autoMoveBox2, speed);
} else if (event.keyCode == 82) {
  location.reload();
}

function autoMoveBox2 () {



  if (i < 360) {
    i += 1;
    box2x += 1;
  } else if (i >= 360 && i < 720) {
    i += 1;
    box2x -= 1;
  } else if (i == 720) {
    i = 0;
  }



//regulates score. I didn't have a better place to put this.
  if (i == 360 && userColor != "red") {
    score ++;
    document.getElementById("scoreBox").innerHTML = score;
  } else if (i == 0 && userColor != "red") {
    score ++;
    document.getElementById("scoreBox").innerHTML = score;
  }
}




function jump () {


    if (k < 70) {
      k += 1;
      usery += 1;

    } else if (k >= 70 && k <= 139) {
      k += 1;
      usery -= 1;

    } else if (k == 140) {
      clearInterval(j);
      k = 0;
    }
  }


}

function stopMoveUser (event) {

addEventListener("keyup", stopMoveUser);

document.getElementById("user").style.left = userx + "px";
document.getElementById("user").style.bottom = usery + "px";


if (event.keyCode == 68 && moveLeft !== 1) {
  moveRight = 0; //I picked 2 just because it's not 1 and 0 doesn't work
  clearInterval(r); //stops the rightwards movement

} else if (event.keyCode == 65 && moveRight !== 1) {
  moveLeft = 0; //you can figure out what's hapenning here based on the previous if statement
  clearInterval(l);
}
}
//loops that create movement
function userMoveRight() {

  if (moveRight == 1) {
    userx += 1;
  }
}

function userMoveLeft() {

  if (moveLeft == 1){
    userx -= 1;
  }
}

function collision() {

  //collision physics
    if (userx <= 0) {
    userx++;
    } else if (userx >= box2x - 20 && usery < box2Top && userx <= box2x + 40) {
      //userx -= 1;
      //userColor = "red";
      location.reload();
    } else if (userx >= 380) {
      userx--;
    }
}



//regulates hoop visibility and activity as well as ball dropping
function blueHoops() {

  document.getElementById("user").style.background = userColor;

  document.getElementById("user").style.left = userx + "px";
  document.getElementById("user").style.bottom = usery + "px";

  document.getElementById("box2").style.left = box2x + "px";
  document.getElementById("box2").style.bottom = box2y + "px";

  document.getElementById("but1").style.display = butdisp1;
  document.getElementById("but2").style.display = butdisp2;
  document.getElementById("but3").style.display = butdisp3;

  document.getElementById("light1").style.left = light1x + "px";
  document.getElementById("light1").style.bottom = light1y + "px";
  document.getElementById("light2").style.left = light2x + "px";
  document.getElementById("light2").style.bottom = light2y + "px";
  document.getElementById("light3").style.left = light3x + "px";
  document.getElementById("light3").style.bottom = light3y + "px";

  document.getElementById("but1").style.left = but1x + "px";
  document.getElementById("but1").style.bottom = but1y + "px";
  document.getElementById("but2").style.left = but2x + "px";
  document.getElementById("but2").style.bottom = but2y + "px";
  document.getElementById("but3").style.left = but3x + "px";
  document.getElementById("but3").style.bottom = but3y + "px";


//regulate light dropping loops and makes hoops dissapear
if (userColor !== "red" && level == 1 &&
    userx >= but1x + 5 && userx <= but1x + 15 &&
    usery >= but1y + 5 && usery <= but1y + 20 &&
    light1y == 380) {
  f = setInterval(dropLight1, speed);
  //document.getElementById("scoreBox").innerHTML = level;
} else if (userColor !== "red" && level == 2 &&
    userx >= but2x + 5 && userx <= but2x + 15 &&
    usery >= but2y + 5 && usery <= but2y + 20 &&
    light2y == 380) {
  f = setInterval(dropLight2, speed);
  //document.getElementById("scoreBox").innerHTML = level;
} else if (userColor !== "red" && level == 3 &&
    userx >= but3x + 5 && userx <= but3x + 15 &&
    usery >= but3y + 5 && usery <= but3y + 20 &&
    light3y == 380) {
  f = setInterval(dropLight3, speed);
  //document.getElementById("scoreBox").innerHTML = level;
} else if (level == 4) {
  //document.getElementById("scoreBox").innerHTML = level;
  f = setInterval(win, speed);
}

if (light1y < 380 && level == 1) {
  butdisp1 = "none";
} else if (light2y < 380 && level == 2) {
  butdisp2 = "none";
} else if (light3y < 380 && level == 3) {
  butdisp3 = "none";
}

//regulate level
if (userColor !== "red" && light1x == box2x - 20 && light1y < box2y + 20 && level == 1 ||
    userColor !== "red" && light1x == box2x + 40 && light1y < box2y + 20 && level == 1) {
  level ++;
  butdisp2 = "block";
  document.getElementById("light1").style.display = "none";
} else if (userColor !== "red" && light2x == box2x - 20 && light2y < box2y + 20 && level == 2 ||
           userColor !== "red" && light2x == box2x + 40 && light2y < box2y + 20 && level == 2) {
  level ++;
  butdisp3 = "block";
  document.getElementById("light2").style.display = "none";
} else if (userColor !== "red" && light3x == box2x - 20 && light3y < box2y + 20 && level == 3 ||
           userColor !== "red" && light3x == box2x + 40 && light3y < box2y + 20 && level == 3) {
  level ++;
  document.getElementById("light3").style.display = "none";
}

function win() {

  clearInterval(j);
  clearInterval(m);
  clearInterval(r);
  clearInterval(l);
  clearInterval(s);
  clearInterval(h);
  clearInterval(f);
document.getElementById("winText").style.display = "block";

}

}

function dropLight1() {
  document.getElementById("light1").style.left = light1x + "px";
  document.getElementById("light1").style.bottom = light1y + "px";

  if (light1y > 40) {
    light1y -= 5;
  } else if (light1y == 40) {
    clearInterval(f);
  }
}

function dropLight2() {
  document.getElementById("light2").style.left = light2x + "px";
  document.getElementById("light2").style.bottom = light2y + "px";

  if (light2y > 40) {
    light2y -= 5;
  } else if (light2y == 40) {
    clearInterval(f);
  }
}

function dropLight3() {
  document.getElementById("light3").style.left = light3x + "px";
  document.getElementById("light3").style.bottom = light3y + "px";

  if (light3y > 40) {
    light3y -= 5;
  } else if (light3y == 40) {
    clearInterval(f);
  }
}

</script>
