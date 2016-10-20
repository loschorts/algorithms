# Name

Longest Common Substring

# Prompt

Given two strings, return the longest common substring using `m`*`n` time and `m`*`n` space, where `m` and `n` are the lengths of the two strings, respectively.

# Difficulty

Easy

# Solution

```

def longest_common_substring(short, long)
	short, long = long, short if long.length < short.length

	buffer = Proc.new { Array.new(short.length - 1)}

	base = buffer + long + buffer
	base.each_index do |i|

		register = Array.new(base.length)

		short.length.times do |j|
			register[i + j] = short[j]
		end

		memo = Array.new(base.length)

		count = 0
		register.each_with_index do |j|
			if base[j] == register[j]
				if base[j-1] != register[j-1]
					sub_st = true
					end
				if base[j+1] != register[j+1] || base[j+1].nil? || register[j+1].nil?
					sub_end = true
				end

				memo[j] = :start if sub_st
				memo[j] = :end if sub_end
				memo[j] = :single if sub_st && sub_end
			else
				memo[j] = :middle
			end

			case memo[j]
			when :single
				count = 1
				longest = count if count > longest
				s = j
				e = j
				end
				count = 0
			when :start
				count = 1
				s = j
			when :middle
				count += 1
			when :end
				count += 1
				e = j
				longest = count if count > longest
				count = 0
			end

			if s & e
				best_s = s if count > longest
				best_e = e if count > longest
			end

		end
	end

	register[s..e]


end
```

[0, 1, 2]
[0, 1]

_ _ _ _ _ 

# Subjects

Arrays
Dynamic Programming

# Complexity

Time: `mn`

Space: `mn`

# Takeaways


