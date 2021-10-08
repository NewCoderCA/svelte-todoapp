# Get started 
This is a 'To Do List' project built and created for better practical understanding of the Svelte framework

- Check you have Node.js installed (If not, visit nodejs.org and install https://nodejs.org/en/download/package-manager/)

```bash
node -v
```

- Go to the Terminal and type 

```bash
npx degit sveltejs/template svelte-app[or whatever name your project is]
```

- Go inside the folder you have just created 

```bash
cd svelte-app
ls -l
```

- Install the dependencies for the project app

```bash
cd svelte-app
npm install
```

- Then start the live development center/ the website:

```bash
npm run dev
```

- Click on the link and navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.


## Building and running in production mode
To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).


## Deploying to the web

### With [Vercel](https://vercel.com)

Install `vercel` if you haven't already:

```bash
npm install -g vercel
```

Then, from within your project folder:

```bash
cd public
vercel deploy --name my-project
```

### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build
surge public my-project.surge.sh
```
