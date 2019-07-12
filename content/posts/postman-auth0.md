---
title: "Testing Auth0-protected APIs with Postman"
date: 2019-07-12T15:44:02+02:00
tags: [ "auth0", "postman" ]
subscribe: true
comments: true
share: true
image: "postman-auth0.png"
---

I am a big fan of both Postman and Auth0! Postman makes testing APIs really easy. Auth0 makes authentication for APIs worry free. Unfortunately it is a bit cumbersome to get both tools to play nice together. This is how I managed to get the job done.

<!--more-->

[Postman](https://www.getpostman.com) is the defacto standard for API testing tools today. It's free, easy to use and just plain awesome! You can use it to create, organise and run tests.

When you're developing APIs for you applications, you obviously need to take care of proper authentication and authorization. I use [Auth0](https://auth0.com) for most of my projects, because it's really simple to use and I don't want to build my own user management system. 

Unfortunately it is a bit tricky to get both solutions to play nice together ... But there is a solution!

## The challenge

Once you've [set up your API in Auth0](https://auth0.com/docs/getting-started/set-up-api), you can test your authentication flow. This is where Auth0 has one little quirkiness. As you can see in the example below, Auth0 requires you to send in a header with the audience.

{{< code bash >}}
curl --request POST \
     --url https://<DOMAIN-NAME>.auth0.com/oauth/token \
     --header 'content-type: application/json' \
     --data '{
          "client_id":"<CLIENT-ID>",
          "client_secret":"<CLIENT-SECRET>",
          "audience":"<AUDIENCE>",
          "grant_type":"client_credentials"
      }'
{{< /code >}}

Postman's built-in OAuth authentication flows do not provide the option to set additional headers. The [recommended solution](https://community.auth0.com/t/get-new-access-token-in-postman/7169) by Auth0 is to set the default audience for your account to the desired account. Then, when you don't pass in an audience with your authorization request, that default audience will be used. I don't like that solution, because it means I can only use one audience per account.

## The solution

Luckily Postman offers the concept of [variables](https://learning.getpostman.com/docs/postman/environments_and_globals/variables) and [pre-request scripts](https://learning.getpostman.com/docs/postman/scripts/pre_request_scripts/). Thanks to Google and [Ben Chartrand's script example](https://gist.github.com/bcnzer/073f0fc0b959928b0ca2b173230c0669) I didn't even need to write the script myself! :wink:

I have organised all of my tests for a particular Auth0 audience into a single Postman collection. On that collection, I have set Ben's pre-request script that calls out to Auth0 to authenticate and obtain an access token for that audience. That access token is then assigned to a variable that I use in the collection authentication settings. 

{{< image name="collection" ext="png" lazy="true" alt="Authentication settings on the Postman collection.">}}

Et voila!

