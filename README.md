https://www.howtographql.com/react-apollo/2-queries-loading-links/

???
https://www.howtographql.com/react-apollo/5-authentication/
You can verify that the new user is there by sending the users query in the dev Playground in the database project.

At the end of https://www.howtographql.com/react-apollo/5-authentication/
server /// resolvers/mutation.js

```js
// function post(parent, args, context) {
//   return context.prisma.createLink({
//     url: args.url,
//     description: args.description,
//   })
// }

function post(parent, { url, description }, context) {
  const userId = getUserId(context);
  return context.prisma.createLink({
    url,
    description,
    postedBy: {
      connect: {
        id: userId,
      },
    },
  });
}
```

WTF is parent and why does the postedBy not contain data?
