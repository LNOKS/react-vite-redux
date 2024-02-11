![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB)
![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white)
![Redux](https://img.shields.io/badge/redux-%23593d88.svg?style=for-the-badge&logo=redux&logoColor=white)
![Vite](https://img.shields.io/badge/vite-%23646CFF.svg?style=for-the-badge&logo=vite&logoColor=white)

## Project structure

```
src/
├── api/                    => RTK Query for API calls
    ├── baseApi.ts          => base API instance
├── redux/                  => Redux store
    ├── auth/               => authentication slice
    ├── user/               => user slice
    ├── store/              => combine all slices
        ├── index.ts
    ├── hooks/              => Redux hooks
        ├── index.ts          
├── components/             => shared components
├── pages/                  => pages
├── utils/                  => utility functions
├── App.tsx                 => main component
├── main.tsx                => entry point

env-example                 => example of environment variables
index.html                  => main html file
```


## RTK Query Overview

RTK Query is a powerful data fetching and caching tool designed to simplify server-state management in web applications. Built on top of Redux, it provides developers with a set of tools to efficiently load and cache asynchronous data from APIs, while also reducing the amount of boilerplate code needed to manage complex state. This makes it an ideal choice for React applications that interact with external APIs.

### Key Features

- **Automatic Caching:** Reduces unnecessary network requests by reusing cached data.
- **Polling:** Supports automatic polling of endpoints to keep data fresh.
- **Data Transformation:** Allows for the transformation of data before it's stored or fetched.
- **Optimistic Updates:** Facilitates optimistic UI updates for a better user experience.

### Structure within the Project

The `src/api/` directory is dedicated to RTK Query logic, focusing on API calls management. Here's how it's structured:

- **`baseApi.ts`**: This file creates the base API slice using `createApi` from RTK Query. It defines the foundation for making API calls, including setting up endpoints and configuring base URLs and headers.

#### Creating an API Slice

An API slice in RTK Query is created using the `createApi` function, which encapsulates the logic for fetching data from an API. Here's a simplified example:

```typescript
// src/api/baseApi.ts
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

export const baseApi = createApi({
    reducerPath: 'api',
    baseQuery: fetchBaseQuery({ baseUrl: '/api' }),
    endpoints: (builder) => ({
        // Define endpoints here
    }),
});
```

#### Using the API Slice

After defining the API slice, you can create hooks for your endpoints. These hooks are then used within your components to fetch data:

```typescript
// Using an auto-generated hook from an endpoint
const { data, error, isLoading } = useGetUserDataQuery(userId);
```

### Integration with Redux Store

The API slice created by RTK Query is integrated into the Redux store to manage the state of API calls. This integration is handled in the `src/redux/store/index.ts` file, where the API slice's reducer is added to the store:

```typescript
// src/redux/store/index.ts
import { configureStore } from '@reduxjs/toolkit';
import { baseApi } from '../../api/baseApi';

export const store = configureStore({
    reducer: {
        // Other reducers
        [baseApi.reducerPath]: baseApi.reducer,
    },
    // Adding the api middleware
    middleware: (getDefaultMiddleware) =>
        getDefaultMiddleware().concat(baseApi.middleware),
});
```

### Conclusion

RTK Query streamlines the process of working with server-side data in React applications, offering features like caching, polling, and automatic re-fetching. By organizing API logic in a dedicated directory and integrating it with the Redux store, projects can maintain a clean and scalable structure. This setup ensures that components remain focused on UI logic, delegating data management responsibilities to RTK Query and Redux.


## About us
### Ready to see what's beyond? Check out our website to discover more projects and learn how we're making a difference: [Discover More](https://lnoks.com).
<img src="https://api.lnoks.com/api/files/gpdni4nbyo5aj5b/ckzlbh3iiyt5n83/logo_purple_pure_hqhbjiEXbL.svg?token=" alt="drawing" width="200" height="100"/>

