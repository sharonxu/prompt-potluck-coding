# Iterative Error Correction: Getting AI to Fix Its Own Mistakes

- Author: Sharon Xu
- Date: 2025-01-26
- Topic(s): debugging-strategies

## Problem / Use Case

AI coding assistants often generate code with subtle bugs or incorrect assumptions. When you simply ask "fix this bug," the AI might introduce new issues or hallucinate solutions. You need a systematic way to guide the AI toward the correct solution without micromanaging every step.

This pattern is especially useful when:
- The AI's first attempt has logical errors but the structure is correct
- You want the AI to learn from its mistakes within the same session
- You're debugging complex issues where the root cause isn't immediately obvious

## Solution / Strategy

Use a three-step iterative correction pattern:

1. **Show, don't tell**: Provide the exact error message or failing test output
   - Include the **full stack trace**, not just the final error line
   - Add relevant context: input data, environment details, expected vs actual behavior
   - Copy-paste exactly as displayed—don't paraphrase or summarize

2. **Ask for analysis first**: Request the AI to explain what went wrong before fixing
   - Forces chain-of-thought reasoning before code generation
   - Helps you verify the AI understands the root cause

3. **Request targeted fix**: Guide the AI to fix only what's broken, preserving what works
   - Explicitly ask to "preserve working code" to prevent unnecessary rewrites

This prevents the AI from rewriting working code or hallucinating new bugs.

- Model/Tool versions (be specific):
  - Model: Claude 3.5 Sonnet (2024-10-22)
  - Tooling: Cursor v0.43, Warp Terminal

- Key prompt pattern:
  ```
  The code you generated produces this error:
  [paste exact error]
  
  Before fixing it:
  1. Analyze what's causing this specific error
  2. Identify which part of the code needs to change
  3. Then provide a targeted fix that preserves working code
  ```

## Example

### Initial AI-generated code (with bug):
```python path=null start=null
def calculate_discount(price, discount_percent):
    discount = price * discount_percent
    return price - discount

# Test
result = calculate_discount(100, 20)
print(f"Price after 20% discount: ${result}")
```

**Output:** `Price after 20% discount: $1980.0` ❌ (Expected: $80.0)

### Iterative correction prompt:
```
The code produces: "Price after 20% discount: $1980.0" but I expected $80.0 for a 20% discount on $100.

Before fixing:
1. What's causing this incorrect result?
2. What assumption did you make about the discount_percent parameter?
3. Then provide a minimal fix.
```

### AI's analysis and fix:
```python path=null start=null
# Analysis: The bug is treating discount_percent as a whole number (20) 
# instead of a decimal (0.20). The calculation multiplies 100 * 20 = 2000
# instead of 100 * 0.20 = 20.

def calculate_discount(price, discount_percent):
    # Convert percentage to decimal if needed
    if discount_percent > 1:
        discount_percent = discount_percent / 100
    discount = price * discount_percent
    return price - discount
```

**Output:** `Price after 20% discount: $80.0` ✅

**Note:** This example is intentionally simple to illustrate the pattern. For complex multi-file bugs, apply this pattern iteratively to one component at a time.

## Notes

**Why this works:**
- Asking for analysis first engages chain-of-thought reasoning
- The AI is less likely to introduce new bugs when fixing targeted issues
- Providing exact error messages grounds the AI's response in reality

**Trade-offs:**
- Takes slightly longer than "just fix it"
- Requires you to copy/paste error messages
- Best for logical bugs; less effective for architectural issues

**When not to use:**
- When you need a complete rewrite
- When the AI's approach is fundamentally wrong (use a different strategy)
- For trivial syntax errors (just tell the AI directly)
- When the error message is unclear or misleading (investigate the root cause first before prompting)
- After 3+ failed iterations (try a different model, approach, or ask a human)

**Common pitfalls:**
- **AI still hallucinates despite analysis**: Ask it to explain its reasoning step-by-step again, or provide a simpler minimal reproduction
- **Over-explaining confuses the AI**: Balance detail with clarity—focus on observable behavior, not speculation
- **Stuck in a loop**: If the AI keeps making the same mistake, explicitly state what it's doing wrong and what success looks like
- **Multi-file bugs**: Apply this pattern to one component at a time rather than the entire system

**Cost/latency considerations:**
- This pattern typically takes 2-3 exchanges vs. 1, but saves time by avoiding bug loops
- Works well with streaming responses since analysis comes before code

**Variations:**
- **For different error types**: Adapt the analysis questions
  - Compile-time errors: "What syntax or type issue is causing this?"
  - Runtime errors: "What input or state triggered this?"
  - Logical errors: "What assumption or calculation is incorrect?"
- **For non-code outputs**: Works for SQL queries, config files, API requests
  - Example: "This SQL query returns 0 rows but should return 5. Analyze why the JOIN condition might be wrong."
- **For complex codebases**: Narrow scope by asking "Which module/function is most likely responsible?"

## References
- [Chain-of-thought prompting paper](https://arxiv.org/abs/2201.11903)
- Related pattern: "Rubber duck debugging with AI" - explain the problem to the AI as if teaching
