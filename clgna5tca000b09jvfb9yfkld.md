---
title: "React Query - Filter Your Data"
datePublished: Wed Apr 19 2023 05:55:52 GMT+0000 (Coordinated Universal Time)
cuid: clgna5tca000b09jvfb9yfkld
slug: react-query-filter-your-data
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/aZsn0bJYqBU/upload/41952fde5598669536186df4af62205d.jpeg
tags: reactjs, reacthooks, react-query

---

Hey folks,  
Did you know that you can filter your data in react query? Noooo! Ok, it's time to learn it!

To filter the data in your `useQuery` hook, you have to handle the `select` option. This option accepts a function that is used to filter the data.  
The function has one parameter, and this parameter contains the result of the query; the scope of the select function is to manipulate the query's result and returns a new result that respects some rules.

Let's take a look at this example

```typescript
import { useQuery } from '@tanstack/react-query';
import { Dispatch, SetStateAction, useCallback, useState } from 'react';
import { QUERY_KEY } from 'src/app/constants/queryKeys';
import { Todo } from 'src/app/models';
import { ResponseError } from '../../../../utils/Errors/ResponseError';

const fetchTodos = async (): Promise<Todo[]> => {
  const response = await fetch('api/tasks');
  if (!response.ok) {
    throw new ResponseError('Failed to fetch todos', response);
  }
  return await response.json();
};

interface UseTodos {
  todos: Todo[];
  isLoading: boolean;
  isFetching: boolean;
  error?: string;
  setUserFilter: Dispatch<SetStateAction<number | null>>;
}

function mapError(error: unknown | undefined): undefined | string {
  if (!error) return undefined;
  if (error instanceof ResponseError) return error.response.statusText;
  if (error instanceof Error) return error.message;
  return 'Unknown error';
}

export const useTodos = (): UseTodos => {
  const [userFilter, setUserFilter] = useState<number | null>(null);

  const filterTodoByAssignee = useCallback(
    (todos: Todo[]) => {
      if (!userFilter) return todos;
      return todos.filter((todo) => todo.assigneeId === userFilter);
    },
    [userFilter]
  );

  const {
    data: todos = [],
    isLoading,
    isFetching,
    error,
  } = useQuery([QUERY_KEY.todos], fetchTodos, {
    refetchOnWindowFocus: false,
    retry: 2,
    select: filterTodoByAssignee,
  });

  return {
    todos,
    isLoading,
    isFetching,
    error: mapError(error),
    setUserFilter,
  };
};
```

As you can notice, this example has some key points to analyse.  
First, the `filterTodoByAssignee` function is the select function passed to the `useQuery` hook. This function checks the `userFilter` state, and if it is empty, the function returns the entire list; else, it filters the result and returns only the todos that have the `assigneeId` that matches with the `userFilter` value.  
It's important, in this case, to use the `useCallback` hook and pass to it the right dependencies to prevent a decrease in the performance of the application.  
Then another important thing is the `setUserFilter` function that it's used to set the `userFilter` value. This function is exposed by the custom hook to permit the users to change the filter.

And that's all; in these two simple steps, you have a `select` function to filter the dataset got from the query. You can use this solution also to create a client-side pagination in your react query application (for the server-side pagination, there will be a post in the future)

If you want to find out more, check my youtube video about this topic

%[https://www.youtube.com/watch?v=H4l1QAA4Dxw] 

Ok, that's all from the select option!

I hope you enjoyed this content!

See you soon folks

Bye Bye 👋

p.s. you can find the code of the video [**here**](https://github.com/Puppo/learning-react-query/tree/06-query-filters)