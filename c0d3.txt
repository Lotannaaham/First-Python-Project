# my First Python project
# pong game built with py 3
# Part 1: Getting started

import turtle
import winsound

win = turtle.Screen()
win.title("Pong by @Lotanna")
win.bgcolor("blue")
win.setup(width=800, height=600)
win.tracer(0)

# keeping track of the scores
score_a = 0
score_b = 0

# Paddle A
paddle_a = turtle.Turtle()
paddle_a.speed(0)
paddle_a.shape("square")
paddle_a.color("black")
paddle_a.shapesize(stretch_wid=5, stretch_len=1)
paddle_a.penup()
paddle_a.goto(-350, 0)

# Paddle B
paddle_b = turtle.Turtle()
paddle_b.speed(0)
paddle_b.shape("square")
paddle_b.color("black")
paddle_b.shapesize(stretch_wid=5, stretch_len=1)
paddle_b.penup()
paddle_b.goto(350, 0)

# Ball
ball = turtle.Turtle()
ball.speed(0)
ball.shape("circle")
ball.color("black")
ball.penup()
ball.goto(0, 0)
# for Ball movement
ball.dx = 0.2
ball.dy = -0.2

# pen
# for displaying player scores
pen = turtle.Turtle()
pen.speed(0)
pen.color("black")
pen.penup()
pen.hideturtle()
pen.goto(0, 260)
pen.write("Player A: 0  Player B: 0", align ="center", font=("courier", 20, "bold"))

# Function
# for Function paddle a up and down
def paddle_a_up():
    y = paddle_a.ycor()
    y += 20
    paddle_a.sety(y)

def paddle_a_down():
    y = paddle_a.ycor()
    y -= 20
    paddle_a.sety(y)

# for Function paddle b up and down
def paddle_b_up():
    y = paddle_b.ycor()
    y += 20
    paddle_b.sety(y)

def paddle_b_down():
    y = paddle_b.ycor()
    y -= 20
    paddle_b.sety(y)

# Keyboard binding
win.listen()
win.onkeypress(paddle_a_up, "w")
win.onkeypress(paddle_a_down, "s")
win.onkeypress(paddle_b_up, "Up")
win.onkeypress(paddle_b_down, "Down")


# Main game loop
while True:
    win.update()

    # for Moving the ball
    ball.setx(ball.xcor() + ball.dx)
    ball.sety(ball.ycor() + ball.dy)

    # for Bouncing off the border
    # if else statements

    # up
    if ball.ycor() > 290:
        ball.sety(290)
        ball.dy *= -1
        winsound.PlaySound("bounce.wav", winsound.SND_ASYNC)

    # down  
    if ball.ycor() < -290:
        ball.sety(-290)
        ball.dy *= -1
        winsound.PlaySound("bounce.wav", winsound.SND_ASYNC)

    # both sides
    # player a (left)
    if ball.xcor() > 390:
        ball.goto(0, 0)
        ball.dx *= -1
         # incrementing score player a
        score_a += 1
        # for clearing the previous score before displaying the current score
        pen.clear()
        pen.write("Player A: {}  Player B: {}".format(score_a, score_b), align ="center", font=("courier", 20, "bold"))
        winsound.PlaySound("bounce.wav", winsound.SND_ASYNC)
    
    # player b (right)
    if ball.xcor() < -390:
        ball.goto(0, 0)
        ball.dx *= -1
        # incrementing score player b
        score_b += 1
        # for clearing the previous score before displaying the current score
        pen.clear()
        pen.write("Player A: {}  Player B: {}".format(score_a, score_b), align ="center", font=("courier", 20, "bold"))
        winsound.PlaySound("bounce.wav", winsound.SND_ASYNC)


    # ball and paddle collision
    if (ball.xcor() > 340 and ball.xcor() < 350) and (ball.ycor() < paddle_b.ycor() + 40 and ball.ycor() > paddle_b.ycor() -50):
        ball.setx(340)
        ball.dx *= -1
        winsound.PlaySound("bounce.wav", winsound.SND_ASYNC)

    if (ball.xcor() < -340 and ball.xcor() > -350) and (ball.ycor() < paddle_a.ycor() + 40 and ball.ycor() > paddle_a.ycor() -50):
        ball.setx(-340)
        ball.dx *= -1
        winsound.PlaySound("bounce.wav", winsound.SND_ASYNC)