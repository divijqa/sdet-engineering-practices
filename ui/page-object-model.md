# Page Object Model

The Page Object Model centralizes UI behavior so tests describe outcomes and workflows rather than implementation details.

## Boundaries

Page objects expose meaningful actions and state queries. Components model reusable areas such as navigation, tables, or dialogs. Tests own scenario intent and assertions. Keep page objects small, composable, and free of unrelated business logic.

Do not turn page objects into a second application framework. Expose only behavior that improves readability, reuse, or change isolation.
