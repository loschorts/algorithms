# Name

Staircase

# Prompt

Given a staircase of `n` steps, how many different combinations of 1-, 2-, and 3-step steps can you take to get to the top?

# Difficulty

Easy

# Solution

```ruby
	def steps n

		memo = {}

		get_steps = Proc.new do |x|
			return memo[x] if memo[x]
			return 0 if get_steps <= 0
			return 1 if get_steps == 1
			return 2 if get_steps == 2
			return 4 if get_steps == 3

			combos = get_steps(x-1) 
				+ get_steps(x-2) 
				+ get_steps(x-3)
			memo[x] = combos

			combos
		end

		get_steps.call(n)
	end
```

```ruby
	def steps n
		max_threes = n / 3
		max_twos = n / 2

		combos = 0

		0.up_to(max_threes).each do |threes|
			0.up_to(max_twos).each do |twos|
				ones = n - (3 * threes) - (2 * twos)
				steps = ones + twos + threes
				combos += factorial(steps) / threes / twos / ones
			end
		end	

		combos
	end

	def factorial(n)
		result = 1
		n.down_to(1).each do |x|
			result *= x
		end
		result
	end
```

# Subjects

Dynamic Programming
Recursion

# Complexity

Time: 

Recursive: log 3, where 3 is the max step-size
Iterative: n ^ 3

Space: 

Recursive: log 3, where 3 is the max step-size
Iterative: n ^ 2, since n ^ 2 combos are generated
# Takeaways
