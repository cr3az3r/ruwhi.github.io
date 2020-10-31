<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Untuk Nurulku</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css" integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">
    <style type="text/css">
        body{
    font-size: 20px;
    font-family: monospace;
    background-color: #E671FE;
}

.container{
   background-color: #2c3e50;
   min-height: 300px;
   max-width : 800px;
   border-radius: 5px;
   box-shadow: 0px 5px 15px 0px;
   position: relative;
   display: flex;
}
#start{
    font-size: 1.5em;
    height: 45px;
    font-weight: bolder;
    text-align: center;
    cursor: pointer;
    margin: auto;
    align-content: center;
    position: relative;
    padding: 0px 20px;
    top: 0;
}

#qImg{
    width : 300px;
    height : auto;
    position: relative;
    align-content: center;
    top : 0px;
}
#qImg img{
    width: 100%;
    margin: 15px 0;
    height : auto;
    border-top-left-radius: 5px;
}

#question{
    width:500px;
    height : 125px;
    position: absolute;
    right:0;
    top:10px;
}
#question p{
    margin : 0;
    text-align: center;
    padding : 25px;
    font-size: 1.25em;
    color:#fff;
}

#choices{
    width : 500px;
    position: absolute;
    right : 0;
    align-content: center;
    top: 25%;
    padding : 10px;
    color:#fff;
}
.choice{
    width : 150px;
    text-align: center;
    border-radius: 5px;
    cursor: pointer;
    padding : 10px;
    display: block;
    margin: 25px auto;
    margin-left: auto;
    margin-right: auto;
}

#timer{
    position: absolute;
    height : 100px;
    width : 200px;
    bottom : 0px;
    text-align: center;
}
#counter{
    font-size: 3em;
}
#btimeGauge{
    width : 150px;
    height : 10px;
    border-radius: 10px;
    background-color: lightgray;
    margin-left : 25px;
}
#timeGauge{
    height : 10px;
    border-radius: 10px;
    background-color: mediumseagreen;
    margin-top : -10px;
    margin-left : 25px;
}
#progress{
    width : 500px;
    position: absolute;
    bottom : 0px;
    right : 0px;
    padding:5px;
    text-align: right;
}
.prog{
    width : 25px;
    height : 25px;
    border: 1px solid #000;
    display: inline-block;
    border-radius: 50%;
    margin-left : 5px;
    margin-right : 5px;
}
#scoreContainer{
    margin : 20px auto;
    background-color: white;
    opacity: 0.8;
    height: 300px;
    width : 700px;
    border-radius: 5px;
    box-shadow: 0px 5px 15px 0px;
    position: relative;
    display: none;
}
#scoreContainer img{
    position: absolute;
    top:100px;
    left:325px;
}
#scoreContainer p{
    position: absolute;
    display: block;
    width : 59px;
    height :59px;
    top:130px;
    left:325px;
    font-size: 1.5em;
    font-weight: bold;
    text-align: center;
}
.quis{
    display: none;
}

.btn-grad {background-image: linear-gradient(to right, #DA22FF 0%, #9733EE  51%, #DA22FF  100%);}
.btn-grad {
            
            text-align: center;
            text-transform: uppercase;
            transition: 0.5s;
            background-size: 200% auto;
            color: white;            
            box-shadow: 0 0 5px #eee;
            border-radius: 10px;
}

.btn-grad:hover {
            background-position: right center; /* change the direction of the change here */
            color: #fff;
            text-decoration: none;
}

@media screen and (max-width: 800px) {

.container{
    display: flex;
    justify-content: center;
    height: 100%;
}
.quis{
    display: none;
    flex-direction: column;
    height: 100%;
}
.gambar{

    flex: 1;
}
.tanya{
    flex: 1;
}
#qImg{
    margin: auto;
}
#question p{
    padding: 0px;
}
#question{
    margin: auto;
    width: 100%;
    left: 0;
    position: relative;
    height: auto;

}
#choices{
    margin: auto;
    width: 400px;
    top: 0;
    position: relative;
}

}

    </style>
</head>
<body>
    <div id="container" class="container">
        <div id="start" class="btn-grad">Klik Disini!</div>
        <div id="quiz" class="quis">
            <div class="gambar">
            <div id="qImg"></div>
            </div>
            <div class="tanya">
            <div id="question"></div>
            <div id="choices">
                <div class="choice btn-grad" id="A" onclick="alert(kata); + checkAnswer('A')"></div>
                <div class="choice btn-grad" id="B" onclick="checkAnswer('B')"></div>
                <div class="choice btn-grad" id="C" hidden onclick="checkAnswer('C')"></div>
            </div>
            </div>
            <div id="timer" hidden>
                <div id="counter"></div>
                <div id="btimeGauge"></div>
                <div id="timeGauge"></div>
            </div>
            <div hidden id="progress"></div>
        </div>
        <div id="scoreContainer" hidden style="display: hidden"></div>
    </div>
</body>

<script type="text/javascript">
// select all elements
const start = document.getElementById("start");
const quiz = document.getElementById("quiz");
const question = document.getElementById("question");
const qImg = document.getElementById("qImg");
const choiceA = document.getElementById("A");
const choiceB = document.getElementById("B");
const choiceC = document.getElementById("C");
const counter = document.getElementById("counter");
const timeGauge = document.getElementById("timeGauge");
const progress = document.getElementById("progress");
const scoreDiv = document.getElementById("scoreContainer");

