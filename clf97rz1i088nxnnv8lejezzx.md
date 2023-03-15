---
title: "React Query - useQuery"
datePublished: Wed Mar 15 2023 05:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clf97rz1i088nxnnv8lejezzx
slug: react-query-usequery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/aZsn0bJYqBU/upload/52ec4822b648fb481862c9cdb77091a2.jpeg
tags: reactjs, reacthooks, reactquery

---

Hey Folks,  
It's time to take a journey on [react query](https://tanstack.com/query/latest). Don't you know it? Perfect, you are in the right place 😁

## Introduction

What is React Query? React query is an npm library created by [@TannerLinsley](https://twitter.com/tannerlinsley).  
It's a state manager for react that simplifies many tasks like handling the HTTP request state, saving data in the client to prevent many requests, sharing data in your application using hooks and so on.  
You'll discover more in this series about it, learn how to use it, and appreciate its simplicity in your react applications.

## useQuery

The first core concept is useQuery. Through it, you can retrieve data from a source and handle all the states of this request in a very simple way.  
Let's see an example

```typescript
import { useQuery } from '@tanstack/react-query';

const fetchTodos = async (): Promise<Todo[]> => {
  const response = await fetch('api/tasks');
  if (!response.ok) {
    throw new ResponseError('Failed to fetch todos', response);
  }
  return await response.json();
};

export const useTodos = (): UseTodos => {
  const {
    data: todos = [],
    isLoading,
    isFetching,
    error,
  } = useQuery(['todos'], fetchTodos, {
    refetchOnWindowFocus: false,
    retry: 2,
  });
...
};
```

In this example, you can see the essentials of useQuery.  
UseQuery is a react hook; it takes 3 params:

* The query key
    
* The query function
    
* The configurations
    

Let's start with the first one. The query key is a key used by react query to identify your queries; through the key, react query is able to store the result and use it in different parts of the application. The key is used to identify the query, and with it you can also reset the query or change the value by code using the React Query Client.

The query function is the method used to retrieve data from a source (rest, graphQL, etc. etc.). It's simple; a function that returns a kind of data could be a simple function or, in most cases, a promise.

Configurations, ok these are simple :) There are many possible options to run the query in different ways (amount of retries, when refreshing the data, how to cache the data and so on..)

The result of this hook has three important objects instead

* data; this object contains the result of your query function. Please, pay attention that the data could be undefined too; this is because on the first call when the request is pending, data is not yet presented
    
* isLoading; this flag indicates when react query is loading data. There is also the isFetching flag, which is important if you are creating infinite scrolling. The isFetching flag indicates that there is a request pending, which is perfect if the app is asking for the next info
    
* error: this object contains the error if your request has a problem; using it, you can get the error and create a pretty info message for the user
    

Ok, you have an idea of how useQuery works and what its potentialities are, but if you are more interested in it, you can watch my video to learn more about it.

%[https://www.youtube.com/watch?v=q2r2yoq5zaQ] 

ok, that's all! I'll get back to you with another react query feature soon.

I hope you enjoyed this content.

Bye Bye 👋

p.s. you can find the code of the video [here](https://github.com/Puppo/learning-react-query/tree/01-queries)