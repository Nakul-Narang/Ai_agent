# -----------------------------------
# Simple Multi-Agent System (No ADK)
# -----------------------------------

class MemoryBank:
    def __init__(self):
        self.data = {}

    def add(self, key, value):
        self.data.setdefault(key, []).append(value)

    def get(self, key):
        return self.data.get(key, [])


impact_memory = MemoryBank()

# ----------------------------
# 1. Carbon Calculator Agent
# ----------------------------
def carbon_calculator(inputs):
    transport = inputs.get("transport_km", 5)
    energy = inputs.get("energy_kwh", 2)

    score = transport * 0.21 + energy * 0.5
    return {"carbon_score": round(score, 2)}

# ----------------------------
# 2. Green Habit Generator
# ----------------------------
def habit_generator(inputs):
    score = inputs["carbon_score"]

    if score > 5:
        habit = "Try cycling short distances and reduce AC usage."
    elif score > 3:
        habit = "Use a fan instead of AC and reduce plastic waste."
    else:
        habit = "Great job! Keep using public transport."

    return {"habit": habit}

# ----------------------------
# 3. Impact Tracker Agent
# ----------------------------
def track_impact(inputs):
    habit = inputs["habit"]
    impact_memory.add("improvements", habit)
    return {"status": "saved"}

# ----------------------------
# 4. Reward Agent
# ----------------------------
def reward_agent(inputs):
    past = impact_memory.get("improvements")
    count = len(past)

    if count >= 5:
        badge = "🌟 Eco Hero Badge"
    elif count >= 3:
        badge = "🌿 Green Streak Badge"
    else:
        badge = "🍀 Starter Badge"

    return {"badge": badge, "total_actions": count}

# ----------------------------
# 5. Sequential Pipeline
# ----------------------------
def run_pipeline(input_data):
    step1 = carbon_calculator(input_data)
    step2 = habit_generator(step1)
    step3 = track_impact(step2)
    step4 = reward_agent(step3)
    return step4


# Run it
output = run_pipeline({"transport_km": 10, "energy_kwh": 4})
output
