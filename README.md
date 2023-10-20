# pong
import pygame
pygame.init()

from winsound import Beep
import random

screen = pygame.display.set_mode((700,500))
pygame.display.set_caption("pong")

p1x = 20 # variables for paddle position 
p1y = 200
p2x = 666
p2y = 200
p2Speed = 5
bx = 200
by = 40
bVx = 3
bVy = 3 

doExit = False #variable that runs loop


clock = pygame.time.Clock()

while not doExit: #game loop
    
    clock.tick(60) #set fps
    #INPUT SECTION-----------------------------
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            doExit = True
            #game logic goes here
        keys = pygame.key.get_pressed()
    if keys[pygame.K_w]:
        p1y-=5
    elif keys[pygame.K_s]:
        p1y+=5
    if keys[pygame.K_UP]:
        p2y-=p2Speed
        p2Speed += 0.01
    elif keys[pygame.K_DOWN]:
        p2y+=p2Speed
        p2Speed += 0.01
    
    #pHYSICS SECTION----------------------
    
    #BOUNCE OFF LEFT OR RIGHT WALL
    if bx-7 < 0 or bx + 7 > 700:
        bVx *= -1
        
    #BOUNCE OFF top OR BOTTOM WALL
    if by-7 < 0 or by + 7 > 500:
        bVy *= -1
         
    #BOUNCE OFF LEFT PADDLE
    if bx-7 < p1x + 20 and by + 20 > p1y and by < p1y + 100:
        bVx *= -1
        
    
    #BOUNCE OFF RIGHT PADDLE
    if by < p2y + 20 and bx + 20 > p2x and bx < p2x + 100:
        bVy *= 2
    
    #UPDATE BALL'S POSITION
    bx += bVx
    by += bVy        
            
            #tess wqz here
            
            
            
    #render section         
    screen.fill((0,0,0))

    pygame.draw.rect(screen, (255, 255, 255), (p1x, p1y, 20, 100), 1)
    pygame.draw.line(screen, (255, 255, 255), [349, 0], [349,500], 5)
    pygame.draw.rect(screen, (255, 255, 255), (p2x, p2y, 20, 100), 1)
    pygame.draw.circle(screen, (255, 255, 255), (bx, by), 15)
    pygame.display.flip()






    #end of loop

pygame.quit()

            