// create our questions
let questions = [
    {
        question : "Kamu sayang gak sama aku?",
        imgSrc : "1.jpg",
        choiceA : "Iya Sayang",
        choiceB : "Tidak",
        choiceC : "",
        tanya : "sayang",
        correct : "A"

    },{
        question : "Apa kamu selalu cinta sama aku?",
        imgSrc : "1.jpg",
        choiceA : "Iya dong",
        choiceB : "Gak sih",
        choiceC : "",
        tanya : "baik",
        correct : "A"
    },{
        question : "Kamu rindu gak sama aku?",
        imgSrc : "1.jpg",
        choiceA : "Rindu banget",
        choiceB : "Gak sama seklai",
        choiceC : "",
        tanya : "rindu",
        correct : "A"
    }
];

// create some variables

const lastQuestion = questions.length - 1;
let runningQuestion = 0;
let count = 0;
const questionTime = 1000000; // 10s
const gaugeWidth = 150; // 150px
const gaugeUnit = gaugeWidth / questionTime;
let TIMER;
let score = 0;

// render a question
function renderQuestion(){
    let q = questions[runningQuestion];
    
    question.innerHTML = "<p>"+ q.question +"</p>";
    qImg.innerHTML = "<img src="+ q.imgSrc +">";
    choiceA.innerHTML = q.choiceA;
    choiceB.innerHTML = q.choiceB;
    choiceC.innerHTML = q.choiceC;

    if (q.tanya == "sayang") {
        kata = "Aku juga sayaaang banget sama kamu :)";
    } else if (q.tanya == "baik") {
        kata = "Makasih sayangkuu. Kamu juga baik banget sama aku";
    } else {
        kata = "Aku juga rindu banget sama kamu";
    }
}

start.addEventListener("click",startQuiz);

// start quiz
function startQuiz(){
    start.style.display = "none";
    renderQuestion();
    quiz.style.display = "block";
    renderProgress();
    renderCounter();
    TIMER = setInterval(renderCounter,1000); // 1000ms = 1s
}

// render progress
function renderProgress(){
    for(let qIndex = 0; qIndex <= lastQuestion; qIndex++){
        progress.innerHTML += "<div class='prog' id="+ qIndex +"></div>";
    }
}

// counter render

function renderCounter(){
    if(count <= questionTime){
        counter.innerHTML = count;
        timeGauge.style.width = count * gaugeUnit + "px";
        count++
    }else{
        count = 0;
        // change progress color to red
        answerIsWrong();
        if(runningQuestion < lastQuestion){
            runningQuestion++;
            renderQuestion();
        }else{
            // end the quiz and show the score
            clearInterval(TIMER);
            scoreRender();
        }
    }
}

// checkAnwer

function checkAnswer(answer){
    if( answer == questions[runningQuestion].correct){
        // answer is correct
        score++;
        // change progress color to green
        answerIsCorrect();
    }else{
        // answer is wrong
        // change progress color to red
        answerIsWrong();
    }
    count = 0;
    if(runningQuestion < lastQuestion){
        runningQuestion++;
        renderQuestion();
    }else{
        // end the quiz and show the score
        clearInterval(TIMER);
        scoreRender();
    }
}

// answer is correct
function answerIsCorrect(){
    document.getElementById(runningQuestion).style.backgroundColor = "#0f0";
}

// answer is Wrong
function answerIsWrong(){
    document.getElementById(runningQuestion).style.backgroundColor = "#f00";

    let q = questions[runningQuestion];

    if (q.tanya == "sayang") {
        kata = "Tapi kenapa?";
    } else if (q.tanya == "baik") {
        kata = "Apa yang gak baik dari aku?";
    } else {
        kata = "Kenapa siiih?";
    }

    prompt(kata);
}

// score render
function scoreRender(){
    document.getElementById("muncul").click();
    scoreDiv.style.display = "block";
    
    // calculate the amount of question percent answered by the user
    const scorePerCent = Math.round(100 * score/questions.length);
    
    // choose the image based on the scorePerCent
    let img = (scorePerCent >= 80) ? "img/5.png" :
              (scorePerCent >= 60) ? "img/4.png" :
              (scorePerCent >= 40) ? "img/3.png" :
              (scorePerCent >= 20) ? "img/2.png" :
              "img/1.png";
    
    scoreDiv.innerHTML = "<img src="+ img +">";
    scoreDiv.innerHTML += "<p>"+ scorePerCent +"%</p>";
}
</script>

<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.1/js/bootstrap.min.js"></script>


<!-- Button trigger modal -->
<button hidden type="button" id="muncul" class="btn btn-primary" data-toggle="modal" data-target="#exampleModalLong">
</button>

<!-- Modal -->
<div class="modal fade" id="exampleModalLong" tabindex="-1" role="dialog" aria-labelledby="exampleModalLongTitle" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
        <video width="100%" id="vid" autoplay muted loop>
            <source src="vidio.mp4" type="video/mp4">
        </video>

    </div>
  </div>
</div>
<script type="text/javascript">
    document.getElementById('vid').play();
</script>
</html>