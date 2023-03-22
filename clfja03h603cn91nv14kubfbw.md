---
title: "React Query - useMutation"
datePublished: Wed Mar 22 2023 06:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clfja03h603cn91nv14kubfbw
slug: react-query-usemutation
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/aZsn0bJYqBU/upload/52ec4822b648fb481862c9cdb77091a2.jpeg
tags: reactjs, reacthooks, reactquery

---

Hey Folks,  
It's time to talk about the second core concept in React Query, mutation.

## What is it?

Mutations are actions that a user can do in your application. You can imagine a mutation as an action to change or create something.  
To understand better in the code what a mutation is, let's start with a code snippet

```typescript
import { useMutation } from '@tanstack/react-query';

const postTodo = async (text: Todo['text']): Promise<Todo> => {
  const response = await fetch('api/tasks', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({ text }),
  });
  if (!response.ok) {
    throw new ResponseError('Failed to insert new todo', response);
  }
  return await response.json();
};

export const useAddTodo = (): UseAddTodo => {
  const { mutate: addTodo, isLoading, error } = useMutation(postTodo, {
    onSuccess: () => {
      // Success actions
    },
    onError: (error) => {
      // Error actions
    },
  });

  return {
    addTodo,
  };
};
```

As you can see, the mutation is a simple hook with two params:

* The function to handle the request
    
* The options to handle, in this case, the success and the error hooks, but also to configure the mutation (retry, retry delay and so on).
    

The result has three main objects:

* mutate: this is the action to run the mutation in your code
    
* isLoading: this flag indicates if the mutation is ongoing
    
* error: this indicates the errors in case there is an error in the request
    

Using mutations in your React applications, you can handle all those actions to mutate the data and simplify the management of the states of these requests.

Another important concept to know when you work with mutation is the [QueryClient](https://tanstack.com/query/v4/docs/react/reference/useQueryClient).  
Using the QueryClient, you can invalidate a query already provided and say to react query to ask again for the data because you are sure that those data are not yet valid after the mutation.  
To do that, you have to use the `useQueryClient` hook to retrieve the queryClient and using the `invalidateQueries` method, you can invalidate the react query cache for a specific query or multiple queries.  
Here you can find an example

```typescript
import { useMutation, useQueryClient } from '@tanstack/react-query';
import { QUERY_KEY } from '../../../../constants/queryKeys';

export const useAddTodo = (): UseAddTodo => {
  const client = useQueryClient();
  const { mutate: addTodo } = useMutation(postTodo, {
    onSuccess: () => {
      client.invalidateQueries([QUERY_KEY.todos]);
    },
  });
  ...
};
```

Ok, I think you have an idea of how useMutation and useQueryClient work, but if you want to dive into them, don't forget to see my Youtube video.

%[https://www.youtube.com/watch?v=Cpxoxj9sTXA] 

Ok, That's all!  
I hope you enjoyed this content, and I'll get back to you soon with another concept of React Query.

Bye Bye 👋

p.s. you can find the code of the video [here](https://github.com/Puppo/learning-react-query/tree/02-mutations)