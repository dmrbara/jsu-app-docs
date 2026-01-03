# Naming Conventions

## Project Structure

```
/app                 # Expo Router pages
/components          # Reusable UI components
/hooks               # Custom React hooks
/stores              # Zustand stores
/lib                 # Utilities, helpers, Supabase client
/types               # TypeScript type definitions
/constants           # App-wide constants
```

---

## Files & Folders

| Type | Convention | Example |
|------|------------|---------|
| Components | `PascalCase.tsx` | `QRScanner.tsx`, `DrinkTracker.tsx` |
| Hooks | `use-kebab-case.ts` | `use-auth.ts`, `use-drinks.ts` |
| Stores | `kebab-case-store.ts` | `auth-store.ts`, `drink-store.ts` |
| Utils | `kebab-case.ts` | `date-utils.ts`, `format-helpers.ts` |
| Types | `kebab-case.types.ts` | `user.types.ts`, `event.types.ts` |
| Constants | `kebab-case.ts` | `app-config.ts`, `query-keys.ts` |

### Expo Router Files

| Type | Convention | Example |
|------|------------|---------|
| Layouts | `_layout.tsx` | `app/_layout.tsx` |
| Pages | `kebab-case.tsx` | `app/drink-history.tsx` |
| Dynamic routes | `[param].tsx` | `app/profile/[id].tsx` |
| Route groups | `(group-name)/` | `app/(tabs)/`, `app/(auth)/` |
| Not found | `+not-found.tsx` | `app/+not-found.tsx` |

---

## Code-Level Naming

### Variables & Functions

| Type | Convention | Example |
|------|------------|---------|
| Variables | camelCase | `currentUser`, `drinkCount`, `isLoading` |
| Functions | camelCase | `fetchProfile`, `calculateAge`, `formatDate` |
| Constants | SCREAMING_SNAKE_CASE | `MAX_DRINKS`, `API_URL`, `QUERY_KEYS` |
| Booleans | `is/has/can/should` prefix | `isLoggedIn`, `hasPermission`, `canScan` |

### Components & Types

| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `ProfileCard`, `DrinkCounter`, `QRScanner` |
| Props interface | `ComponentNameProps` | `ProfileCardProps`, `DrinkCounterProps` |
| Types | PascalCase | `User`, `DrinkRecord`, `EventType` |
| Enums | PascalCase | `UserRole`, `DrinkStatus` |
| Enum values | PascalCase | `UserRole.Participant`, `UserRole.Coordinator` |

### Event Handlers

| Context | Convention | Example |
|---------|------------|---------|
| Props (external) | `onAction` | `onPress`, `onSubmit`, `onScan` |
| Internal handlers | `handleAction` | `handlePress`, `handleSubmit`, `handleScan` |

---

## Stack-Specific Conventions

### Zustand Stores

```typescript
// stores/auth-store.ts
interface AuthState {
  user: User | null;
  isLoading: boolean;
  // Actions: verb + noun
  login: (credentials: Credentials) => Promise<void>;
  logout: () => void;
  setUser: (user: User) => void;
}

export const useAuthStore = create<AuthState>()(...);
```

**Store naming:**
- File: `feature-store.ts`
- Hook: `useFeatureStore`
- Actions: `verbNoun` (e.g., `fetchUser`, `setDrinkCount`, `resetState`)

### TanStack Query

```typescript
// constants/query-keys.ts
export const QUERY_KEYS = {
  PROFILE: 'profile',
  DRINKS: 'drinks',
  EVENTS: 'events',
} as const;

// hooks/use-profile.ts
export function useProfile(userId: string) {
  return useQuery({
    queryKey: [QUERY_KEYS.PROFILE, userId],
    queryFn: () => fetchProfile(userId),
  });
}
```

**Query hook naming:**
- Queries: `useFeature` (e.g., `useProfile`, `useDrinks`, `useEvents`)
- Mutations: `useFeatureMutation` (e.g., `useAddDrinkMutation`)

### Supabase

| TypeScript | Supabase Table |
|------------|----------------|
| `User` | `users` |
| `DrinkRecord` | `drink_records` |
| `HouseAssignment` | `house_assignments` |

- Tables: `snake_case` (plural)
- Columns: `snake_case`
- RPC functions: `snake_case` (e.g., `get_drink_count`, `check_age_limit`)

### NativeWind

```tsx
// Inline styles - use className directly
<View className="flex-1 bg-white p-4">

// Reusable style constants (if needed)
const cardStyles = "rounded-xl bg-white p-4 shadow-md";

// Component variants
const buttonVariants = {
  primary: "bg-blue-500 text-white",
  secondary: "bg-gray-200 text-gray-800",
  danger: "bg-red-500 text-white",
};
```

---

## Component Patterns

```tsx
// components/DrinkCounter.tsx
interface DrinkCounterProps {
  count: number;
  maxCount: number;
  onIncrement: () => void;
  isDisabled?: boolean;
}

export function DrinkCounter({
  count,
  maxCount,
  onIncrement,
  isDisabled = false
}: DrinkCounterProps) {
  const handlePress = () => {
    if (!isDisabled && count < maxCount) {
      onIncrement();
    }
  };

  return (
    <Pressable onPress={handlePress} disabled={isDisabled}>
      {/* ... */}
    </Pressable>
  );
}
```

**Key patterns:**
- Named exports for components (not default)
- Props destructured with defaults in function signature
- Internal handlers prefixed with `handle`
- Boolean props prefixed with `is/has/can`
