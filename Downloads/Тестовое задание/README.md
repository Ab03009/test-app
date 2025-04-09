# Vue Todo Application

Simple SPA application built with Vue 3 and TypeScript that allows users to manage a list of tasks.

## Features

- Loads tasks from a JSON file
- Allows marking tasks as completed
- Persists task state across page reloads using localStorage
- Built with Vue 3 and TypeScript

## Project Setup

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

## Implementation Details

- Tasks are initially loaded from `public/tasks.json`
- Task state is persisted in the browser's localStorage
- Uses Vue 3 Composition API with TypeScript
- Responsive design with CSS