#assignment 4 im24001
import random
import matplotlib.pyplot as plt
from collections import Counter

class urnSimulation:
    def __init__(self, white_balls, black_balls, total_draws, trials):
        self.white_balls = white_balls
        self.black_balls = black_balls
        self.total_balls = white_balls + black_balls
        self.total_draws = total_draws
        self.trials = trials
    
  def simulate(self):
        results = []
        urn = ['W'] * self.white_balls + ['B'] * self.black_balls
        for i in range(self.trials):
            drawn_balls = random.sample(urn, self.total_draws)
            white_count = drawn_balls.count('W')
            results.append(white_count)
        return results
    
  def estimate_probability_distribution(self):
        simulation_results = self.simulate()
        counts = Counter(simulation_results)
        total_trials = sum(counts.values())
        prob_distribution = {outcome: count / total_trials for outcome, count in counts.items()}
        return prob_distribution
    
  def plot_distribution(self):
        prob_distribution = self.estimate_probability_distribution()
        plt.bar(prob_distribution.keys(), prob_distribution.values(), color='pink')
        plt.xlabel('Number of White Balls Drawn Randomly')
        plt.ylabel('Estimated Probability')
        plt.title('Estimated Probability Distribution of White Balls Drawn')
        plt.xticks(range(min(prob_distribution.keys()), max(prob_distribution.keys())+1))
        plt.show()


simulation = urnSimulation(white_balls=4, black_balls=6, total_draws=5, trials=1000000)
simulation.plot_distribution()
print(simulation.estimate_probability_distribution)


"temp"
