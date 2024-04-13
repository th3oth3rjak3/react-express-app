# Creating a new full stack TypeScript application with Express and React

## Server App
Create a new folder to put both the client and server code in
```bash
mkdir new_app && cd new_app
``` 
Make a server folder for the Express code.
```bash
mkdir server && cd server
touch index.js
```

Initialize the node project.
```bash
npm init -y
```

Add TypeScript support.
```bash
npm i -D typescript
npx tsc --init
```

Update tsconfig.json.
```typescript
{
  "compilerOptions": {
    // …
    "outDir": "./dist"
    // …
  }
}
```

Install dependencies.
```bash
npm i express @types/express
npm i cors @types/cors
```

Rename index.js to index.ts
```bash
mv index.js index.ts
```

Update package.json
```typescript
{
  "name": "server",
  "version": "0.1.0",
  "description": "",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "npx tsc",
    "start": "npx tsc && node dist/index.js",
    "dev": "npx tsc && nodemon dist/index.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cors": "^2.8.5",
    "express": "^4.19.2",
    "nodemon": "^3.1.0"
  },
  "devDependencies": {
    "@types/cors": "^2.8.17",
    "@types/express": "^4.17.21",
    "typescript": "^5.4.5"
  }
}
```

## Client App
Change directories to the root
```bash
cd ..
```

Create a new React App with Vite
```bash
npm create vite@latest client 
```

Follow the prompts and choose React with TypeScript.

Update the vite.config.js file to add a proxy to the server address.
```typescript
// client/vite.config.js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: { // add this code
    proxy: {
      '/api': {
        target: 'http://localhost:5000',
        changeOrigin: true
      }
    }
  }
})
```

In the example code, you will find that I added a button to the main app to make a fetch request to the server endpoint.

For more information about getting started with a fullstack app, see [React-Express](https://github.com/Techtonica/curriculum/blob/main/pair-programming/week-7/react-express-app/react-expressjs.md).