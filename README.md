# Test Project:

**ONLY ONE** of the following test tasks should be completed.
**Each test can be done within one hour.**
If you need more time, please let us know.
You can stop after one hour and send us the result.
Choose one of the frameworks: Angular or Svelte and use Typescript.

## Test V1: Exercise Timer

Create a home workout exercise timer where the user can determine:

- the total number of exercises (default: 5)
- the number of supersets within the time window (default: 3)
- the duration of each sub-exercise (default: 30s)
- the time taken to switch (superset pause) (default: 5s)
- the time between superset exercises to take a break (default: 60s)
- start the timer and optionally pause it

### Example:

Here's an example of how it should work: [YouTube Example](https://www.youtube.com/watch?v=T2lyoAhcnXI) 
- Notice: in the example there is no "set-break"!

```
- Start
  - 5x Exercise
    - 3x Set
      - Timer counts down from 30s to 0 (First sub-exercise)
      - Timer counts down from 5s to 0 (set-break)
      - Timer counts down from 30s to 0 (Second sub-exercise)
      - if not the last set: Timer counts down from 5s to 0 (set-break)
      - ... and so on
    - 1x Break
      - if not the last exercise: Rest for 60s
- Finished
```


### Code

- Visually indicate the mode the user is currently in (Start/Set break/Exercise/Big - break/Finished)
- Emphasis is placed on functionality and code quality
- Optional: Attractive design, here you can show off with your UI skills, surprise us 😀
- Optional: "Bing" sound between exercise break transitions
- Don't get bogged down in the details, just make it work, keep it simple and efficient
  



## Test V2: Fancy Table

Create a "functional" table (like a spread sheet) where rows can be filtered, sorted, and the table paginated.

- User can sort (eg: clicking on the column header)
- User can filter/search (input-field)
- User can determine the number of entries per page
- User can change pages
- User can hide/show columns (think of how to do this in a good way)

An example JSON file is provided as the data source (src/assets/database.json). Just import it into the file or fetch() it from GitHub.

### Code

- Emphasis is placed on functionality and code quality
- Optional: Attractive design - Surprise us with your UI/UX skills 😀
- Optional: Mobile-friendly design: think about how to make the table responsive


## Setup

This project uses [Vue](https://vuejs.org/) with [Vite](https://vitejs.dev/).
To start the development server run:

```bash
npm install
npm run dev
```

The app will be available at `http://localhost:5173` by default.

This setup comes preconfigured with **Tailwind CSS v4** and **DaisyUI v5**. Styles are imported in `src/style.css` using the new `@import "tailwindcss"` syntax with DaisyUI.

The default page shows a simple exercise timer component styled with DaisyUI.
