# ADR-002: ML.NET Fallback for OpenAI API Quota Exhaustion

## Status
Accepted – April 2026

---

## Context
The Categoriser tool uses OpenAI’s API to generate natural language explanations for expense categorization.  
However, API usage is subject to quota limits and potential outages.  
We needed a fallback mechanism to ensure the system remains functional even when OpenAI is unavailable.

Options considered:
1. **Fail silently** – No explanation returned when quota is exhausted.
2. **Static rule-based text** – Predefined messages for each category.
3. **ML.NET fallback** – Use a lightweight ML.NET model to generate explanations based on category rules.

---

## Decision
We chose **ML.NET fallback** as the solution.  
When OpenAI quota is exhausted, the system automatically switches to ML.NET rule‑based text generation.  
This ensures explanations are always available, even if less sophisticated.

---

## Consequences
### Positive
- Guarantees continuity of user experience (no blank outputs).
- Demonstrates resilience and responsible AI design.
- Easy to maintain and extend with new rules.
- No additional external dependency beyond ML.NET.

### Negative
- Explanations are less natural and engaging compared to OpenAI.
- Requires maintaining two logic paths (OpenAI + ML.NET).
- Adds complexity to testing and validation.

---

## Alternatives Considered
- **Fail silently**: Simplest, but poor user experience.
- **Static text**: Reliable, but too rigid and repetitive.
- **Third‑party APIs**: Possible, but adds cost and dependency risk.

---

## References 
- Microsoft Docs: [ML.NET Overview](https://learn.microsoft.com/en-us/dotnet/machine-learning/)  
