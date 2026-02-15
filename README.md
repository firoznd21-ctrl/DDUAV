import random
class DroneEnv:
    def __init__(self):
        self.position = 0
        self.goal = 10
    def reset(self):
        self.position = 0
        return self.position
    def step(self, action):
        # action: 0 = move forward, 1 = stay
        if action == 0:
            self.position += 1
        reward = -1
        done = False
        if self.position >= self.goal:
            reward = 100     # gate crossed
            
done = True
        return self.position, reward, done
class Agent:
    def __init__(self):
        self.q_table = {}
        self.alpha = 0.1
        self.gamma = 0.9
        self.epsilon = 0.3
    def get_q(self, state, action):
        return self.q_table.get((state, action), 0)
    def choose_action(self, state):
        if random.random() < self.epsilon:
            return random.choice([0, 1])
        else:
            q_forward = self.get_q(state, 0)
            q_stay = self.get_q(state, 1)
            return 0 if q_forward >= q_stay else 1

def learn(self, state, action, reward, next_state):
        old_q = self.get_q(state, action)
        future_q = max(self.get_q(next_state, 0),
                       self.get_q(next_state, 1))
        new_q = old_q + self.alpha * (reward + self.gamma * future_q - old_q)
        self.q_table[(state, action)] = new_q
env = DroneEnv()
agent = Agent()
episodes = 20
for ep in range(episodes):
    state = env.reset()
 for step in range(50):
        action = agent.choose_action(state)

 next_state, reward, done = env.step(action)
        agent.learn(state, action, reward, next_state)
        state = next_state

        if done:
            print(f"Episode {ep+1}: Gate reached in {step+1} steps")
            break

print("\nTraining completed successfully ✅")
