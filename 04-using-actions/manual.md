

## Exercise: Using Actions
In this practical exercise, our goal is to explore how we can use third-party custom actions to perform tasks without having to define them from scratch.
In order to achieve that, we will leverage a React application that we will scaffold with the help of the `create-react-app` utility.
```sh
name: 04 - Using Actions

on:
  push:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    # 0. Checkout the code from the repository
    # 1. Install dependencies of our React application
    # 2. Execute the automated tests
```

## Solution Steps
1. **Generate a React application**:
   - Create a new folder named `04-using-actions` at the root of the repository.
   - Using a terminal, `cd` into this directory and scaffold a React application inside a `react-app` directory. You can either create the directory yourself or let the `create-react-app` utility do it for you.
   - Once the React setup is done, you should see a success message.
   - Take a few moments to inspect the files and get familiar with the application folder

```yaml
name: 04 - Using Actions

on:
  push:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    # 0. Checkout the code from the repository
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Printing Folders
        run: |
          echo "Printing folder structure..."
          ls -R
    
    # 1. Install dependencies of our React application
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '20.x'

      - name: Install Dependencies
        run: npm ci
        working-directory: 04-using-actions/react-app

    # 2. Execute the automated tests
      - name: Run Unit Tests
        run: npm run test
        working-directory: 04-using-actions/react-app
```