import pygame
import random

# Initialize Pygame
pygame.init()
pygame.mixer.init()
pygame.mixer.music.load("C:\\Users\\Mateo\\Downloads\\339703__ffkoenigsegg20012017__audi-v8-acceleration-sound.wav")

# Screen settings
WIDTH, HEIGHT = 600, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Car Game")

# Colors
WHITE = (255, 255, 255)
GRAY = (50, 50, 50)
GREEN = (0, 200, 0)
YELLOW = (255, 255, 0)
RED = (200, 0, 0)
BLACK = (0, 0, 0)

# Clock & FPS
clock = pygame.time.Clock()
FPS = 60

# Load car images
player_img = pygame.image.load("C:\\Users\\Mateo\\Downloads\\Car game\\red_car.png")
enemy_img = pygame.image.load("C:\\Users\\Mateo\\Downloads\\Car game\\blue_car.png")

# Resize images
player_img = pygame.transform.scale(player_img, (60, 108))
enemy_img = pygame.transform.scale(enemy_img, (60, 108))

# Font
font = pygame.font.SysFont(None, 36)
game_over_font = pygame.font.SysFont(None, 50)

# Global level
level = 1

# Define bullet variables
bullets = []  # List to store bullets
bullet_speed = 10  # Speed at which bullets move
bullet_img = pygame.Surface((10, 20))  # Create a simple bullet shape
bullet_img.fill(YELLOW)  # Color bullet


