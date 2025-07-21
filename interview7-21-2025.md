## 1. Tell me about your current project

I’m working on United.com’s React migration project. We’re converting legacy .NET modules to React with a strong focus on accessibility, performance, and security. I lead the UI side—building components using React 18, Redux-Saga, and integrating them with backend services over REST and xAPI. We also embed the frontend into AEM containers for CMS-driven rendering.

## 2. Which hooks did you work on?

I use `useState`, `useEffect`, `useRef`, `useCallback`, `useMemo`, and `useContext` regularly. For example, I use `useMemo` for memoizing heavy computations and `useCallback` for preventing unnecessary re-renders in child components. I also write custom hooks when logic needs to be reused across components.

## 3. Authentication and Authorization—how did you handle it?

For frontend auth, I used tokens (usually JWTs) stored in memory or HTTP-only cookies. Based on user roles returned from the backend, I conditionally render routes and UI elements. On login, we fetch user details and permissions, store them in Redux, and use them for access control in the UI.

## 4. Redux?

Yes, I’ve used both classic Redux and Redux Toolkit. In my current project, we use Redux-Saga for handling async flows like API calls, and selectors for memoization. I organize state using slices and modular patterns, especially in larger applications.

## 5. Which version of React.js?

I’m currently using React 18. I’ve worked with features like automatic batching, concurrent rendering (with Suspense), and improved SSR support. Most projects I’ve led used React 16+ initially, and we've migrated to 18 over time.

## 6. Error boundaries?

Yes, I use class-based components as error boundaries. It helps catch rendering errors in child components without crashing the whole app. I wrap key parts of the UI (like dynamic dashboards or user forms) with error boundaries and log errors using Sentry.

## 7. React with Java—how did you deal?

The React frontend interacts with Java-based backend via REST APIs. We use Axios/fetch to call APIs, handle tokens for auth, and parse JSON responses. I work closely with backend teams to align on contracts and test integration flows using Postman or Swagger before wiring up the UI.

## 8. Virtual DOM vs Real DOM—what's the difference?

The virtual DOM is a lightweight JS copy of the real DOM. React uses it to figure out the minimal changes needed and applies them efficiently to the real DOM. This diffing and batching reduces direct manipulation, making rendering faster and more optimized.

## 9. Internationalization (i18n)?

I’ve used libraries like `react-i18next` for i18n. We create translation JSON files for each language and load them dynamically. I also handled RTL (right-to-left) support and fallback languages. The AEM setup helped manage language content for global sites.

## 10. Route protection in React application?

I use wrapper components or higher-order components that check auth state before rendering routes. For example, a `<PrivateRoute>` checks if the user is authenticated (from Redux or Context), and redirects to login if not. Same goes for role-based routes.

## 11. Multi-step form with persistent data (even on navigation away)?

I manage multi-step form state in Redux or Context. To persist it across sessions or page reloads, I use `localStorage` or `sessionStorage`. Each step updates a slice of the global state, and on submission, we compile and send the complete payload to the backend.

## 12. How to make an API call in frontend?

Typically with Axios or fetch. I structure API calls in service files. In Redux-Saga, I use generator functions to make async calls and dispatch actions based on success or failure. I also show loading spinners and handle error states gracefully.

## 13. Context API?

I’ve used it when the state doesn't require Redux-level complexity—like theme toggles, language switchers, or user session data. I define a context provider and use `useContext` hook to access state in child components.

## 14. How did you integrate frontend and backend process?

We define API contracts first (REST or GraphQL). I use Postman to test them. Once confirmed, I write services in the frontend using Axios, manage state via Redux, and ensure type consistency using TypeScript. I also handle error cases and retry logic for robustness.

## 15. Authentication in backend—how did you implement?

In backend projects with Node or Java, I’ve implemented JWT-based auth. On login, the backend validates credentials, signs a token, and sends it to the frontend. Backend middleware checks for token validity on each request, along with role/permission validation for sensitive endpoints.

## 16. What is a Higher-Order Component (HOC) in React?

A Higher-Order Component (HOC) is a function that takes a component and returns a new component with additional functionality.

Think of it as a pattern for reusing component logic without duplicating code.

### Example:

```jsx
const withLoader = (WrappedComponent) => {
  return function WithLoaderComponent({ isLoading, ...props }) {
    if (isLoading) {
      return <div>Loading...</div>;
    }
    return <WrappedComponent {...props} />;
  };
};

// Usage
const UserListWithLoader = withLoader(UserList);
```

In the example above, `withLoader` is a HOC that wraps any component and adds a loading UI based on props.

## When I used HOC:

At United, I used HOCs to wrap protected routes with auth checks and also to inject layout or common behaviors like error handling, logging, or feature toggling into reusable modules.

## Key Notes:

- HOCs don’t modify the original component—they return a new one.
- **Common use cases**: authentication, layout wrappers, logging, performance monitoring.
- They follow the pattern:
  ```js
  const EnhancedComponent = hoc(WrappedComponent);
  ```

## What are Custom Hooks in React?

Custom Hooks are JavaScript functions that start with `use` and let you reuse stateful logic across multiple components.

They help avoid duplication and keep components clean by abstracting common logic.

---

## Example: `useWindowWidth`

```jsx
import { useState, useEffect } from "react";

function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener("resize", handleResize);

    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return width;
}

// Usage in a component
function Dashboard() {
  const width = useWindowWidth();

  return <div>Current width: {width}px</div>;
}
```

## When I used Custom Hooks:

At United and Visa, I created several custom hooks to manage:

- **Debounced search input** (`useDebounce`)
- **Tracking scroll position** (`useScrollPosition`)
- **Form validation logic** (`useFormState`)
- **Media query handling for responsive behavior** (`useMediaQuery`)
- **Fetch abstraction** (`useApi` with loading/error/state management)

These hooks helped isolate logic, reduce duplication, and made components much more maintainable.

---

## Key Notes:

- Custom hooks can call other hooks inside them.
- Great for reusing logic without repeating it in every component.
- Should always start with the word `use` to follow React rules.
