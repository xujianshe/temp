# Local Dev of New CICD
If you want to debug local code, just only require two steps :  
1. `npm start`  
2. Append `?=cdn=https://127.0.0.1:4444` to url

How does it work? go deeper.
## what is the overview solution of local dev for new cicd
The new local dev solution is based on the idea that we just want to debug the repos we need and others' repos should be online, so we can avoid repos' version conflicts. 

## How to load assets from local
When we run command "npm start", actually it runs the command like "start seismic-fe-dev-server ./dist/assets && npm run build:dev-newcicd", it will be to do that:

1. The `seismic-fe-dev-server` plugin will start a local server using port 4444 (the port is builded in the plugin), the server folder is `dist/assets`
2. If there are multiple commands(`npm start`), then all repos's assets folder("dist/assets") will be mapped to the server folder
3. Run packaging of webpack with "--watch", packing assets into "dist/assets" in new cicd solution

After it we can access "https://127.0.0.1:4444/static/default/version.js" to check if it works.
the next we will create a association for the online and local by setting the query parameter "cdn=https://127.0.0.1:4444" for online url.  when the page is loading, we ensure that association work through a set of mechanisms, See in detail [Understand NewCICD](5. Understand NewCICD.md)
