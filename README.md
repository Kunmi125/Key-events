import pygame

pygame.init()
pygame.display.set_caption("Rocket in space")

screen_width = 700
screen_height = 500
screen = pygame.display.set_mode([screen_width,screen_height])

# Define the player sprite
# player startsat (0,0) by default

class Player(pygame.sprite.Sprite):
    def __init__(self):
        self.image = pygame.image.load("rocket.png").convert_alpha() 
        self.image = pygame.transform.scale(self.image,(70,100))
        self.rect = self.image.get_rect()

        # move the sprite based on the jeypresses
    def update(self,pressed_keys):
        if pressed_keys[pygame.K_UP]:
            self.rect.move_ip(0,-5)
        if pressed_keys[pygame.K_DOWN]:
            self.rect.move_ip(0,5)
        if pressed_keys[pygame.K_LEFT]:
            self.rect.move_ip(-5,0)
        if pressed_keys[pygame.K_RIGHT]:
            self.rect.move_ip(5,0)
        
        # keep player on the screen
        if self.rect.left < 0:
            self.rect.left = 0
        
        elif self.rect.right > screen_width:
            self.rect.right = screen_width

        if self.rect.top <= 0:
            self.rect.top= 0

        elif self.rect.bottom >= screen.height:
            self.rect.bottom = screen_height

# make a group of all the sprites
sprites = pygame.sprite.Group()

def startgame():
    player = Player()
    player2 = Player()
    sprites.add(player)
    sprites.add(player2)

    #start the loop

    while True:
        # look at every event
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                #if it is the quit event
                pygame.quit()
                exit(0)

            # Get the set of keys pressed and check for user input
            pressed_keys = pygame.key.get_pressed()
            player.update(pressed_keys)

            screen.blit(pygame.image.load("background.png"),(0,0))

            sprites.draw(screen)

            pygame.display.update()

startgame()
                


            
            


