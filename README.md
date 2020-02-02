https://www.howtographql.com/react-apollo/2-queries-loading-links/


GraphQl Server - spec ??
- need to build a GQL server
- use any programming language or
- and use one of the reference implementations or
- use [graphcool](https://www.graph.cool) - backend-as-a-service or BaaS - (vs. Prisma?) that provides a server out of the box

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

Update: postedBy started working when the query in LinkList was updated to:

```js
const FEED_QUERY = gql`
  {
    feed {
      links {
        id
        createdAt
        url
        description
        postedBy {
          id
          name
        }
        votes {
          id
          user {
            id
          }
        }
      }
    }
  }
`;
```

from

```js
const FEED_QUERY = gql`
  {
    feed {
      links {
        id
        createdAt
        url
        description
      }
    }
  }
`;
```

Check

`export const FEED_QUERY = gql`

on LinkList