def game_loop():
    global level, bullets, bullets_fired  

    print("Starting Level: " + str(level))  
    pygame.mixer.music.play(-1)  
    pygame.mixer.music.set_volume(1)

    max_lanes = WIDTH // 100
    num_lanes = min(level + 1, max_lanes)
    road_width = num_lanes * 80
    road_x = (WIDTH - road_width) // 2

    player_x = road_x + (road_width // 2) - 10  
    player_y = HEIGHT - 120  

    enemies = []  
    enemy_speed = level  + 5
    score = 0  
    bullets_fired = 0  
    max_bullets = 10  

    lane_positions = [road_x + i * (road_width // num_lanes) for i in range(num_lanes)]  
    min_spacing = 200  
    used_y_positions = []

    for _ in range(min(level * 2, 8)):  
        retries = 0  
        while retries < 20:  
            enemy_x = random.choice(lane_positions) + 20  
            enemy_y = random.randint(-600, -100)  
            if all(abs(enemy_y - other_y) >= min_spacing for other_y in used_y_positions):  
                used_y_positions.append(enemy_y)  
                enemies.append([enemy_x, enemy_y])  
                break  
            retries += 1  

    running = True  
    while running:  
        clock.tick(FPS)  
        screen.fill(GREEN)  

        # ✅ Handle events correctly for bullet firing
        for event in pygame.event.get():  
            if event.type == pygame.QUIT:  
                pygame.quit()  
                return  
            if event.type == pygame.KEYDOWN:  
                if event.key == pygame.K_SPACE and bullets_fired < max_bullets:  
                    bullets.append([player_x + 25, player_y])  
                    bullets_fired += 1  

        # ✅ Get key states for movement
        keys = pygame.key.get_pressed()  
        if (keys[pygame.K_LEFT] or keys[pygame.K_a]) and player_x > road_x:  
            player_x -= 5  
        if (keys[pygame.K_RIGHT] or keys[pygame.K_d]) and player_x < road_x + road_width - 60:  
            player_x += 5  

        # ✅ Move bullets upward & check collisions  
        for bullet in bullets[:]:  
            bullet[1] -= bullet_speed  
            if bullet[1] < 0:  
                bullets.remove(bullet)  

            bullet_rect = pygame.Rect(bullet[0], bullet[1], 10, 20)  
            for enemy in enemies[:]:  
                enemy_rect = pygame.Rect(enemy[0] + 10, enemy[1] + 10, 60, 90)  
                if bullet_rect.colliderect(enemy_rect):  
                    bullets.remove(bullet)  
                    enemies.remove(enemy)  
                    score += 1  

                    # ✅ Spawn new enemy when one is destroyed  
                    new_enemy_x = random.choice(lane_positions) + 20  
                    new_enemy_y = random.randint(-600, -100)  
                    enemies.append([new_enemy_x, new_enemy_y])  

        pygame.draw.rect(screen, GRAY, (road_x, 0, road_width, HEIGHT))  

        for i in range(1, num_lanes):  
            lane_x = road_x + (i * (road_width // num_lanes)) - 5  
            for y in range(0, HEIGHT, 60):  
                pygame.draw.rect(screen, WHITE, (lane_x, y, 10, 40))  

        for enemy in enemies:  
            enemy[1] += enemy_speed  
            if enemy[1] > HEIGHT:  
                enemy[1] = random.randint(-600, -100)  
                enemy[0] = random.choice(lane_positions)  
                score += 1  

        # ✅ End game when player collides with an enemy  
        player_rect = pygame.Rect(player_x + 10, player_y + 10, 60, 90)  
        for enemy in enemies:  
            enemy_rect = pygame.Rect(enemy[0] + 10, enemy[1] + 10, 60, 90)  
            if player_rect.colliderect(enemy_rect):  
                running = False  
                return game_over_screen(score)  

        if score >= level * 10:  
            return level_complete_screen()  

        screen.blit(player_img, (player_x, player_y))  
        for enemy in enemies:  
            screen.blit(enemy_img, (enemy[0], enemy[1]))  

        # ✅ Draw bullets properly  
        for bullet in bullets:  
            screen.blit(bullet_img, (bullet[0], bullet[1]))  

        score_text = font.render("Level " + str(level) + " | Score: " + str(score) + "/" + str(level*10) + " | Bullets: " + str(max_bullets - bullets_fired), True, RED)  
        screen.blit(score_text, (10, 10))  

        pygame.display.flip()
        
def game_over_screen(score):
    pygame.mixer.music.stop()
    global level
    game_over_text = game_over_font.render("GAME OVER", True, WHITE)
    final_score_text = font.render("Final Score: " + str(score), True, YELLOW)
    restart_game_text = font.render("Restart", True, WHITE)
    exit_game_text = font.render("Exit", True, WHITE)

    restart_button = pygame.Rect(WIDTH // 2 - 60, HEIGHT // 2, 120, 40)
    exit_button = pygame.Rect(WIDTH // 2 - 60, HEIGHT // 2 + 50, 120, 40)

    while True:
        screen.fill(GRAY)
        pygame.draw.rect(screen, BLACK, restart_button)
        pygame.draw.rect(screen, BLACK, exit_button)
        screen.blit(game_over_text, (WIDTH // 2 - 100, HEIGHT // 2 - 80))
        screen.blit(final_score_text, (WIDTH // 2 - 80, HEIGHT // 2 - 40))
        screen.blit(restart_game_text, (WIDTH // 2 - 43, HEIGHT // 2 + 8))
        screen.blit(exit_game_text, (WIDTH // 2 - 27, HEIGHT // 2 + 58))
        pygame.display.flip()

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
            if event.type == pygame.MOUSEBUTTONDOWN:
                if restart_button.collidepoint(event.pos):
                    level = 1
                    return "restart"
                if exit_button.collidepoint(event.pos):
                    pygame.quit()
                    return


def level_complete_screen():
    pygame.mixer.music.stop()
    global level
    level_complete_text = game_over_font.render("LEVEL " + str(level) + " COMPLETE!", True, WHITE)
    next_level_text = font.render("Next Level", True, BLACK)
    next_level_button = pygame.Rect((WIDTH // 2) - 53, HEIGHT // 2, 140, 40)

    while True:
        screen.fill(GREEN)
        pygame.draw.rect(screen, YELLOW, next_level_button)
        screen.blit(level_complete_text, (WIDTH // 2 - 170, HEIGHT // 2 - 80))
        screen.blit(next_level_text, (WIDTH // 2 - 45, HEIGHT // 2 + 10))
        pygame.display.flip()

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                return
            if event.type == pygame.MOUSEBUTTONDOWN:
                if next_level_button.collidepoint(event.pos):
                    return "next"


def main():
    global level, screen
    while True:
        result = game_loop()
        if result == "restart":
            level = 1
        else:
            level += 1

main()
 
