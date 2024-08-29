# Performance Debugging

## Table of Contents

1. [Profiling With Chrome Devtools and React Profiler](#profiling-with-chrome-devtools-and-react-profiler)

## Profiling With Chrome Devtools and React Profiler

### Record the App’s Activity With Chrome Devtools

When facing a performance issue, open Chrome DevTools' Performance pane. Start by recording the app's activity during the issue. The resulting performance trace will reveal everything happening in the app. Although it might seem overwhelming at first, focus on two key areas: the CPU row, which shows when the main thread was busy, and the main pane, which shows what was happening during those times.

Analyze the CPU spikes to pinpoint where the app slows down. You don't need to inspect every function—just look for the color pattern. If multiple functions share the same color, they likely originate from the same source. In Chrome DevTools, functions from the same file are colored similarly, so if you identify one function as coming from `react-dom development`, you can safely assume others with the same color do too.

### Record the App’s Activity With React Profiler

Here's the situation: The app is slow. Each event in the app triggers a JavaScript task, which then leads to a chain of React code execution. You don't need to understand the code deeply—just recognize that **if React code dominates the performance recording, it’s time to switch to the React Profiler.**

Install the React Developer Tools extension if you haven't already, reload DevTools, and switch to the Profiler tab. Record again the interaction with the Profiler to see every component that renders during your interaction. You'll be able to see all the renders that occurred and identify every component that re-rendered during each render.

After profiling the interaction, identify and prevent unnecessary component re-renders to speed up the interaction.

Optimizing React Code and Effects [^1]

**[⬆ back to top](#table-of-contents)**

[^1]: Ivan Akulov, "React Performance Debugging Masterclass," presented at React Summit 2023, [https://gitnation.com/contents/react-performance-debugging-masterclass](https://gitnation.com/contents/react-performance-debugging-masterclass).
