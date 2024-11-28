import tkinter as tk
from tkinter import messagebox
import csv
import os
WORKOUTS = {
    'Beginner': {
        'SmallChild': {
            'Low': ['Arm Circles (5 reps)', 'Marching in Place (10s)', 'Toe Touches (5 reps)'],
            'Normal': ['Arm Circles (10 reps)', 'Marching in Place (20s)', 'Toe Touches (10 reps)'],
            'High': ['Arm Circles (15 reps)', 'Marching in Place (30s)', 'Toe Touches (15 reps)']
        },
        'Youth': {
            'Low': ['Push-ups (5 reps)', 'Squats (10 reps)', 'Lunges (5 reps each leg)', 'Plank (15s)', 'Jumping Jacks (10 reps)'],
            'Normal': ['Push-ups (10 reps)', 'Squats (15 reps)', 'Lunges (10 reps each leg)', 'Mountain Climbers (10 reps)'],
            'High': ['Push-ups (15 reps)', 'Squats (20 reps)', 'Lunges (15 reps each leg)', 'Mountain Climbers (15 reps)']
        },
        'Adult': {
            'Low': ['Running', 'Aerobics', 'push-ups(10 reps)', 'Plank (20s)','rollerblading'],
            'Normal': ['Push-ups (12 reps)', 'Squats (18 reps)', 'Lunges (12 reps each leg)', 'Mountain Climbers (12 reps)'],
            'High': ['walking', 'running', 'squats(5 reps)', 'dancing']
        },
        'Senior': {
            'Low': ['Wall Push-ups (10 reps)', 'Chair Squats (10 reps)', 'Leg Raises (5 reps each leg)', 'Seated Marches (30s)','yoga'],
            'Normal': ['Wall Push-ups (15 reps)', 'Chair Squats (12 reps)', 'Leg Raises (10 reps each leg)', 'Seated Marches (1 min)','yoga'],
            'High': ['walking', 'running', 'squats(5 reps)', 'dancing','yoga']
        }
    },
    'Intermediate': {
        'SmallChild': {
            'Low': ['Arm Circles (10 reps)', 'Marching in Place (15s)', 'Toe Touches (10 reps)'],
            'Normal': ['Arm Circles (15 reps)', 'Marching in Place (25s)', 'Toe Touches (15 reps)'],
            'High': ['Arm Circles (20 reps)', 'Marching in Place (35s)', 'Toe Touches (20 reps)']
        },
        'Youth': {
            'Low': ['Push-ups (10 reps)', 'Squats (15 reps)', 'Lunges (10 reps each leg)', 'Plank (20s)', 'Mountain Climbers (15 reps)'],
            'Normal': ['Push-ups (15 reps)', 'Squats (20 reps)', 'Lunges (15 reps each leg)', 'Mountain Climbers (20 reps)'],
            'High': ['Push-ups (20 reps)', 'Squats (25 reps)', 'Lunges (20 reps each leg)', 'Mountain Climbers (25 reps)']
        },
        'Adult': {
            'Low': ['Running', 'Aerobics', 'push-ups(15 reps)', 'Plank (30s)','rollerblading'],
            'Normal': ['Push-ups (15 reps)', 'Squats (20 reps)', 'Lunges (15 reps each leg)', 'Mountain Climbers (15 reps)'],
            'High': ['walking', 'running', 'squats(10 reps)', 'dancing']
        },
        'Senior': {
            'Low': ['Wall Push-ups (15 reps)', 'Chair Squats (20 reps)', 'Leg Raises (10 reps each leg)', 'Seated Marches (40s)','yoga'],
            'Normal': ['Wall Push-ups (20 reps)', 'Chair Squats (15 reps)', 'Leg Raises (20 reps each leg)', 'Seated Marches (2 min)','yoga'],
            'High': ['walking', 'running', 'squats(10 reps)', 'dancing','yoga']
        }
    },
    'Advanced': {
        'SmallChild': {
            'Low': ['Arm Circles (15 reps)', 'Marching in Place (20s)', 'Toe Touches (15 reps)'],
            'Normal': ['Arm Circles (20 reps)', 'Marching in Place (30s)', 'Toe Touches (20 reps)'],
            'High': ['Arm Circles (25 reps)', 'Marching in Place (40s)', 'Toe Touches (25 reps)']
        },
        'Youth': {
            'Low': ['Push-ups (15 reps)', 'Squats (20 reps)', 'Lunges (15 reps each leg)', 'Plank (30s)', 'Mountain Climbers (20 reps)'],
            'Normal': ['Push-ups (20 reps)', 'Squats (25 reps)', 'Lunges (20 reps each leg)', 'Mountain Climbers (25 reps)'],
            'High': ['Push-ups (25 reps)', 'Squats (30 reps)', 'Lunges (25 reps each leg)', 'Mountain Climbers (30 reps)']
        },
        'Adult': {
            'Low': ['Running', 'Aerobics', 'push-ups(20 reps)', 'Plank (40s)','rollerblading'],
            'Normal': ['Push-ups (20 reps)', 'Squats (30 reps)', 'Lunges (20 reps each leg)', 'Mountain Climbers (20 reps)'],
            'High': ['walking', 'running', 'squats(20 reps)', 'dancing']
        },
         'Senior': {
            'Low': ['Wall Push-ups (20 reps)', 'Chair Squats (30 reps)', 'Leg Raises (20 reps each leg)', 'Seated Marches (50s)','yoga'],
            'Normal': ['Wall Push-ups (30 reps)', 'Chair Squats (20 reps)', 'Leg Raises (30 reps each leg)', 'Seated Marches (3 min)','yoga'],
            'High': ['walking', 'running', 'squats(20 reps)', 'dancing','yoga']
        }
            }
} 
def calculate_bmi(weight, height):
    try:
        bmi = weight / (height / 100) ** 2
        return round(bmi, 2)
    except ZeroDivisionError:
        return None
