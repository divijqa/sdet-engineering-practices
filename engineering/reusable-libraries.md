# Reusable Libraries

Reusable libraries reduce duplicated automation code without hiding important behavior.

Good candidates include API clients, data builders, authentication helpers, assertions, environment adapters, and evidence collectors. Keep APIs narrow, document assumptions, test libraries independently, and version changes when consumers depend on them.

A library should remove repeated mechanics while leaving test intent obvious at the call site.
