## Typescript - Tips & Tricks - Index Signature

Welcome back guys, today I'll speak about the _"Index Signature"_.
In some cases, we need to create some special types like dictionaries.
These special types have some keys that identifies the elements and the datas.
A simple example:
```ts
export type User = {
    name: string,
    email: string;
    session: string
}

export type UserDictionary = {
    [username: string]: User
}

const userDictionary: UserDictionary = {
  'myusername': { email: "myemail@email.it", name: "myname", session: "session" },
  'myusername1': {
    email: "myemail1@email.it",
    name: "myname1",
    session: "session",
  },
};

console.log(userDictionary.myusername); // { email: 'myemail@email.it', name: 'myname', session: 'session' }
console.log(userDictionary["myusername"]); // { email: 'myemail@email.it', name: 'myname', session: 'session' }
console.log(userDictionary.myusername1); // { email: 'myemail1@email.it', name: 'myname1', session: 'session' }
console.log(userDictionary["myusername1"]); // { email: 'myemail1@email.it', name: 'myname1', session: 'session' }
delete userDictionary.myusername;

```
In this case, the _UserDictionary_ is a special type where the usernames are the keys of the objects and the user data are the values.
This type is powerful because it permits the consumer to access directly to the data if it knows the keys and it permits to store a unique value of a specific key.
With the index signature, we can create special types where the keys can be string or number.
An important thing that you must remember is that the keys of these objects can be iterated with the for-in loop or with the Object.keys method.
```ts
console.log(Object.keys(userDictionary)); // [ 'myusername', 'myusername1' ]
for (const key in userDictionary) {
  console.log(key);
}
/*
'myusername'
'myusername1'
*/
```

It's all from the _Index Signature_ for today.
Bye-bye guys!