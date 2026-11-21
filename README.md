import pgzrun, random

WIDTH, HEIGHT = 800, 400
TITLE = "Minimal Dino Game"


dino = Rect((50, 310), (40, 50))
cacti = []


gravity, velocity, is_jumping = 1, 0, False
score, game_over, speed = 0, False, 7

def update():
global velocity, is_jumping, game_over, score, speed
if game_over: return



if is_jumping:
dino.y -= velocity
velocity -= gravity
if dino.y >= 310:
dino.y, is_jumping = 310, False
elif keyboard.space or keyboard.up:
velocity, is_jumping = 16, True


speed += 0.002
if not cacti or cacti[-1].x < WIDTH - random.randint(200, 400):
cacti.append(Rect((WIDTH, 360 - random.randint(30, 60)), (25, random.randint(30, 60))))

for c in list(cacti):
c.x -= speed
if c.x < -25:
cacti.remove(c)
score += 1


if dino.colliderect(c):
game_over = True

def draw():
screen.fill((247, 247, 247))
screen.draw.line((0, 360), (WIDTH, 360), (210, 210, 210))
screen.draw.filled_rect(dino, (83, 83, 83))

for c in cacti:
screen.draw.filled_rect(c, (46, 139, 87))

screen.draw.text(f"SCORE: {score}", (WIDTH - 150, 20), color=(83, 83, 83), fontsize=24)

if game_over:
screen.draw.text("GAME OVER - Press R to Restart", center=(WIDTH//2, HEIGHT//2), color=(200, 50, 50), fontsize=36)

def on_key_down(key):
global cacti, score, game_over, speed, is_jumping
if key == keys.R and game_over:
cacti.clear()
dino.y, score, speed, is_jumping, game_over = 310, 0, 7, False, False

pgzrun.go()
