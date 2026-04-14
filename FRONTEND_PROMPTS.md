# Development Prompts: Frontend Edition


Whats working for krishna when he makes quick demos on cursor:

```
Ensure that all the components use shadcnui and reuse as much of the @frontend/src/components as possible. Ensure that you follow the coding guidelines including how all react modules have argument interfaces to ensure that they comply. There should be an easy way to ensure that they comply. Also all network / serverside querying should happen at the page level and not at the component level so it should be pull passing the data through property dirlling. It should then ensure that any form should be using a zod model to capture all the data fields being captured, the parsing errors, etc. 

don't  create any server pages since we use the nimbus backend to serve data. All the sample data should be jsons that are fed to the components in the pages. All the api calls should just be stubs that we will fill out with the correct api calls. 

Make sure that all the application specific components are created in the directory `frontend/src/components/application`

Add all the sample data json to @frontend/src/data
```
