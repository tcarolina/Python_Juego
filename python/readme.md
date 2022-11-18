# Juego de Serpiente
Snake - Game 

main.py 
from turtle import Screen  #importa la libreria turtle
from snake import Snake #importa la clase serpiente
from food import Food #importación Alimento
from scoreboard import Scoreboard  #importar el marcador
import time #libreria de tiempo 

screen = Screen() #poner pantalla
screen.setup(width=600, height=600) #pantalla.configuración(ancho=600, alto=600)
screen.bgcolor("black") #pantalla.bgcolor("negro")
screen.title("My Snake Game")#titulo ("Mi juego de la serpiente")
screen.tracer(0) #pantalla.trazador(0)

snake = Snake() #serpiente = serpiente()
food = Food() #comida = comida()
scoreboard = Scoreboard() #marcador = marcador()

screen.listen() #pantalla.escuchar()
screen.onkey(snake.up, "Up") #pantalla.en la tecla(serpiente.arriba, "Arriba")
screen.onkey(snake.down, "Down") #pantalla.en la tecla (serpiente.abajo, "Abajo")
screen.onkey(snake.left, "Left") #pantalla.en la tecla (serpiente.izquierda, "Izquierda")
screen.onkey(snake.right, "Right") #pantalla.en la tecla (serpiente.derecha, "Derecha")

# si el juego esta encendido ejecutara en pantalla: 
game_is_on = True
while game_is_on:
screen.update()

# tiempo en el que se va mover la culebra:
time.sleep(0.1)
snake.move()

# Detecta la colisión con la comida:
if snake.head.distance(food) < 15:
food.refresh()
snake.extend()
scoreboard.increase_score()

# Detecta la colisión con la pared:
if snake.head.xcor() > 280 or
snake.head.xcor() < -280 or snake.head.ycor() > 280 or snake.head.ycor() < -280:
game_is_on = False # esto termina el juego en caso de colision con la pared
scoreboard.game_over()

# esto detecta la colision con la cola.
for segment in snake.segments:
if segment == snake.head:
pass
elif snake.head.distance(segment) < 10:
game_is_on = False  # esto termina el juego en caso de colision con la cola.
scoreboard.game_over()
# cierra la pantalla
screen.exitonclick()

food.py
from turtle import Turtle #importa la libreria turtle
import random #importa la funcion random

class Food(Turtle): #crea una clase 

# define las caracteristicas fisicas de la comida
def __init__(self):
super().__init__()
self.shape("circle")
self.penup()
self.shapesize(stretch_len=0.5,
stretch_wid=0.5)
self.color("blue")
self.speed("fastest")
self.refresh()
# tdetermina donde va estar la comida de forma aleatoria 
def refresh(self):
random_x = random.randint(-280, 280)
random_y = random.randint(-280, 280)
self.goto(random_x, random_y)

scoreboard.py #marcador (importa la clase puntuacion)
from turtle import Turtle #importa la libreria turtle
ALIGNMENT = "center" #indica marcador centrado
FONT = ("Courier", 24, "normal") #indica la tipografia

# crea la clase de marcador
class Scoreboard(Turtle): 
# define las caracteristicas fisicas del marcador
def __init__(self):
super().__init__()
self.score = 0
self.color("white")
self.penup()
self.goto(0, 270)
self.hideturtle()
self.update_scoreboard()
# muestra en pantalla la puntuacion
def update_scoreboard(self):
self.write(f"Score: {self.score}",align=ALIGNMENT, font=FONT)
# muestra en pantalla game_over
def game_over(self):
self.goto(0, 0)
self.write("GAME OVER",
align=ALIGNMENT, font=FONT)
# conteo de puntos
def increase_score(self):
self.score += 1

self.clear() #elimina los datos
self.update_scoreboard() #actualiza los datos
