# Full-stack Depth Interview Setup


1. `npm create vite@latest hello-world -- --template react-ts` and follow the prompts OR https://vite.new/react-ts for a browser IDE already setup
2. `npm i vite-plugin-mock-server -D`
3. Copy the below into `vite.config.ts`

```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import mockServer from 'vite-plugin-mock-server'

export default defineConfig({
  plugins: [react(), mockServer()],
});
```

4. `mkdir ./mock && touch ./mock/api.mock.ts`

5. Add the following to the created `./mock/api.mock.ts`

```typescript
import { MockHandler } from 'vite-plugin-mock-server';

export default (): MockHandler[] => [
  {
    pattern: '/api/hello',
    handle: (req, res) => {
      res.statusCode = 200;
      res.setHeader('Content-Type', 'application/json');
      console.log('/api/hello');
      res.end(JSON.stringify({ helloResult: 'Hello world!' }));
    },
  },
]; 
```

6. Call our endpoint, by adding the following in the `App.tsx`

```tsx
const [data, setData] = useState()

useEffect(() => {
  fetch("/api/hello")
    .then(res => res.json())
    .then(data => {
      console.log(data)
      setData(data.helloResult)
    })
}, [])
```
