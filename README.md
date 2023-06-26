# Snake-Game
import turtle
import time
import random
speed = 0.30

table = turtle.Screen()
table.title('SNAKE GAME')
table.bgcolor('black')
table.setup(width=700, height=700)
table.tracer(0)

head = turtle.Turtle()
head.speed(0)
head.shape('square')
head.color('lightgreen')
head.penup()
head.goto(0,150)
head.direction = 'stop'

rat = turtle.Turtle()
rat.speed(0)
rat.shape('circle')
rat.color('red')
rat.penup()
rat.goto(0,0)
rat.shapesize(0.70,0.70)

tails = []
score = 0
text = turtle.Turtle()
text.speed(0)
text.shape('square')
text.color('white')
text.penup()
text.goto(0,270)
text.hideturtle()
text.write('SCORE: {}'.format(score), align ='center', font=('Times New Roman', 26,'normal'))

def move():
    if head.direction == 'up':
        y = head.ycor()
        head.sety(y + 20)
    if head.direction == 'down':
        y = head.ycor()
        head.sety(y - 20)
    if head.direction == 'right':
        x = head.xcor()
        head.setx(x + 20)
    if head.direction == 'left':
        x = head.xcor()
        head.setx(x - 20)

def goUp():
    if head.direction != 'down':
        head.direction = 'up'
def goDown():
    if head.direction != 'up':
        head.direction = 'down'
def goRight():
    if head.direction != 'left':
        head.direction = 'right'
def goLeft():
    if head.direction != 'right':
        head.direction = 'left'

table.listen()
table.onkey(goUp, 'Up')
table.onkey(goDown, 'Down')
table.onkey(goRight, 'Right')
table.onkey(goLeft, 'Left')

while True:
    table.update()

    if head.xcor() > 400 or head.xcor() < -400 or head.ycor() > 400 or head.ycor() < -400:
        time.sleep(1)
        head.goto(0,0)
        head.direction = 'stop'

        for tail in tails:
            tail.goto(1000,1000)

        tails = []
        score = 0
        text.clear()
        text.write('SCORE: {}'.format(score), align='center', font=('Times New Roman', 26, 'normal'))

        speed = 0.30

    if head.distance(rat) < 20:
        x = random.randint(-250, 250)
        y = random.randint(-250, 250)
        rat.goto(x,y)

        score = score + 10
        text.clear()
        text.write('SCORE: {}'.format(score), align='center', font=('Times New Roman', 26, 'normal'))

        speed = speed - 0.015

        newtail = turtle.Turtle()
        newtail.speed(0)
        newtail.shape('square')
        newtail.color('lightgreen')
        newtail.penup()
        tails.append(newtail)

    for i in range(len(tails) -1,0,-1):
        x = tails[i - 1].xcor()
        y = tails[i - 1].ycor()
        tails[i].goto(x,y)

    if len(tails) > 0 :
        x = head.xcor()
        y = head.ycor()
        tails[0].goto(x,y)

    move()
    time.sleep(speed)

