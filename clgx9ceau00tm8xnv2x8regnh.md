---
title: "React Query - Enable Query"
datePublished: Wed Apr 26 2023 05:30:42 GMT+0000 (Coordinated Universal Time)
cuid: clgx9ceau00tm8xnv2x8regnh
slug: react-query-enable-query
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/aZsn0bJYqBU/upload/41952fde5598669536186df4af62205d.jpeg
tags: reactjs, reacthooks, reactquery

---

Hey folks,  
Do you know that you can enable or disable a query in react query? Noooo! Ok, it's time to learn it!

Some specific hooks must be enabled only if there are some data in the application; for instance, some queries must run only if the users are logged in.  
To solve this problem, the `useQuery` hooks accept an option called `enabled` that accepts a boolean to determine if a condition is true or false.  
Let's take a look at this example

```typescript
import { useQuery } from '@tanstack/react-query';
import { QUERY_KEY } from 'src/app/constants/queryKeys';
import { Todo } from 'src/app/models';
import { User, useUser } from '../../../../auth/useUser';
import { ResponseError } from '../../../../utils/Errors/ResponseError';

const fetchTodos = async (user: User): Promise<Todo[]> => {
  const response = await fetch(`api/tasks?assigneeId=${user.user.id}`, {
    headers: {
      Authorization: `Bearer ${user.accessToken}`,
    },
  });
  if (!response.ok) {
    throw new ResponseError('Failed to fetch my todos', response);
  }
  return await response.json();
};

interface UseMyTodos {
  todos: Todo[];
  error?: string;
}

function mapError(error: unknown | undefined): undefined | string {
  if (!error) return undefined;
  if (error instanceof ResponseError) return error.response.statusText;
  if (error instanceof Error) return error.message;
  return 'Unknown error';
}

export const useMyTodos = (): UseMyTodos => {
  const { user } = useUser();

  const { data: todos = [], error } = useQuery(
    [QUERY_KEY.myTodos],
    () => fetchTodos(user!),
    {
      refetchOnWindowFocus: false,
      retry: 2,
      enabled: !!user,
    }
  );

  return {
    todos,
    error: mapError(error),
  };
};
```

As you can notice, in this case, a custom hook calls the API and gets all the todos assigned to the current users.  
The key point of this example stands in the enabled option. As you can see, this `useQuery` is called only if there is a user; else, the query is stopped.  
This feature permits developers to be sure to call a specific API only if a condition is satisfied, preventing a bad API request.  
This feature is pretty simple but very powerful, as you can imagine!

To find out more about the `enabled` option take a look at my youtube video about it

%[https://www.youtube.com/watch?v=5JSD_b2slJs] 

Ok, that's all from the enabled option.

I hope you enjoyed this content!

See you soon folks

Bye Bye 👋

p.s. you can find the code of the video [**here**](https://github.com/Puppo/learning-react-query/tree/07-enable-query)