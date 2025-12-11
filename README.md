import os
import time
import random
import json

# ------------------------------------------------------
# SIMPLE CLOUD + AI PRODUCTIVITY PLATFORM
# PROJECT NAME: AI PRODUCTIVE CLOUD
# ------------------------------------------------------

# Fake satellite dataset
SATELLITE_IMAGES = [
    "forest_region.png",
    "city_map.png",
    "river_flow.png",
    "mountain_view.png"
]

# Fake AI tags based on filename
TAGS = {
    "forest": ["trees", "green", "dense vegetation"],
    "city": ["buildings", "roads", "urban"],
    "river": ["water", "flow", "nature"],
    "mountain": ["hills", "snow", "rock"]
}

# ------------------------------
# LOGIN SYSTEM
# ------------------------------
users = {}

def register():
    name = input("Enter username: ")
    pwd = input("Enter password: ")
    users[name] = pwd
    print("Registration successful!\n")

def login():
    name = input("Username: ")
    pwd = input("Password: ")

    if name in users and users[name] == pwd:
        print("\nLogin successful!\n")
        return True
    else:
        print("Invalid login.\n")
        return False

# ------------------------------
# Simulate satellite data fetch
# ------------------------------
def fetch_satellite_data():
    print("Connecting to satellite...")
    time.sleep(1)
    img = random.choice(SATELLITE_IMAGES)
    print(f"Received satellite image: {img}")
    return img

# ------------------------------
# AI processing (very simple)
# ------------------------------
def ai_analyze(image):
    print("\nAI Processing Image...")

    for key in TAGS:
        if key in image:
            return TAGS[key]

    return ["unknown"]

def ai_summary(tags):
    print("\nGenerating summary...")
    summary = "This region contains: " + ", ".join(tags)
    return summary

# ------------------------------
# CLOUD STORAGE (local folder)
# ------------------------------
def save_to_cloud(username, image, summary):
    folder = f"cloud_{username}"
    os.makedirs(folder, exist_ok=True)

    data = {
        "image_name": image,
        "tags": summary
    }

    filename = image.replace(".png", ".json")
    path = os.path.join(folder, filename)

    with open(path, "w") as f:
        json.dump(data, f, indent=4)

    print(f"\nSaved to cloud: {path}\n")

# ------------------------------
# Productivity Tools (simple AI)
# ------------------------------
def todo_list():
    tasks = []
    print("\n--- AI Productivity To-Do List ---")
    while True:
        t = input("Add task (or type 'exit'): ")
        if t == "exit":
            break
        tasks.append(t)

    print("\nYour Tasks:")
    for i, t in enumerate(tasks):
        print(f"{i+1}. {t}")

def ai_note_generator():
    text = input("\nEnter topic for AI to generate note: ")
    print("Generating note...\n")
    print(f"AI Note on {text}:")
    print(f"- {text} is important for satellite data understanding.")
    print(f"- Helps improve productivity in cloud systems.\n")

# ------------------------------
# MAIN MENU
# ------------------------------
def main_menu(username):
    while True:
        print("""
============================
 AI PRODUCTIVE CLOUD
============================
1. Fetch Satellite Data
2. View Productivity Tools
3. AI Note Generator
4. Logout
""")
        choice = input("Enter choice: ")

        if choice == "1":
            img = fetch_satellite_data()
            tags = ai_analyze(img)
            summary = ai_summary(tags)
            save_to_cloud(username, img, summary)

        elif choice == "2":
            todo_list()

        elif choice == "3":
            ai_note_generator()

        elif choice == "4":
            break

        else:
            print("Invalid choice.\n")

# ------------------------------
# PROGRAM START
# ------------------------------
def main():
    print("Welcome to AI PRODUCTIVE CLOUD\n")

    while True:
        print("1. Register\n2. Login\n3. Exit")
        c = input("Enter choice: ")

        if c == "1":
            register()
        elif c == "2":
            if login():
                username = input("Enter your username again: ")
                main_menu(username)
        elif c == "3":
            print("Goodbye!")
            break
        else:
            print("Invalid option.\n")

main()

