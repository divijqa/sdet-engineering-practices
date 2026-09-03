# Locator Strategy

Locators are part of the test contract. They should survive presentation changes while remaining specific enough to detect regressions.

## Preference order

1. Accessible role and name.
2. Label or associated form text.
3. Stable test identifiers owned by the product team.
4. Stable domain attributes.
5. CSS or XPath only when the structure is the behavior being tested.

Avoid positional selectors, styling classes, and long descendant chains. A locator failure should point to a meaningful product change, not incidental markup movement.
