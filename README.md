

# DemoNx

## Tech Stack:
- React Js
- Next.js
- Electron.js
- Nx workspace

## Note:
1. Use Nx version 14 because latest version (15) does not support electron.

## Step to init:
1. Create a Nx workspace with a default Next.js app:
```
npx create-nx-workspace@14

Workspace name (e.g., org name)     › demo-nx
What to create in the new workspace › next.js
Application name                    › demo-nextjs
```

2. Create an front end app for electron project. I'm using React app:
```
nx g @nrwl/react:application demo-electron-fe-react --style=none --e2eTestRunner=none
```
- Should update baseHref to "./" instead of "/" in project.json

3. Install nx-electron lib: https://github.com/bennymeg/nx-electron
```
yarn add -D nx-electron
```

4. Generate electron app
```
nx g nx-electron:app demo-electron --frontendProject=demo-electron-fe-react
```

5. Generate a React lib to share component between Next.js app and Electron FE React app:
```
nx g @nrwl/react:library ui
```

6. Create a React component in ui lib:
```
nx g @nrwl/react:component header --project=ui
```
- Remember to export the component in `libs/ui/src/index.ts`

7. Use shared component in both Next.js app and Electron FE React app:
```
import { Header } from '@demo-nx/ui';

...

<Header />
```

8. Run electron app:
```
nx serve demo-electron-fe-react
nx serve demo-electron
```

9. Run Next.js app
```
nx serve demo-nextjs
```
- Check to see Header component in both app.

