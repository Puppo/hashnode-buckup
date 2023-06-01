---
title: "React Query - Paginated List"
datePublished: Thu Jun 01 2023 06:14:11 GMT+0000 (Coordinated Universal Time)
cuid: clicqqzix000109l2ezqvfblg
slug: react-query-paginated-list
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/o4SzxPgMwV8/upload/c11ec8a06625444d23f47684fe0a8870.jpeg
tags: reactjs, reacthooks, reactquery

---

Hey Folks,

Today it's time to learn how you can paginate a list with ReactQuery.

It's common to create a pagination of a list to improve the user interface of your platform if you are building a list in your application, but also to limitate the work in your API.

Using ReactQuery, building a paginate list is a piece of cake.

You have to follow 3 steps:

1. Create a state to save the value of the current page
    
2. Create a state to save the limit of the pages (the number of elements on every page)
    
3. Fetch the data every time the user changes one of the previous states.
    

But let's see an example that is easier to understand

```typescript
const fetchTodos = async (
  page: number,
  limit: number,
  signal: AbortSignal | undefined
): Promise<{
  totals: number;
  todos: Todo[];
}> => {
  const response = await fetch(`api/tasks?_page=${page}&_limit=${limit}`, {
    signal,
  });
  if (!response.ok) {
    throw new ResponseError('Failed to fetch todos', response);
  }
  const todos: Todo[] = await response.json();
  const totals = Number.parseInt(
    response.headers.get('x-total-count') || '0',
    10
  );

  return {
    totals,
    todos,
  };
};

interface UseTodos {
  todos: Todo[];
  isLoading: boolean;
  isFetching: boolean;
  error?: string;
  pages: number;
  page: number;
  setPage: Dispatch<SetStateAction<number>>;
}

export const useTodos = (): UseTodos => {
  const [page, setPage] = useState<number>(1);
  const [limit] = useState<number>(5);

  const {
    data: { todos, totals } = {
      todos: [],
      totals: 0,
    },
    isLoading,
    isFetching,
    error,
  } = useQuery(
    [QUERY_KEY.todos, page, limit],
    ({ signal }) => fetchTodos(page, limit, signal),
    {
      refetchOnWindowFocus: false,
      retry: 2,
    }
  );

  return {
    todos,
    isLoading,
    isFetching,
    error: mapError(error),
    pages: Math.ceil(totals / limit),
    page,
    setPage,
  };
};
```

As you can notice, the process to build a pagination with ReactQuery is very simple.  
The fetch request has to contain the page and the limit (you can handle a pagination also with limit and offset if you want) and in your `useQuery` you have to handle some simple stuff. First, the key of your query must include the page and limit too, second you must pass page and limit to your fetch request.

As you can see, building a paginated list with ReactQuery is really a piece of cake, but if want to dive into it don't miss my youtube video about it

%[https://www.youtube.com/watch?v=Ma7-hdNMdWs] 

I think that’s all from this article; I hope you enjoyed this content!

See you soon folks  
Bye Bye 👋

p.s. you can find the code of the video [**here**](https://github.com/Puppo/learning-react-query/tree/11-paginate-result)