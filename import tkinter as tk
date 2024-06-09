import tkinter as tk

# Initialize the main window
root = tk.Tk()
root.title("Ball Game")

# Set up the canvas
canvas_width, canvas_height = 800, 600
canvas = tk.Canvas(root, width=canvas_width, height=canvas_height, bg="black")
canvas.pack()

# Ball properties
ball_radius = 20
ball_color = "red"
start_pos = [canvas_width // 2, canvas_height // 2]
ball_pos = start_pos.copy()
ball_vel = [5, 5]  # Velocity in x and y directions; starts moving towards the platform

# Platform properties
platform_width = 20
platform_height = 100
platform_color = "blue"
platform_x = 50  # Distance from the left edge
platform_y = canvas_height // 2 - platform_height // 2
platform_speed = 20

# Create the ball
ball = canvas.create_oval(ball_pos[0] - ball_radius, ball_pos[1] - ball_radius,
                          ball_pos[0] + ball_radius, ball_pos[1] + ball_radius,
                          fill=ball_color)

# Create the platform
platform = canvas.create_rectangle(platform_x, platform_y,
                                   platform_x + platform_width, platform_y + platform_height,
                                   fill=platform_color)

# Initialize score counter
score = 0

# Create a label to display the score
score_label = tk.Label(root, text=f"Score: {score}", fg="white", bg="black", font=("Helvetica", 16))
score_label.pack()

# Function to move the ball
def move_ball():
    global ball_pos, ball_vel, score

    # Update the ball's position
    ball_pos[0] += ball_vel[0]
    ball_pos[1] += ball_vel[1]

    # Check if the ball hits the left wall
    if ball_pos[0] <= ball_radius:
        # Reset ball position
        ball_pos = start_pos.copy()
        ball_vel[0] = 5  # Ensure it moves towards the platform after reset
        # Increment the score
        score += 1
        # Update the score label
        score_label.config(text=f"Score: {score}")

    # Check if the ball hits the platform
    if ball_pos[0] <= platform_x + platform_width + ball_radius:
        if platform_y <= ball_pos[1] <= platform_y + platform_height:
            ball_vel[0] = -ball_vel[0]

            # Adjust the ball's vertical velocity based on where it hit the platform
            hit_pos = ball_pos[1] - platform_y
            hit_ratio = (hit_pos - platform_height / 2) / (platform_height / 2)
            ball_vel[1] += hit_ratio * 5  # Modify this factor to change the bounce effect

    # Check if the ball hits the right wall
    if ball_pos[0] >= canvas_width - ball_radius:
        ball_vel[0] = -ball_vel[0]

    # Bounce the ball off the top and bottom walls
    if ball_pos[1] <= ball_radius or ball_pos[1] >= canvas_height - ball_radius:
        ball_vel[1] = -ball_vel[1]

    # Update the ball's position on the canvas
    canvas.coords(ball, ball_pos[0] - ball_radius, ball_pos[1] - ball_radius,
                  ball_pos[0] + ball_radius, ball_pos[1] + ball_radius)

    # Schedule the next move
    root.after(30, move_ball)

# Function to move the platform up
def move_platform_up(event):
    global platform_y
    if platform_y > 0:
        platform_y -= platform_speed
        canvas.coords(platform, platform_x, platform_y,
                      platform_x + platform_width, platform_y + platform_height)

# Function to move the platform down
def move_platform_down(event):
    global platform_y
    if platform_y < canvas_height - platform_height:
        platform_y += platform_speed
        canvas.coords(platform, platform_x, platform_y,
                      platform_x + platform_width, platform_y + platform_height)

# Bind the arrow keys to the platform movement functions
root.bind("<Up>", move_platform_up)
root.bind("<Down>", move_platform_down)

# Start moving the ball
move_ball()

# Start the Tkinter main loop
root.mainloop()