def bmi_category(bmi):
    if bmi < 18.5:
        return 'Low'
    elif 18.5 <= bmi <= 24.9:
        return 'Normal'
    else:
        return 'High'
def age_group(age):
    if age < 2:
        return None
    elif 2 <= age <= 10:
        return 'SmallChild'
    elif 11 <= age < 18:
        return 'Youth'
    elif 18 <= age < 60:
        return 'Adult'
    else:
        return 'Senior'
def generate_workout(level, bmi_cat, age_grp):
    if age_grp is None:
        return None
    level_workouts = WORKOUTS.get(level, {})
    age_workouts = level_workouts.get(age_grp, {})
    return age_workouts.get(bmi_cat, [])
def save_to_csv(name, age, height, weight, bmi, level, workout):
    headers = ["Name".ljust(15), "Age".ljust(5), "Height (cm)".ljust(12), "Weight (kg)".ljust(12), "BMI".ljust(10), "Level".ljust(10), "Workout".ljust(50)]
    file_exists = os.path.isfile('workout_log.csv')
    with open('workout_log.csv', 'a', newline='') as file:
        writer = csv.writer(file)
        if not file_exists or os.stat('workout_log.csv').st_size == 0:
            writer.writerow(headers)
        row_data = [
            name.ljust(15),
            str(age).ljust(5),
            f"{height}".ljust(12),
            f"{weight}".ljust(12),
            f"{bmi}".ljust(10),
            level.ljust(10),
            ', '.join(workout).ljust(50)
        ]
        writer.writerow(row_data)
def on_submit():
    name = entry_name.get()
    age = entry_age.get()
    height = entry_height.get()
    weight = entry_weight.get()
    level = var_level.get()
    if not name or not age or not height or not weight or not level:
        messagebox.showerror("Input Error", "Please fill all the fields.")
        return
    try:
        age = int(age)
        height = float(height)
        weight = float(weight)
        if age <= 0 or height <= 0 or weight <= 0:
            raise ValueError("Age, height, and weight must be positive numbers.")
    except ValueError as e:
        messagebox.showerror("Input Error", str(e))
        return
    bmi = calculate_bmi(weight, height)
    bmi_cat = bmi_category(bmi)
    age_grp = age_group(age)
    workout = generate_workout(level, bmi_cat, age_grp)
    if workout:
        save_to_csv(name, age, height, weight, bmi, level, workout)
        show_workout_window(name, bmi, bmi_cat, workout)
    else:
        messagebox.showerror("No Workout", "No workout assigned based on your age.")
def show_workout_window(name, bmi, bmi_cat, workout):
    workout_window = tk.Toplevel(root)
    workout_window.title(f"Workout for {name}")
    workout_window.configure(bg="#e0f7fa")
    workout_text = tk.Text(workout_window, width=50, height=10, font=("Helvetica", 12), bg="#ffffff", fg="#00695c")
    workout_text.pack(padx=20, pady=20, expand=True, fill='both')
    workout_info = f"Name: {name}\nBMI: {bmi} ({bmi_cat})\nAssigned Workout:\n"
    workout_info += '\n'.join(workout) 
    workout_text.insert(tk.END, workout_info)
root = tk.Tk()
root.title("Workout Generator")
root.configure(bg="#f0f4c3")
root.geometry("800x600")
label_name = tk.Label(root, text="Name:", bg="#f0f4c3", font=("Helvetica", 12, "bold"))
label_name.pack(pady=(10, 0))
entry_name = tk.Entry(root, bg="#ffffff", fg="#4e342e", font=("Helvetica", 10), width=40)
entry_name.pack(pady=(0, 10))
label_age = tk.Label(root, text="Age:", bg="#f0f4c3", font=("Helvetica", 12, "bold"))
label_age.pack(pady=(10, 0))
entry_age = tk.Entry(root, bg="#ffffff", fg="#4e342e", font=("Helvetica", 10), width=40)
entry_age.pack(pady=(0, 10))
label_height = tk.Label(root, text="Height (cm):", bg="#f0f4c3", font=("Helvetica", 12, "bold"))
label_height.pack(pady=(10, 0))
entry_height = tk.Entry(root, bg="#ffffff", fg="#4e342e", font=("Helvetica", 10), width=40)
entry_height.pack(pady=(0, 10))
label_weight = tk.Label(root, text="Weight (kg):", bg="#f0f4c3", font=("Helvetica", 12, "bold"))
label_weight.pack(pady=(10, 0))
entry_weight = tk.Entry(root, bg="#ffffff", fg="#4e342e", font=("Helvetica", 10), width=40)
entry_weight.pack(pady=(0, 10))
label_level = tk.Label(root, text="Fitness Level:", bg="#f0f4c3", font=("Helvetica", 12, "bold"))
label_level.pack(pady=(10, 0))
var_level = tk.StringVar(value='Beginner')
level_options = ['Beginner', 'Intermediate', 'Advanced']
level_menu = tk.OptionMenu(root, var_level, *level_options)
level_menu.configure(bg="#a5d6a7", font=("Helvetica", 10), activebackground="#388e3c", width=36)
level_menu.pack(pady=(0, 10))
submit_button = tk.Button(root, text="Generate Workout", command=on_submit, bg="#81c784", fg="white", font=("Helvetica", 14, "bold"))
submit_button.pack(pady=20)
root.mainloop()
